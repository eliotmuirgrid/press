# Library

The build system I am replacing because of 
[history would create a separate static library for each directory of code](history.md). 


Static libraries can hide problems in a source tree because of the way the linker uses them. A static library is essentially an archive of object files. When linking an application, the linker generally does not include every object in the archive. It extracts only the objects needed to satisfy symbols required by the program.

This means problems can remain hidden for years. Two objects may define the same symbol without causing an error if only one of them is ever extracted from its library. Likewise, an object can contain unresolved references that don't matter as long as nothing causes that object to be pulled into the final executable. A successful link therefore doesn't necessarily mean that every object in the libraries could successfully coexist in one program.

The new Iguana build approach is different. Rather than organizing the code into layers of static libraries and allowing the linker to selectively extract objects, it compiles the source into object files and links those objects together directly in a single step. That forces the linker to consider the complete set of objects.

As a result, this new build exposed duplicate symbols, unresolved references, and other inconsistencies that the previous build architecture had quietly hidden. Fixing these issues is valuable because it makes the actual dependencies and structure of the code explicit rather than relying on incidental behavior of static-library linking.

This is a quiet, but really big win for the long term sustainable future of Iguana 6 in making the product much much easier to keep current and evolve it safely.

I feel a quiet satisfaction in achieving this.  See [iguana_log_verifier](verify.md) and the [job system](job.md).
