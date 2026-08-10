# Flow

One of the most important design goals of Flow is keeping technical debt under control.

Traditional frameworks encourage messy, spaghetti-style coding, where it becomes very hard to see what depends on what.

Flow requires unique names for each function and enforces functional programming practices.

The framework makes it possible to see, at a very granular level, exactly what code your application is using. Starting from any entry point, Flow can trace not only the Lua code being executed, but also the underlying C+ implementation (note that I deliberately say C+—not C++). Nothing should be hidden.

This visibility changes how you maintain software. Unused code becomes obvious. Code that's only referenced in one place stands out immediately. Instead of accumulating technical debt, you can confidently delete what no longer provides value.

Flow is deliberately structured to support change. Every function lives in its own file with a consistent naming convention and clear prefixes. If you discover that a name is poor, it's easy to rename. If an abstraction turns out to be unnecessary, it's easy to remove. If a feature is no longer useful, you should be able to delete it without fear.

Every function is treated as a small black box with well-defined inputs and outputs. That makes testing straightforward, dependencies easy to understand, and the impact of removing code much more predictable.

Good software isn't measured by how much code it contains; it's measured by how much unnecessary code can be safely removed. A system that is easy to simplify is a system that stays healthy for decades.

It's also about security and minimizing the attack surface of interfaces.

Your interfaces are like cockroaches: hard to kill. And in a wartime situation or other public emergency, that actually becomes important. The Flow architecture encourages resiliency.

