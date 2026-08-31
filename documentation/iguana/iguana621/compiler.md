# Compiler

As C++ compiler standards have evolved, I’ve had to make some gentle changes to accommodate new requirements. Most of these modifications were necessary in third-party code, rather than in my own.

For example, **Iguana 6** uses an embedded git library. This removes the need for a separate git installation, a convenience I’m considering keeping for **Iguana X** to avoid including git as part of the install process.

However, third-party code often doesn’t follow the conventions I’ve established for my own projects and team. For example, I always use consistent type or module prefixes—such as `COLstring`, `FILexists`—which prevent naming conflicts with system header files.

In contrast, the git library defined a struct named `thread_local`. In modern C++, `thread_local` is a reserved keyword, so this caused compiler issues. To resolve this, I renamed it to something unique, avoiding the conflict.

Moving forward, I’ll have to consider whether to update and harmonize the git library across both Iguana X and the original Iguana. However, changes to critical infrastructure software must be made gradually and respectfully—one careful step at a time.

