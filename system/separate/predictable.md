# Predictability

**Predictability is better than organization.**

Traditional codebases often group definitions into general files such as:

```
COLtypes.h
```

which might contain:

```
COLuint64
COLint64
NULL
```

This approach aims to keep things tidy, but it introduces a common problem: How do we define and find large 64-bit numbers—signed and unsigned? Most codebases put these definitions into common header files.

While this method may look organized, it creates unnecessary cognitive load. A programmer—or an AI—must remember:

```
COLuint64 → COLtypes.h
COLint64  → COLtypes.h
NULL      → COLtypes.h

```

But this knowledge adds no real value.

A more predictable structure would be:

```
COLuint64 → COLuint64.h
COLint64  → COLint64.h
COLnull   → COLnull.h
```

Now there’s nothing extra to remember.  Notice we are using COLnull instead of NULL.

Easier to predict where it is coming from.

> **To find X, look for X.**

Generic files like `types.h`, `utils.h`, and `common.h` create arbitrary categories that both humans and machines have to learn. This not only increases cognitive overhead, but it also complicates automation, since finding something requires knowledge of someone else’s organizational choices.

The same principle applies to identifiers: prefer `COLnull` over generic `NULL`. It’s explicit, searchable, namespaced, and predictably defined in `COLnull.h`.

More files are cheap, but cognitive load is expensive.

**Optimize your codebase for predictability, not just organization.*
# Predicatable

**Predictability is better than organization.**

Traditional codebases group definitions into files such as:

```text
COLtypes.h
```

containing:

```text
COLuint64
COLint64
```

This is common problem. How do we define a large 64 bit number - signed and unsigned?
Most codes bases will put these definitions into a common header file - but then every
programmer working on the system has to remember where it is.

This looks organized, but creates cognitive load. A programmer or AI must remember:

```text
COLuint64 → COLtypes.h
COLint64  → COLtypes.h
```

That knowledge adds no value.

A more predictable structure is:

```text
COLuint64 → COLuint64.h
COLint64  → COLint64.h
COLnull   → COLnull.h
```

Now there is nothing to remember.

> **To find X, look for X.**

Files such as `types.h`, `utils.h`, and `common.h` create arbitrary categories that humans and machines must learn. They make automation harder because finding something requires knowledge of how somebody chose to organize the code.

The same principle favors `COLnull` over `NULL`: it is explicit, searchable, namespaced, and predictably defined in `COLnull.h`.

More files are cheap. Cognitive load is expensive.

**Optimize code for predictability, not organization.**

