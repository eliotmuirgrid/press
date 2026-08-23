# Test

**Testing is a central concept in Flow.**

I had to try Claude to see what all the fuss was about. I was genuinely hopeful that it might help me write Flow faster.

But I found it surprisingly cumbersome and difficult to keep pointed in the right direction.

So I went back to building Flow myself and finished the JSON parser. My next focus is building out the testing framework.

The plan is to cut the core classes in COL like the string class down to the minimum. Rather than having lots of methods attached to classes, most operations will be represented as small global functions.

Then I can test those functions rigorously using a declarative testing strategy.

The basic idea is extremely simple: **a file containing one JSON object per line, with each object representing a single test.**

Each JSON object will have `in` and `out` fields. `in` represents the inputs to the function and `out` represents the expected output.

So effectively:

**one line = one test = input + expected output**

Because most Flow functions will operate on relatively simple types, I think this structure should cover a surprisingly large proportion of the system.

There will obviously be cases that need something more sophisticated, but I’ll deal with those when I encounter them.

This should greatly reduce the amount of boilerplate code required for testing. It also makes the tests themselves extremely easy to read, generate, modify and automate.

More importantly, testing becomes part of the basic architecture rather than something bolted on afterwards.

And the same mechanism shouldn’t just test the core Flow code. Eventually it should make it straightforward to automatically test customer code as I start porting it over to Flow.

I’ll do what I can with this approach and see where its limits are.

But right now, building a very small, very well-tested foundation feels like much higher leverage than having an AI generate large amounts of code for me.

