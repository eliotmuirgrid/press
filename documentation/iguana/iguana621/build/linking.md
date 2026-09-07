# Linking

**iguana_log_verify linking mystery.**

At first, **iguana_log_verify** confused me. It was using some methods from the `DBDservice` object in Iguana 6.

I sometimes called this the “application object,” but really it was a “kitchen sink object” — everything just kept getting added to it over time.

In Iguana X, I managed to get rid of this pattern. Instead of a big object full of methods and state, I switched to using a large struct. This struct holds all the state the app needs, but no code (no ‘methods’).

Methods (functions attached to objects) make code harder to understand because it’s not obvious what the inputs and outputs are. By just using plain functions and passing data around explicitly, everything is easier to follow.

### Why did the old system build, but the new one failed at first?

The old system built static libraries for each directory and then linked them together. This made the build slower, but it also tended to **hide linker errors**. So, problems could be missed or masked.

I’m actually grateful these linker errors finally started showing up—and quietly, without creating bigger issues! For example, the [job system](job.md) had a weird error that was finally exposed because of this.

Here’s what the relevant part of the build system looks like:

```makefile
TARGET=iguana_log_verify

IW_OPENSSL := 1

DIRS=\
DBQ\
DBE\
OSSL\
DQU\
SQL\
sqlite\
MT\
SIG\
REX\
libpcre\
DBDID\
TXM\
SFI\
TSM\
FIL\
CMD\
expat\
COL\

IW_EXTRA_SOURCES := 

# This file gets excluded; it really belongs somewhere else since it contains DBDservice
IW_EXCLUDE_SOURCES := ../DBQ/DBQqueueBuild.cpp

include ../make_new/makefile.common
```

