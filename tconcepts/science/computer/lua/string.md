# Porting String Metatable Support into Lua 5.0

In every language, there are ways of expressing ourselves more clearly, so it’s sometimes worthwhile to make the effort to bring a feature from a more modern language into an older one.

It's worth using Lua 5.0 for its small footprint and simplicity, but this was one feature I couldn't do without: the ability to express string operations as methods.

Lua 5.0 does *not* natively support methods on string values (e.g., `AString:upper()` does not work; you have to use `string.upper(AString)`).

I had to work quite hard to patch the Lua 5.0 engine to provide the same capability as Lua 5.1.

This was non-trivial, but it was worth it.

Software is a game of inches—steadily solving one [bottleneck]{/system/toc) after another until things flow.

This was the [patch](https://github.com/eliotmuirgrid/flowlua/commit/dc0b3e71eaa19722471f889dce8e61e6f899b39f).
