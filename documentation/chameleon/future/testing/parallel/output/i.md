# Output

**The second concern is observing and measuring what each implementation actually does with the same input.**

At the simplest level, we need to know:

* Was the message consumed successfully?
* Was an output produced?
* If so, what was the output?
* How was the incoming HL7 data mapped into that output?
* Did the production and parallel implementations produce equivalent results?

With Chameleon applications, this will depend considerably on how the application was originally implemented.

Chameleon provided a reasonably well-encapsulated **table grammar** as the target data model. Where applications stayed within that model, tracing and comparing behaviour should be relatively straightforward.  This would the desired outcome:

```
HL7 Input
    │
    ▼
Implementation
    │
    ▼
Table Grammar
(structured output model)
    │
    ▼
Observable Output
(destination unknown)
```

**If so wonderful - we have a more managable problem.**

However, some implementations may have bypassed that abstraction and written directly to SQL databases, invoked stored procedures, generated files, made API calls then we have this problem:

```
HL7 Input
    │
    ▼
Implementation
    │
    ├──► Table Grammar
    ├──► Stored Procedures
    └──► Files / Messages / Other Side Effects
```

In those cases, the real "output" of the interface may not be another message. It may be a database change or some other external side effect.

That makes tracing more complicated because we need to identify and measure the **actual observable behaviour** of the interface.

This is why output tracing is such an important part of modernization.

If the same input can be fed independently to the existing and replacement implementations, and their observable outputs can be rigorously compared, then compatibility becomes something that can be **measured rather than assumed**.

[So how do you go about determining on mass what is true for say 500-1000 interfaces?](detection.md).

