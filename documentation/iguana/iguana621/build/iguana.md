# Iguana

It was a lot of work to quietly go through and figure out how
to rebuild the Iguana 6 binary.  I don't understand how most
developers seem to be content to be surrounded by chaos. To me
that seems terribly stressful.

This is new make file.

```
TARGET:=iguana

IW_OPENSSL := 1

DIRS:=\
DBD\
DTI\
html_tools\
DDB\
TIC\
CHC\
CHM\
NFC\
DBL\
DSE\
DWB\
NOW\
ANN\
DLL\
NWB\
NODL\
LUA\
lua514\
TIME\
luax\
CHL\
ANT\
ARF\
JLG\
ARFX\
ATT\
CARC\
CHF\
CHJ\
CHP\
CHX\
LAG\
CMD\
CS\
CSV\
CTT\
CHT\
CURL\
DAP\
DBSQL\
DB\
DBDID\
GUID\
DRS\
DBDRPC\
DBDVER\
DBQ\
DBE\
DBT\
DBU\
DHT\
DIS\
DQU\
DRG\
DTR\
EML\
EVN\
FIL\
FILB\
FMT\
HFIL\
HTPC\
IFWSVC\
IP\
GZIP\
JBB\
JSON\
LAN\
LIC\
LLP\
MLG\
MPH\
MAP\
MT\
MZIP\
NTV\
NLOG\
NOB\
NODB\
NODC\
LOC\
MPRC\
JSC\
NOH\
NOPH\
NOTG\
NOX\
DOM\
NTAB\
NOD\
NTBS\
NTB\
SCM\
DBC\
PER\
PIP\
POD\
PRT\
REG\
IPG\
IPA\
REX\
RGN\
SCC\
SDM\
SGC\
SGM\
SGP\
SGPY\
SGX\
SMTPB\
SMTP\
SQL\
STMZIP\
TBM\
TCM\
TCP\
TCPS\
TRE\
TREBIN\
TREXML\
TSM\
TTA\
TXM\
TXT\
UDP\
WEB\
WEBC\
XML\
HTTP\
SFI\
OSSL\
SIG\
LEG\
BID\
COL\
PC\
INI\
DBG\
PC\
Objects\
Modules\
Python\
Parser\
libgit2/src/libgit2 \
libgit2/deps/xdiff \
libgit2/deps/llhttp \
libpcre2\
libgit2/src/libgit2/transports \
libgit2/src/libgit2/streams \
libgit2/src/util \
libgit2/src/util/allocators \
libgit2/src/util/hash \
libgit2/src/util/hash/openssl \
libgit2/src/util/regexp \
libgit2/src/util/unix \
curllib\
curllib/vtls\
curllib/vssh\
curllib/vquic\
curllib/vauth\
sqlite\
bzip\
clearsilver\
expat\
jsonc\
zlib\
libpcre\
libssh2


IW_EXTRA_SOURCES := \
	../CHM_LIB3/CHMtableDll.cpp \
	../CHM_LIB3/CHMimpDll.cpp \
	../CHM_LIB3/CHMtableGrammarDll.cpp \
	../CHM_LIB3/CHMtableDefinitionDll.cpp \
	../CHM_LIB3/CHMerrorDll.cpp \
	../CHM_LIB3/CHMmessageDll.cpp \
	../CHM_LIB3/CHMdllDll.cpp \
	../CHM_LIB3/CHMeventDll.cpp \
	../CHM_LIB3/CHMengineDll.cpp \
	../CHM_LIB3/CHMdateTimeDll.cpp \
	../CHM_LIB3/CHMcharacterSetDLL.cpp \
	../CHM_LIB3/CHMconfigDll.cpp \
	../NETDLL2/CHMchameleonEncodingDll.cpp \
	../NETDLL2/CHMlicenseDll.cpp \
	../NETDLL2/CHMutilsDll.cpp

IW_EXCLUDE_SOURCES := \
	../CHM/CHMllpServer.cpp \
	../CHM/CHMllpConnection.cpp \
	../CHM/CHMllpClient.cpp

include ../make_new/makefile.common
```

This was the old one.

