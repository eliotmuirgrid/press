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

