# Tracing

**See [detection](detection.md).**

Tracing is the most reliable way to understand exactly what an interface is truly doing. There are several levels at which this can be accomplished. The logical place to start is at the highest layer, which is the dynamic language of the system.

## At the dynamic language level (Python, Lua, or JavaScript)

The same principles apply to any dynamic language. The general idea is to alter or replace core function calls—such as those that write to files, databases, or other outputs—so that they still function as normal, but their outputs are also carefully logged.

Some people describe this as "monkey patching":

```
original_write = file.write

def traced_write(data):
    log(data)
    return original_write(data)

file.write = traced_write
```

With dynamic languages like Python and Lua, this is straightforward. A variable can store the original function or "object method" (which is essentially a function attached to a body of data).

A new implementation can then be provided, one that either calls the original implementation (if running in production), or simply logs the output.

**Pros:** This is usually the easiest place to instrument. You can wrap file, database, network, or other calls while preserving the original behavior, and you get very rich context about why the code is making the call. It is also comparatively easy to test and remove.

**Cons:** You only see operations that pass through the functions you wrapped. Direct native calls, extension modules, hidden library behavior, or code paths that bypass your wrapper can be missed. Monkey-patching also changes the runtime environment, so poorly designed tracing can itself alter behavior.

All of this is best tested first within a test environment, and then in a production environment where the tracing code is not running on the live system but on a [parallel one](i.md).

## Within C/C++ (or Java, for third-party technologies)

Another approach is to trace not at the scripting level, but by altering the implementation of Chameleon itself to trace these functions. This captures operations at a lower level, in the engine's source code, rather than in the scripting language. This also has its pros and cons.

**Pros:** This catches activity below the scripting layer and can cover many interfaces at once without modifying every individual script. It is often a good compromise between high-level understanding and low-level completeness. If you control the engine source, the instrumentation can also be very deterministic.

**Cons:** It is more invasive and requires rebuilding and validating the engine. You need to be extremely careful that tracing does not introduce timing, memory, threading, or behavioral changes. It may still miss operations performed outside the engine or through third-party native components.

## DLL injection

This involves tricking the engine’s code into loading another DLL, which sandboxes and provides implementations of system-level or database driver calls. This is technically more sophisticated, but it operates at a very low level to capture what a process is truly doing.

This is probably the most difficult tracing technique and the hardest to navigate due to the operating system's security measures.

**Pros:** This can observe behavior much closer to the operating-system boundary, including file access, database-driver calls, networking, and other native operations that higher-level tracing might miss. It is therefore potentially the most comprehensive way of discovering unknown side effects.

**Cons:** It is the most technically difficult and risky approach. Modern operating-system security mechanisms can make injection difficult or block it entirely. It can also interfere with application behavior, complicate debugging, create its own security concerns, and produce a large amount of low-level noise that is harder to interpret