```
###############################################################################
# This makefile includes a couple of extra environmental settings:
#    IFW_WANT_PACKAGE=1
#       Builds additional support libraries and binaries to generate a
#       package (iguana.tar.gz) using makefiles/utils/gen-iguana-package.sh
#       Set to anything other than 1 to skip it
#    IFW_WANT_DICOM=1
#       Builds ../ext_DICOM and copies dicom_raw.so/dll into ../DBD
#       Set to anything other than 1 to skip it
#       If skipped, the Iguana package will not contain it
###############################################################################

BINARY=../DBD/iguana

SRC=\
main.cpp\
IguanaPythonConfig.c\

WIN_SRC=\
IguanaResource.rc\

DEPS+=\
client_exe\
hl7simulator\
ifware_service\
iguana_log_verify\
fossil\
git_src\
IGCDLL\
JSZ\
vmd_tool\
libiconv

POSIX_DEPS+=\
$(IFW_OPENSSL_MODULE) \
cyrus-sasl

MODULES=\
DBD\
DDB\
TIC\
DBL\
DSE\
DWB\
DBD\
NOW\
ANN\
NWB\
NODL\
LUA\
$(IFW_LUA_MODULE)\
TIME\
luax\
CHL\
ANT\
ARF\
JLG\
ARFX\
ATT\
CARC\
CHF\
CHJ\
CHP\
CHX\
LAG\
CMD\
CS\
CSV\
CTT\
CHT\
CURL\
DAP\
DBSQL\
DB\
DBDID\
GUID\
DRS\
DBDRPC\
DBQ\
DBE\
DBT\
DBU\
DHT\
DIS\
DLL\
DQU\
DRG\
DTR\
EML\
EVN\
FIL\
FILB\
FMT\
HFIL\
HTPC\
IFWSVC\
IP\
GZIP\
JBB\
JSON\
LAN\
LLP\
MLG\
MPH\
MAP\
MT\
MZIP\
NTV\
NLOG\
NOB\
NODB\
NODC\
MPRC\
JSC\
NOH\
NOPH\
NOTG\
NOX\
DOM\
NTAB\
NOD\
NTBS\
NTB\
SCM\
DBC\
PER\
PIP\
POD\
PRT\
REG\
IPG\
IPA\
REX\
RGN\
SCC\
SDM\
SGC\
SGM\
SGP\
SGPY\
SGX\
SMTPB\
SMTP\
SQL\
STMZIP\
TBM\
TCM\
TCP\
TCPS\
TRE\
TREBIN\
TREXML\
TSM\
TTA\
TXM\
TXT\
UDP\
WEB\
WEBC\
XML\
HTTP\
SFI\
OSSL\
SIG\
LEG\
BID\
COL\
PC\
bzip\
clearsilver\
curllib\
expat\
jsonc\
sqlite\
zlib\
libpcre\
libgit2\
libpcre2\
libssh2\
html_tools\
openldap

WIN_MODULES=\
DBG\
INI\

include ../makefiles/binary.makefile

# This is not a build dependency.
# Needed for Visual Studio Intellisense of header file definitions.
VSDEPS += DBDVER

CPPEXTRA += $(IFW_PYTHON_INCLUDE)

ifeq ($(IFW_POSIX), 1)
# SASL needs to link before OpenSSL
LDEXTRA = $(IFW_SASL_LIB)
endif

LDEXTRA += $(IFW_OPENSSL_LIB) $(IFW_CURL_LIB)

POSIX_LDEXTRA += $(IFW_DL_LINK) $(IFW_PTHREAD_LINK) $(IFW_RT_LINK) \
                 $(IFW_LINK_RPATH)

# Use the Lua library symbols as exported symbols in the binary
# This allows Lua extension modules to load and use library code directly
# from the binary, instead of having to include the code in each extension
EXPORTSLIST = $(IFW_LUA_EXPORTS_LIST)
IFW_MAKE_USE_EXPORTS_LIST = 1
STRIPFLAGS = $(IFW_LUA_STRIP_FLAGS)

# Deprecated: IFW_WANT_IGUANA_TAR_GZ, IFW_WANT_IGUANA_PACKAGE
ifeq ($(IFW_WANT_PACKAGE),)
   ifneq ($(IFW_WANT_IGUANA_TAR_GZ),)
      $(warning 'IFW_WANT_IGUANA_TAR_GZ' is deprecated, \
         use 'IFW_WANT_PACKAGE' instead)
      IFW_WANT_PACKAGE = $(IFW_WANT_IGUANA_TAR_GZ)
   endif
   ifneq ($(IFW_WANT_IGUANA_PACKAGE),)
      $(warning 'IFW_WANT_IGUANA_PACKAGE' is deprecated, \
         use 'IFW_WANT_PACKAGE' instead)
      IFW_WANT_PACKAGE = $(IFW_WANT_IGUANA_PACKAGE)
   endif
endif

# By default, build iguana.tar.gz and IGCDLL on posix, but not on Windows
# Either way, setting IFW_WANT_PACKAGE=1 will always build it, and
# setting IFW_WANT_PACKAGE= anything else will never build it
ifeq ($(IFW_POSIX), 1)
   IFW_WANT_PACKAGE ?= 1
else
   IFW_WANT_PACKAGE ?=
endif
# Similarly, allow skipping DICOM since it takes a while to build
IFW_WANT_DICOM ?= 1

###############################################################################
# Definitions for building the Iguana package (and its support files)
IFW_IGUANA_PACKAGE_NAME = iguana.tar.gz

IGC_SHLIB = ../IGCDLL/$(call MAKESHLIBRARYNAME, IGC)
ICONV_SHLIB = ../libiconv/$(call MAKESHLIBRARYNAME, libiconv)
JSZ_DIST_FILES = $(IFW_JS_DIST_FILES)

# DICOM is a bit weird - its extension for posix is always .so, never .dylib
DICOM_SHLIB =
ifeq ($(IFW_WIN), 1)
   DICOM_SHLIB = ../ext_DICOM/dicom_raw.dll
else
   DICOM_SHLIB = ../ext_DICOM/dicom_raw.so 
endif

# Define the rule for building DICOM and IGCDLL, if need be:
ifneq ($(DICOM_SHLIB),)
$(DICOM_SHLIB): | ext_DICOM
ext_DICOM:
	$(call MAKEMODULE, ext_DICOM)
clean-ext_DICOM:
	$(call MAKEMODULE, ext_DICOM, clean)
else
clean-ext_DICOM: ;
endif

ifneq ($(IGC_SHLIB),)
$(IGC_SHLIB): | IGCDLL
endif

ifneq ($(IFW_DBGHELP_DLL),)
DBGHELP_SHLIB = $(IFW_DBGHELP_DLL)
endif

.PHONY: ext_DICOM clean-ext_DICOM

# These support files are different than the DBD support files - the
# gen-iguana-package utility script looks for these files at the directories they
# are built in, rather than in DBD
IFW_IGUANA_PACKAGE_SUPPORT_FILES = \
../ifware_service/ifware_service$(EXE) \
../fossil/fossil$(EXE) \
../vmd_tool/vmd_tool$(EXE) \
../client_exe/client_exe$(EXE) \
../hl7simulator/hl7simulator$(EXE) \
$(GIT_UTILITIES_DEST) \
../DBD/ca-bundle/ca-bundle.crt \
$(IGC_SHLIB) \
$(ICONV_SHLIB) \
$(JSZ_DIST_FILES) \

ifeq ($(IFW_WANT_DICOM), 1)
   IFW_IGUANA_PACKAGE_SUPPORT_FILES += $(DICOM_SHLIB)
endif

###############################################################################
# Definitions for support files (binaries, libraries, etc.)

SUPPORT_FILES_DEST = \
../DBD/fossil$(EXE) \
../DBD/iguana_service$(EXE) \
$(GIT_UTILITIES_DEST)

ifneq ($(IGC_SHLIB),)
IGC_SHLIB_DEST = ../DBD/$(notdir $(IGC_SHLIB))
endif
ifneq ($(ICONV_SHLIB),)
ICONV_SHLIB_DEST = ../DBD/$(notdir $(ICONV_SHLIB))
endif
ifneq ($(DICOM_SHLIB),)
DICOM_SHLIB_DEST = ../DBD/$(notdir $(DICOM_SHLIB))
endif
ifneq ($(DBGHELP_SHLIB),)
DBGHELP_SHLIB_DEST = ../DBD/$(notdir $(DBGHELP_SHLIB))
endif

SUPPORT_FILES_DEST += $(ICONV_SHLIB_DEST) $(IGC_SHLIB_DEST) \
                      $(DBGHELP_SHLIB_DEST)
# GIT_FILES_RELATIVE is defined in utils.makefile
GIT_UTILITIES_DEST = $(foreach gitfile, $(GIT_FILES_RELATIVE), \
                       ../DBD/git-utilities/$(strip $(gitfile)))

# Pre-requisite rule for getting git-utilities for iguana.tar.gz
$(GIT_UTILITIES_DEST): | copy-git-utilities

copy-support-files: copy-extra-support copy-iconv copy-igcdll \
                    copy-dbghelp copy-git-utilities copy-fossil-exe
copy-extra-support: ../DBD/iguana_service$(EXE)
clean-support-files: clean-extra-support clean-iconv clean-igcdll \
                     clean-dbghelp clean-git-utilities clean-fossil-exe
clean-extra-support:
	$(call RM, ../DBD/iguana_service$(EXE) $(DICOM_SHLIB_DEST), support files)

copy-iconv copy-igcdll copy-dbghelp: DEST = ../DBD
copy-git-utilities copy-fossil-exe: DEST = ../DBD
clean-iconv clean-igcdll clean-dbghelp: DEST = ../DBD
clean-git-utilities clean-fossil-exe: DEST = ../DBD

# Extra support targets:
../DBD/iguana_service$(EXE): ../ifware_service/ifware_service$(EXE)
	$(call CP, $^, $@, iguana_service$(EXE))
../ifware_service/ifware_service$(EXE): | ifware_service
../vmd_tool/vmd_tool$(EXE): | vmd_tool
../client_exe/client_exe$(EXE): | client_exe
../hl7simulator/hl7simulator$(EXE): | hl7simulator
../fossil/fossil$(EXE): | fossil

ifneq ($(DICOM_SHLIB_DEST),)
$(DICOM_SHLIB_DEST): $(DICOM_SHLIB)
	$(call CP, $^, $@, $(notdir $@))
	@chmod 755 $@
endif

ifeq ($(IFW_WANT_DICOM), 1)
# Add dicom_raw to the support list and copy over to DBD
SUPPORT_FILES_DEST += $(DICOM_SHLIB_DEST)
copy-extra-support: $(DICOM_SHLIB_DEST)
clean: clean-ext_DICOM
endif

$(BINARY): | copy-support-files
clean cleanme: clean-support-files

.PHONY: copy-support-files clean-support-files
.PHONY: copy-extra-support clean-extra-support

###############################################################################
# Info

# Speed up command calculation by flagging support libraries as old
info: ASSUMEOLD += $(foreach support, $(SUPPORT_FILES_DEST), -o $(support))
info: info-support
info-support:
	$(call PRINTCMD, SUPPORT:, $(SUPPORT_FILES_DEST))

###############################################################################
# Rules to actually carry out making iguana.tar.gz

ifeq ($(IFW_WANT_PACKAGE), 1)
all: package
clean cleanme: clean-package
clean: clean-JSZ-dist
endif

package: $(IFW_IGUANA_PACKAGE_NAME)

$(IFW_IGUANA_PACKAGE_NAME): $(BINARY) $(IFW_IGUANA_PACKAGE_SUPPORT_FILES)
	$(call RM, $(PKGLOG), $(PKGLOG))
	sh ../makefiles/utils/gen-iguana-package.sh -v > log.package.txt 2>&1

clean-package: clean-qa
	$(call RM, $(IFW_IGUANA_PACKAGE_NAME) $(PKGLOG), \
	           $(IFW_IGUANA_PACKAGE_NAME))

.PHONY: package clean-package

###############################################################################
# Extensions
$(BINARY) $(IFW_IGUANA_PACKAGE_NAME): | extensions

extensions:
	$(call MAKEMODULE, DBD/extensions)

clean: clean-extensions
clean-extensions:
	$(call MAKEMODULE, DBD/extensions, clean)

.PHONY: extensions clean-extensions

###############################################################################
# Send/upload configuration
# NOTE : qa_iguana.tar.gz & iguana_unstripped.gz come from gen-iguana-package

QA_IGUANA_PACKAGE_NAME = qa_iguana.tar.gz
IGUANA_UNSTRIPPED_NAME = iguana_unstripped.gz
SEND_NAME = iguana
SEND_ITEMS = \
$(IFW_IGUANA_PACKAGE_NAME) \
$(QA_IGUANA_PACKAGE_NAME)

$(QA_IGUANA_PACKAGE_NAME): | $(IFW_IGUANA_PACKAGE_NAME)

include ../makefiles/send.makefile

clean cleanme: clean-qa
clean-qa:
	$(call RM, $(QA_IGUANA_PACKAGE_NAME) $(IGUANA_UNSTRIPPED_NAME), \
	           $(QA_IGUANA_PACKAGE_NAME) $(IGUANA_UNSTRIPPED_NAME))

.PHONY: clean-qa
```

The old one is the tip of a massive iceberg of complex dependencies with many many make
files - one is every directory of code.  It has a very different architecture.
