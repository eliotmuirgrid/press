# Tracing System

The BAS tracing system provides lightweight, module-based diagnostic logging for C++ code.

Tracing can report:

* Function and method entry and exit
* Source line numbers
* Thread IDs
* Timestamps with microsecond precision
* Nested call indentation
* Variable values
* Hexadecimal buffer contents

Tracing is selected at runtime using simple glob expressions.

## Enabling tracing in a source file

Include the tracing header and initialize the module:

```cpp
#include "BAStrace.h"

BAS_TRACE_INIT;
```

`BAS_TRACE_INIT` creates a module name from the current source filename.

For example:

```text
APPinstall.cpp
```

becomes the tracing module:

```text
APPinstall
```

The module name is displayed in each trace line and is used when applying the trace pattern.

## Selecting modules to trace

Call:

```cpp
BAStrace("APP*");
```

This enables tracing for modules matching the supplied glob expression.

Example command-line use:

```sh
./flowlua.com --trace "APP*"
```

Example output:

```text
### Tracing files matching: APP*
  Timestamp       Thread ID File
  03:02:41.931618     96189 APPinstall         >APPinstall Line:11
  03:02:41.931805     96189 APPinstall         . .
  03:02:41.931812     96189 APPinstall         . ..
  03:02:41.931817     96189 APPinstall         . dir
  03:02:41.931823     96189 APPinstall         . git
  03:02:41.931830     96189 APPinstall         <APPinstall
```

Glob expressions support `*`, multiple space-separated patterns, explicit inclusions using `+`, and exclusions using `-`.

```text
APP*
```

Trace all modules beginning with `APP`.

```text
APP* -APPtest*
```

Trace modules beginning with `APP`, except modules beginning with `APPtest`.

## Trace messages

Use `BAS_TRC` to write a trace message:

```cpp
BAS_TRC("Opening configuration file");
```

Values can be streamed into the message:

```cpp
BAS_TRC("Read " << Count << " records");
```

Output:

```text
03:02:41.931805     96189 APPinstall         Read 12 records
```

## Tracing variables

Use the variable macros to display variable names and values:

```cpp
BAS_VAR(Value);
BAS_VAR2(Name, Value);
BAS_VAR3(X, Y, Z);
BAS_VAR4(X, Y, Z, Result);
```

Example:

```cpp
int Count = 12;
BAS_VAR(Count);
```

Output:

```text
Count = 12
```

The macros use the normal `BASstream` output operators, so the value must be supported by the stream.

## Tracing functions

Place `BAS_FUNCTION` near the beginning of a function:

```cpp
void APPinstall()
{
    BAS_FUNCTION(APPinstall);

    BAS_TRC("Installing files");
}
```

The trace displays entry and exit automatically:

```text
>APPinstall Line:11
. Installing files
<APPinstall
```

The `>` character indicates function entry.

The `<` character indicates function exit.

The source line shown is the line containing `BAS_FUNCTION`.

Function exit is produced by an RAII object, so it is written when the function scope ends, including when the function returns early.

## Tracing methods

Use `BAS_METHOD` inside a class method:

```cpp
void Installer::run()
{
    BAS_METHOD(Installer::run);
}
```

Method traces also include the `this` pointer:

```text
>Installer::run Line:42 this=0x7ff7b240
```

## Nested indentation

Function and method traces maintain a thread-local indentation level.

Example:

```cpp
void outer()
{
    BAS_FUNCTION(outer);
    inner();
}

void inner()
{
    BAS_FUNCTION(inner);
    BAS_TRC("Working");
}
```

Output:

```text
>outer Line:10
. >inner Line:17
. . Working
. <inner
<outer
```

Each nested level is represented by `. `.

Because indentation is thread-local, calls on different threads maintain independent nesting levels.

## Hexadecimal tracing

Use `BAS_HEX` to display a memory buffer:

```cpp
BAS_HEX("Packet", Buffer, Size);
```

The output includes the buffer size followed by a hexadecimal dump:

```text
Packet= (size=128)
...
```

The buffer is formatted using the BAS hexadecimal formatter with a width of 60 characters.

## Output format

Each trace line begins with:

```text
Timestamp  Thread ID  Module  Indentation  Message
```

Example:

```text
03:02:41.931618     96189 APPinstall         >APPinstall Line:11
```

The timestamp uses local time and contains six fractional digits:

```text
HH:MM:SS.microseconds
```

The thread ID is supplied by `BASthreadId()`.

By default, tracing is written through `BASlog` to file descriptor `1`, which is normally standard output.

## Disabling tracing at compile time

Define `BAS_TRACE_OFF` before compiling:

```cpp
#define BAS_TRACE_OFF
#include "BAStrace.h"
```

When disabled, the tracing macros expand to nothing:

```cpp
BAS_TRC(...)
BAS_VAR(...)
BAS_FUNCTION(...)
BAS_METHOD(...)
BAS_HEX(...)
BAS_TRACE_INIT
```

This removes the runtime tracing operations from the compiled code.

## Performance behaviour

Each tracing macro contains a static integer that caches whether its source module is enabled.

The first time a trace location is reached, the module name is checked against the active trace expression. The result is then cached:

* `1` means tracing is enabled.
* `-1` means tracing is disabled.
* `0` means it has not yet been checked.

This avoids repeatedly evaluating the glob expression.

A consequence is that changing the trace pattern after a trace location has already been evaluated will not update that location. Trace patterns should therefore normally be configured before traced code begins running.

## Current implementation notes

Module names are stored in a fixed 20-byte buffer. Long filenames may not be represented safely by the current implementation.

The module initialization also assumes that the source filename ends in a four-character extension such as `.cpp`.

The active trace pattern is copied using `strdup()` and deliberately retained for the life of the process.

`BASsetTraceFile()` is declared in the public interface, but its implementation is currently commented out. Trace output therefore continues to use the default `BASlog` destination.

