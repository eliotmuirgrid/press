# Equivalent

Being able to locate and eliminate equivalent functions in Flow is a major goal. Programmers often create duplicate functionality in code bases.

This happens because they are focused on solving a particular problem and end up creating helper functions that already exist elsewhere in the code base.

Declarative tests that do not alter state—using techniques like [journaling](journal.md)—could actually make it possible to automate the process of "if it looks like a duck, sounds like a duck, then it is a duck."

This is a key design goal in Flow, and declarative tests would make it possible. It’s an interesting problem to find candidates. A variety of methods can be used to compare tests; once you have a candidate, it should be possible to run the same tests through each function and confirm whether or not the functions are identical.

These are all powerful techniques that, later on, can be used to analyze customer code and bring it over into Flow.
