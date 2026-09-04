# OpenSSL Build

I have such a hard time understanding why developers make things complicated when they simply don’t need to be.

I’m rebuilding the build and release process for Iguana 6. This is critical infrastructure. The process deserves to be linear, transparent and predictable: compile the components, assemble the product, test it, package it, release it.

Instead, the Makefiles I’m replacing are bizarrely complicated. They refer through layers of other Makefiles, abstractions and special cases until it becomes extremely difficult to understand what the build is actually doing.

I almost wanted to cry looking at the original build system. Not because the underlying problem is difficult, but because so much unnecessary complexity had accumulated around something fundamentally simple.

I knew the personalities who created it. One developer was eventually fired by his manager, but for a long time the manager valued him because he could remember enormous amounts of obscure information about the system. That, in retrospect, was part of the problem: the system rewarded knowing the complexity rather than eliminating it.

Good engineering should make obscure knowledge unnecessary.

I’m replacing all of this with something I can read from top to bottom and understand. Dependencies should be explicit. Platform differences should be obvious. Third-party libraries should build in self-contained directories. And when something fails, it should be clear why.

See for yourself — this is the original Makefile I’m replacing. It’s mind-boggling that building Iguana ever needed to be this complicated:

```
###############################################################################
# Wrapper makefile for OpenSSL.
#
# Configure, build OpenSSL-x.y.z and copy over headers and libraries into this
# top-level directory. Other modules requiring OpenSSL headers and libs can use
# openssl_src/include and openssl_src/libs to get at them.
#
# There are also convenience targets for testing OpenSSL in its own harness.
#
# To upgrade OpenSSL in-tree, all that should need to be done is to expand the
# tarball in this directory and change RELEASE to the new release string.
###############################################################################

# Disable warnings for third-party systems
override IFW_MAKE_THIRD_PARTY = 1
# Disable ccache - there are issues when using ccache and ranlib:
# /Library/Developer/CommandLineTools/usr/bin/ranlib: archive member: 
#    ../../libcrypto.a(XXX.o) size too large
#    (archive member extends past the end of the file)
# (the XXX.o object file in question may change between each run)
# There is documentation of this issue, though in a slightly different context:
# https://dev.openwrt.org/ticket/4518
override IFW_MAKE_NO_CCACHE = 1

include ../makefiles/base.makefile

###############################################################################
# Vars and settings
BUILD_LOG = log.openssl-build.txt
CWD := $(abspath ./)

# Platform- and architecture-specific options passed to OpenSSL Configure.
# --prefix is not really used, but it keeps us from accidentally installing
# the OpenSSL we build into a system path.
# CONFIGUREEXTRA is unused internally, but can be set in the environment to
# add some extra flags for testing
CONFIGURE_OPTS += \
--prefix=$(CWD)/dest \
threads \
no-shared \
-DPURIFY \
$(IFW_CONFIGURE_TRIPLE) \
$(CONFIGUREEXTRA)

# Triples used to specify target platform in configure script
ifeq ($(IFW_LINUX), 1)
   # LINUX
   ifeq ($(shell uname -m),aarch64)
      IFW_CONFIGURE_TRIPLE = linux-aarch64
   else
      IFW_CONFIGURE_TRIPLE = linux-x86_64
   endif 
endif
ifeq ($(IFW_MAC), 1)
   # MAC
   ifeq ($(IFW_MAKE_32_BIT), 1)
      IFW_CONFIGURE_TRIPLE = darwin-i386-cc
   else
      IFW_CONFIGURE_TRIPLE = darwin64-x86_64-cc
   endif

endif
ifeq ($(IFW_WIN), 1)
   # WIN
   # TODO: see 22819
   IFW_CONFIGURE_TRIPLE = Cygwin
endif

ifeq ($(IFW_CONFIGURE_TRIPLE),)
   $(error Could not determine configuration triple from makefile settings)
endif

ifeq ($(IFW_LINUX), 1)
   # Include architecture flags to enforce 32/64-bit builds
   CONFIGURE_OPTS += $(IFW_ARCH_FLAGS)
   # Need to explicitly specify -fPIC so that IGCDLL and other shared libraries
   # can correctly include OpenSSL
   CONFIGURE_OPTS += -fPIC
endif


RELEASE=3.0.14
OPENSSL_SRCDIR=openssl-$(RELEASE)

OPENSSL_CONF_H = openssl/opensslconf.h
OPENSSL_CONF_H_SRC = $(addprefix $(OPENSSL_SRCDIR)/include/, $(OPENSSL_CONF_H))
OPENSSL_CONF_H_DEST = $(addprefix include/, $(OPENSSL_CONF_H))
SSL_LIB = libssl.a
CRYPTO_LIB = libcrypto.a
OPENSSL_LIBS = $(SSL_LIB) $(CRYPTO_LIB)
OPENSSL_LIBS_SRC = $(addprefix $(OPENSSL_SRCDIR)/, $(OPENSSL_LIBS))
OPENSSL_LIBS_DEST = $(addprefix lib/, $(OPENSSL_LIBS))

ifeq ($(call ISEMPTYDEFAULT, PLATFORM_OK), 1)
   # Generate a stamp that differentiates between configs
   # this allows for proper rebuilding when switching from, say, Mac to Linux
   PLATFORM_OK = ok_$(IFW_MACHINE_ID)
endif
CFG_OK_STAMP = $(OPENSSL_SRCDIR)/cfg_$(strip $(PLATFORM_OK))
BUILD_OK_STAMP = $(OPENSSL_SRCDIR)/build_$(strip $(PLATFORM_OK))


# Top-level functionality
RMDIST = $(call RM, $(OPENSSL_SRCDIR) lib include $(BUILD_LOG), \
                    $(OPENSSL_SRCDIR))
RMMOST = $(call RM, lib include, openssl/lib openssl/include)

all: | headers libs
headers: $(OPENSSL_CONF_H_DEST)
libs: $(OPENSSL_LIBS_DEST) | headers

info: infoconfig infoid
infoconfig:
	$(call PRINTCMD, CFG:, $(CONFIGURE_OPTS))

.PHONY: libs headers infoconfig

###############################################################################
# Configure
# First, extract the tarball
# Second, apply any patches and fixes
# Third, run openssl-src/Configure

UNTARVERBOSE = gzip -dc "$(strip $(1))" | tar xfm -
ifneq ($(IFW_VERBOSE), 1)
   UNTAR = $(call PRINTCMD, UNTAR, $(strip $(1))) && $(UNTARVERBOSE)
else
   UNTAR = $(UNTARVERBOSE)
endif

# Helper that fixes up the default OpenSSL Makefile to play nice with our
# build system. This regex targets recursive make invocations, expanded via
# variables, to include a '+' prefix in the recipe lines. Without it,
# parallel building reverts back to 1 job only... Sloppy coding on their part
FIXSUBMAKEPROXYTOKENS = \
   (RECURSIVE_BUILD_CMD|BUILD_ONE_CMD|RECURSIVE_MAKE|BUILD_CMD)
FIXSUBMAKEREGEX = \
   s/^(\s*)(@.*)( \$$\($(strip $(FIXSUBMAKEPROXYTOKENS))\))/$$1+$$2$$3/g
FIXSUBMAKECMDSVERBOSE = \
   find "$(strip $(1))" \
      -name "Makefile" -print0 -o \
      -name "Makefile.org" -print0 | \
   xargs -0 perl -pi.orig -e '$(strip $(FIXSUBMAKEREGEX))'

ifneq ($(IFW_VERBOSE), 1)
   FIXSUBMAKECMDS = $(call PRINTCMD, FIX-MK, "$(strip $(1))/**Makefile") && \
      $(FIXSUBMAKECMDSVERBOSE)
else
   FIXSUBMAKECMDS = $(FIXSUBMAKECMDSVERBOSE)
endif

CONFIGUREVERBOSE = export $(1) &&  cd $(OPENSSL_SRCDIR) && \
   ./Configure $(2) >> $(CWD)/$(BUILD_LOG) 2>&1
ifneq ($(IFW_VERBOSE), 1)
   CONFIGURE = +$(call PRINTCMD, CFG, Configure) && $(CONFIGUREVERBOSE)
else
   CONFIGURE = +$(CONFIGUREVERBOSE)
endif

# These intermediate targets can be used for testing, to quickly extract
# and the distribution without configuring/building
extract: tarname = $(OPENSSL_SRCDIR).tar.gz
extract:
	$(call RMDIST)
	$(call UNTAR, $(tarname))


configure: $(CFG_OK_STAMP)

.PHONY: extract configure

$(CFG_OK_STAMP): settings = $(IFW_EXPORT_COMPILER_SETTINGS)
$(CFG_OK_STAMP): tarname = $(OPENSSL_SRCDIR).tar.gz
$(CFG_OK_STAMP):
	$(call RMDIST)
	$(call UNTAR, $(tarname))
	$(call FIXSUBMAKECMDS, $(OPENSSL_SRCDIR))
	$(call CONFIGURE, $(settings), $(CONFIGURE_OPTS))
	$(call PRINTCMD, TOUCH, $@) && touch $@

###############################################################################
# Build
# Treat the local copy as canonical; if it doesn't exist, just rebuild
# it from scratch and copy it over, along with all the other OpenSSL headers.
# We deliberately ignore any copy that may be in the OpenSSL include directory.

ifneq ($(IFW_VERBOSE), 1)
$(OPENSSL_CONF_H_DEST): quiet=@
endif
$(OPENSSL_CONF_H_DEST): | $(BUILD_OK_STAMP)
	$(quiet)mkdir -p include/openssl
	$(call CP, $(OPENSSL_SRCDIR)/include/openssl/*, \
	           $(CWD)/include/openssl, \
	           "include/openssl/*.h")

# NOTE : The invocation of make here resets MAKEFLAGS, which re-enables
#        command printing, and sub-directory printing, regardless of what
#        IFW_VERBOSE is. This is useful for capturing verbose information
#        in the log file, even when building non-verbosely.
SUBMAKEDIR = -C "$(strip $(1))"
SUBMAKETARGETS = $(if $(strip $(2)), $(strip $(2)), build_libs)
# Include header for overriding thread unsafe time function usage within openssl 
# THREADSAFE_HEADER_INC = -include $(CWD)/OpenSSLTimeFixes.h
# SUBMAKEFLAGS = $(THREADSAFE_HEADER_INC) $(strip $(filter-out -s -no-%, $(MAKEFLAGS))) 
SUBMAKEFLAGS = $(strip $(filter-out -s -no-%, $(MAKEFLAGS))) 
SUBMAKEVERBOSE = \
   $(MAKE) MAKEFLAGS="$(SUBMAKEFLAGS)" $(SUBMAKEDIR) \
           $(SUBMAKEOPTS) $(SUBMAKETARGETS) \
      >> $(CWD)/$(BUILD_LOG) 2>&1
ifneq ($(IFW_VERBOSE), 1)
   SUBMAKETARGETDESC = $(strip $(if $(strip $(2)), $(2)))
   SUBMAKE = +$(call PRINTCMD, MAKE, $(strip $(1)) $(SUBMAKETARGETDESC)) \
             && $(SUBMAKEVERBOSE)
else
   SUBMAKE = +$(SUBMAKEVERBOSE)
endif

ifneq ($(IFW_VERBOSE), 1)
lib: quiet=@
endif
lib: | $(BUILD_OK_STAMP)
	$(quiet)mkdir -p lib/

$(OPENSSL_LIBS_DEST): | lib
$(call MAKEMAPPEDRECIPES, $(OPENSSL_LIBS_SRC), $(OPENSSL_LIBS_DEST), \
                          CP, '$$(strip $$@)')

$(OPENSSL_LIBS_SRC): $(BUILD_OK_STAMP)

src: $(BUILD_OK_STAMP)
$(BUILD_OK_STAMP): $(CFG_OK_STAMP)
	$(call SUBMAKE, $(OPENSSL_SRCDIR))
	$(call PRINTCMD, TOUCH, $@) && touch $@

.PHONY: src

###############################################################################
# Clean
# The default 'make clean' command does not remove the dist files
# This allows for subsequent 'make' commands to re-use the already-built files
# instead of rebuilding OpenSSL from scratch
# The use of the machine ID in the configure stamp ensures that any changes to
# compile settings, or build machines, will cause a full RMDIST and rebuild
cleanall: clean-dist clean-mostly
clean: clean-mostly
cleanme: clean-dist
clean-dist:
	$(call RMDIST)
clean-mostly:
	$(call RMMOST)

.PHONY: clean-dist clean-mostly

###############################################################################
# OpenSSL built-in test suite
.PHONY: test
test:
	$(MAKE) $(MAKEOPTS) test
```
This is my replacement, I have to add some more logic for different platform targets but it still won't be that complicated:

```
OPENSSL_TARBALL := $(wildcard openssl-*.tar.gz)
OPENSSL_VERSION := $(patsubst openssl-%.tar.gz,%,$(OPENSSL_TARBALL))
OPENSSL_SOURCE := openssl-$(OPENSSL_VERSION)
OPENSSL_DEST := dest

.PHONY: all
all:
	rm -rf $(OPENSSL_SOURCE) $(OPENSSL_DEST)
	tar xzf $(OPENSSL_TARBALL)
	cd $(OPENSSL_SOURCE) && ./Configure \
		darwin64-arm64-cc \
		--prefix=$(abspath $(OPENSSL_DEST)) \
		threads \
		no-shared
	$(MAKE) -C $(OPENSSL_SOURCE)
	$(MAKE) -C $(OPENSSL_SOURCE) install_sw

clean:
	rm -rf $(OPENSSL_SOURCE) $(OPENSSL_DEST)
```

