# Lua

Lua is an amazing language, but one does need to step back and ask reasonable questions, rather than assume that the team behind it is taking the language in the direction it needs to go.

For Flow, I made a very deliberate choice not to select the most **modern and shiny** version of the language. I didn't automatically gravitate to the most recent version, assuming it was the best one.

Quite often, designers—including myself—make a fatal design mistake: We assume we need to add features, when in fact one of the best things we can do is [reduce and simplify](/system/remove) systems.

I chose Lua 5.0 because it was the simplest version of Lua I could find, with the fewest lines of code. My attitude is simple: Thank you, Lua team. But I will take it from here. You made a huge contribution to humanity, but you don't appear to know what to do next.

I do.

As an outsider to the Lua team, I can look at it objectively and see both the good and the bad.

The good is that Lua is the simplest, fastest, Turing-complete dynamic embedded language, with a tiny footprint and no burden of an ugly, technical-debt-ridden 'ecosystem'—which is often a euphemism for dirty, unmaintainable code.

But it's far from perfect—I see that every day. I am not optimizing Flow for 'professional developers'. I am optimizing Flow for organizations that want to apply the [Theory of Constraints](/system/toc) and obliterate their competition by outperforming them.

For this reason, simple is better. Transparent is better. "Where's Waldo?" is good for kids who have unlimited time—but that isn't me, and it's not true for the kind of customers I want to attract.

Let's have a look at the debug structure for Lua. Forget 'opaque'—I want to understand it.

```c
#define LUA_IDSIZE	60

struct lua_Debug {
  int event;
  const char *name;	/* (n) */
  const char *namewhat;	/* (n) `global', `local', `field', `method' */
  const char *what;	/* (S) `Lua', `C', `main', `tail' */
  const char *source;	/* (S) */
  int currentline;	/* (l) */
  int nups;		/* (u) number of upvalues */
  int linedefined;	/* (S) */
  char short_src[LUA_IDSIZE]; /* (S) */
  /* private part */
  int i_ci;  /* active function */
};
```

This structure is not optimal. There are things that need to be removed. Also, I don't appreciate having more than one way to say something in my codebase. A struct is just a public class, so I will rebuild this and simplify it, removing unsafe features. When we focus on simplicity and understandability, speed comes as a natural side effect.

I chose not to use the LuaJIT for this reason.  I cannot verify that it is secure.  Lua will never be the bottleneck in Flow because Flow doesn't make you believe that everything has to be done in Lua.  When there are critical bottlenecks, the C+ is the choice.  Notice I say C+.  Not C++.  Not C.

Everything I do is highly calculated. 

Every choice is very deliberate.  

This is how you win.
