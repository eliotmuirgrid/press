# Job

One of the more outlandish build problems I ran into was with what we call the job system
in Iguana 6.

There was an include which was including the 'cpp' file instead of the header file.

Instead of 

```
#include <NOW/NOWjobSystem.h>
```

it had 

```
#include <NOW/NOWjobSystem.cpp>
```

It was such a crazy error - a correct build system should never have compiled it but because of
how the old build system used static libraries the linker was lazy and didn't fully bring in all
the symbols from the libraries and so the problem was there lurking waiting to come out.

Now it solved and will stay solved since the new build system doesn't allow this.
