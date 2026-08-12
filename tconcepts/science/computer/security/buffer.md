# Buffer

**Buffer overwrites are a serious concern for both security and debugging, especially in C++ programming.** They’re surprisingly easy to introduce, and finding them can take substantial effort. Today, I focused on integrating critical features into Flow to make these issues easier to detect and fix.

The first capability I added is stack tracing on exceptions, enabling me to quickly locate the source of errors with a single command. Next, I ensured that Flow can work with multiple compilers. This means I’m no longer limited to a single toolchain—on Mac, for instance, I can now use the native Clang compiler, which helps Flow detect buffer overwrites directly.

As much as I appreciate writing cross-platform software with Cosmopolitan, it’s a mistake to lock your project into a single toolchain or a “monoculture.” Compiling with different compilers is invaluable: it highlights various issues and helps fix core bugs. Today, this strategy let me improve code that handles passing paths and resolving the locations of executables.

Over time, I plan to replace all the default process-handling machinery (like Lua integration) with more robust, transparent routines. This will make the entire system both more secure and more understandable.

Tools like AddressSanitizer, as supported by Clang, also make it dramatically easier to spot memory corruption issues and fix them for good.

Today, I tracked down a tricky one-line bug through these enhancements. Software development really is a game of inches, but solving these fundamental problems every day means I’m steadily building a more capable and reliable code base. These improvements compound over time and will let me move faster and more confidently in the future.

`flow make:memory:check`

