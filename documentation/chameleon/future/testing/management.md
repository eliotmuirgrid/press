# Management

In my experience, neither healthcare software vendors nor hospitals rigorously manage configuration source control and regression testing across all their interfaces.

This challenge is amplified by the sensitivity of patient data. Production data cannot be freely copied for testing, making it extremely difficult to reproduce the exact conditions under which an interface runs.

As a result, healthcare IT is burdened by a kind of **dark matter**: a vast, business-critical mass of interface logic whose behavior isn’t fully understood—even by those responsible for it.

Each interface is unique—a “snowflake” shaped by the quirks of specific systems, workflows, data peculiarities, and historical decisions. Frequently, the people who made those original decisions have long since left.

This situation makes change both expensive and risky. Reimplementing an interface isn’t just about reading the code—you have to rediscover hidden assumptions, reconstruct the knowledge of departed staff, and somehow prove that your replacement works identically in production.

The core issue isn’t just about **source control**. It’s about **proving compatibility with existing production interfaces—without ever letting confidential patient data leave the customer’s environment**.

That’s the real engineering challenge.

It’s also a source of frustration for vendors and technologists—since they rarely get access to the information they need to modernize or improve their products.

This is a problem that must be solved collaboratively. A shared source model is the most straightforward approach to tackle it.

