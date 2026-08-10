# Python

**Python’s Original Compromise**

My first product, Chameleon, was written in Python. I quickly regretted that choice.

Python was designed to be far more approachable than shell scripting, particularly for system administration. But to make it genuinely useful, it needed access to a large ecosystem of existing C libraries.

That created a serious problem: much of the underlying C code—and parts of Python’s own runtime—were not designed for safe concurrent access from multiple threads.

The solution was the Global Interpreter Lock, or GIL. Only one thread can execute Python bytecode within a process at a time.

It was a pragmatic engineering compromise. It simplified memory management, protected the interpreter, and made it much easier to integrate existing C code.

But the price was substantial.

In a heavily multithreaded, CPU-bound system, the threads do not execute Python code in parallel. They take turns holding the same global lock. A machine may have dozens of processor cores, but a single Python process cannot use them effectively for ordinary Python computation.

You can work around this with multiple processes, native extensions, or separate runtimes—but each workaround adds complexity.

Python escaped the complexity of shell scripting by absorbing a different kind of complexity into its runtime. The GIL made the language practical, but it also placed a fundamental constraint on the architecture of systems built with it.

