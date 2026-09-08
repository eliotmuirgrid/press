# Fast

**Fast build/compile cycles are so important.**

Quick compile times aren't just about raw speed—they directly influence your productivity and reduce frustration as a developer. When you can build and test changes quickly, it maintains your focus and allows for a much more fluid, iterative workflow. That’s why it’s crucial for a project to make incremental builds simple and obvious, letting you avoid unnecessary full rebuilds and work in small steps.

In the Makefile snippet below, you can see the approach taken in the `iguana_complete` build process. The `clean` and `allclean` targets are carefully separated: `clean` lets you do a light cleanup, while `allclean` does a deep clean, wiping out all executables and additional build artifacts. This separation gives you the control you need over how much of the build gets reset—so you can choose between fast, incremental compiles or a fresh start, depending on the situation.

```
clean:
        echo "For a complete rebuild use make allclean"
        rm -f $(EXE_PATHS) 

allclean:
        $(foreach exe,$(EXECUTABLES),$(MAKE) -C ../$(exe) clean;)
        rm -f $(EXE_PATHS) 
        rm -rf app/git-utilities
```

This setup supports good engineering practices by keeping the main Makefile straightforward and easy to follow. Each build step—or clean step—is explicit and transparent, making the flow of the build process easy to reason about. When everything is clear and logical like this, it’s much easier to stay calm, focused, and confident as you work, which is vital for producing high-quality software.

Below you’ll find the full source for this Makefile, which illustrates how all the various components of the Iguana 6 system are brought together into a cohesive package. The structure demonstrates the balance between maintainability and flexibility, enabling both rapid, incremental development and complete, ground-up rebuilds as needed.

**Full Makefile:**
```makefile
.DEFAULT_GOAL := all

include ../make_new/makefile.platform

EXECUTABLES:=\
iguana \
fossil \
iguana_service \
iguana_log_verify

ifeq ($(PLATFORM), mac)
   EXECUTABLES += iguana_controller
endif

EXE_PATHS := $(addprefix app/,$(EXECUTABLES))

ifeq ($(PLATFORM),windows)
EXE_PATHS := $(addsuffix .exe,$(EXECUTABLES)))
endif

.PHONY: print

print:
	@echo "EXECUTABLES = $(EXECUTABLES)"
	@echo "EXE_PATHS   = $(EXE_PATHS)"

# POSIX exe build rule
app/%:
	$(MAKE) -C ../$*
	cp ../$*/$* $@

# WINDOWS exe build rule
app/%.exe:
	$(MAKE) -C ../$*
	cp ../$*/$* $@

clean:
	echo "For a complete rebuild use make allclean"
	rm -f $(EXE_PATHS) 

allclean:
	$(foreach exe,$(EXECUTABLES),$(MAKE) -C ../$(exe) clean;)
	rm -f $(EXE_PATHS) 
	rm -rf app/git-utilities

GIT_UTILITIES = \
	git \
	git-fast-import \
	git-fetch \
	git-gc \
	git-pack-objects \
	git-pack-refs \
	git-rev-list \
	git-upload-pack

app/git-utilities:
	mkdir -p app/git-utilities
	for f in $(GIT_UTILITIES); do cp ../git_src/$$f app/git-utilities/; done

.PHONY: all 

all: $(EXE_PATHS) app/git-utilities
```
