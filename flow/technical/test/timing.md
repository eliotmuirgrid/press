# Timing

Timing attacks exemplify why **simplification makes better testing possible**.

A **timing attack** is a type of side-channel attack where an attacker attempts to compromise a system by carefully measuring how long it takes to perform certain operations. The key insight is that some algorithms—even ones that look secure—can inadvertently reveal secrets through subtle differences in their execution time. For instance, code that compares two passwords might return faster if the first character matches, but the second does not. Attackers can exploit these minute timing differences, collecting thousands or millions of measurements, to infer which parts of a secret (like a password or cryptographic key) are correct—even if they never see the secret directly.

Testing an entire authentication system for this vulnerability is challenging. Numerous unrelated factors—networking delays, logging, memory allocations, or context switches—can introduce "noise" that masks the timing differences or makes them variable and unpredictable.

However, if the sensitive operation is isolated into a tiny function such as:

`SECUREequal(Expected, Actual)`

it becomes feasible to repeatedly call the function with controlled inputs and perform statistical analysis to determine whether the execution time leaks information—for example, if it is faster when the inputs match up to a certain position.

This illustrates the broader testing strategy:

**Break software into small enough pieces that obscure properties become practical to test.**

Timing resistance is just one example of this approach. The principle also applies to other hard-to-test properties like memory behavior, edge cases, and malformed inputs—properties that developers (myself historically included) often neglect to test simply because doing so within a large, complex system is overwhelming.

**Simplification doesn't just make code easier to test. It makes previously impractical tests possible.**

## More about timing attacks.

Timing attack exploits the fact that many computer algorithms and systems handle secret data in ways that unintentionally leak information through the time they take to complete certain operations. Even if no information is explicitly revealed, attackers with the ability to measure how long each computation takes can analyze subtle differences—such as how quickly a comparison loop exits on the first mismatching byte, or how encryption functions respond to slightly different keys. By gathering a large number of measurements and applying statistical methods, a determined attacker can gradually deduce bits of the underlying secret, such as passwords, cryptographic keys, or authentication tokens. This makes timing attacks particularly dangerous because they target the implementation, not just the apparent logic or structure of a security-sensitive function.

To defend against timing attacks, developers must design algorithms and write code so that execution time is independent of any secret data. For instance, "constant time" comparison functions ensure that they always process every byte of the input, regardless of early mismatches. However, achieving true constant-time behavior is notoriously challenging—seemingly innocuous implementation details, or even compiler optimizations, can reintroduce leaks. This challenge highlights the importance of rigorous, focused testing on these isolated components. By reducing the scope of what needs to be verified to a small, testable function, developers stand a much better chance of identifying and fixing subtle security flaws introduced by timing differences
