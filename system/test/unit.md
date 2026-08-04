# Unit 

**Unit testing is where you test the smallest elements of a system.**

I am building unit testing into the foundation of our flow. It needs to be as simple and straightforward as possible.

The most obvious idea is to put each test in a self-contained file, located in a directory under the code file being tested, which in most cases will be a function.

Each unit test should test one thing: one input and one expected output, with preferably minimal boilerplate.

When you phrase the problem as clearly as that, the problem definition becomes obvious.

But the beauty of thinking with this level of rigor is that when you push things to [extremes](/system/extremes) solutions emerge that work smoothly not only with my code but also with customer code.

We simply represent each test case as an assertion with minimal syntax in the language itself:

Imagine in each file we have something like:

```
"C:\\blah" == filepathSimplify("C:\\blah\\..\\blah");
```

Now tests become very easy to write and generate by humans or AI. Most importantly, they are easy to delete when you're done with them.
