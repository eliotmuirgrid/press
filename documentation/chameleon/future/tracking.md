# Changes 

**Changes are much easier to understand.**

The simpler structure also makes changes to the HL7 grammar much easier to track and review.

In the original model, a conceptual change can affect several different kinds of objects and properties. Understanding a diff requires understanding all of those different structures and how they relate to each other.  In practice this is impossible for humans or machines to really understand those changes.

In Iguana X, most changes look like changes to a simple tree.

Adding a field might be:

```json id="j0fl0p"
{"type":"CWE", "desc":"Allergen Type Code"}
```

Making it required is a tiny, obvious change:

```diff id="w81k1a"
- {"type":"CWE", "desc":"Allergen Type Code"}
+ {"type":"CWE", "desc":"Allergen Type Code", "req":true}
```

Making something repeat is equally clear:

```diff id="tvbsb6"
- {"type":"ROL", "desc":"Role"}
+ {"type":"ROL", "desc":"Role", "repeats":true}
```

Adding another child is simply another node:

```diff id="uxys76"
  {"type":"PID", "desc":"Patient Identification", "req":true},
+ {"type":"PD1", "desc":"Patient Additional Demographic"},
  {"type":"PV1", "desc":"Patient Visit", "req":true}
```

There is very little machinery obscuring what changed.

This is particularly valuable when the grammar is kept in Git. A programmer reviewing the history can see not only **that** something changed, but usually understand **what the change means** directly from the diff.

That makes the format easier to maintain, easier to review and much safer to evolve over time.

**A good representation doesn't just make the code simpler. It makes change easier to see and understand.**

