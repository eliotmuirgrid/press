# Test

**Testing is a central concept in Flow.**

Making testing as easy as possible is a key idea in Flow. Rather than requiring tests to be written out with a heavy, cumbersome framework, it’s better to define tests with simple, intuitive functions. This reduces friction and allows developers to focus on the logic and behavior they want to verify.

We start with simple cases and incrementally implement further tools to keep testing both simple and effective.

Let’s start by considering the need for a function such as `FILEpathAbsolute(Path)`.

This function must simplify directories, including expanding "~" characters, to generate an absolute path. Testing it can be challenging, since handling paths and the file system normally requires an assumed or virtual environment.

To address this, we allow the tester to define test cases using a set of sample files located in a controlled directory under `FILE/`. For our tests, we can use the directory `FILE/FILEpathAbsolute/tests/` as a sandbox for input files and directory structures.

By structuring our test environment this way, we can:

- Clearly organize test files and inputs
- Easily define expected outputs for different cases (such as resolving "~", absolute paths, and relative paths)
- Run tests in isolation, without affecting or depending on the actual user environment

### Example

Suppose we want to test how `FILEpathAbsolute` handles different kinds of input. We can express these tests simply:

```
# Pseudocode Example
assert FILEpathAbsolute("~/project") == "/home/testuser/project"
assert FILEpathAbsolute("docs/../images") == "/current/working/directory/images"
assert FILEpathAbsolute("/etc/passwd") == "/etc/passwd"
```

Each test case resides alongside sample directory fixtures in `FILE/FILEpathAbsolute/tests/`, ensuring results are consistent and reproducible.

By following this approach, Flow makes writing and running tests straightforward—even when dealing with tricky cases like file paths.

