## A Crazy Idea, But Cool

What if we stick to **one function per file**, or at minimum, one clear entry point per file?

Now, imagine laying out code for both **Lua** and **C++**, side by side. But instead of using language-specific conventions, we adopt a universal **prefix naming system**—something portable across all languages. This keeps things consistent and makes switching contexts a breeze.

It sounds wild, but that's exactly what makes it *cool*. Most people might not immediately see why this is such a good idea—but trust me, there's real power here.

**The best part?** Tracing just got way simpler. I can now run:

```
./flowlua.com --trace "TEST* COL*"
```

…and effortlessly trace function calls *across both languages*, without having to remember weird, language-specific syntax. Super straightforward—and really efficient.

