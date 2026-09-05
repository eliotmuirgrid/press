# Continuity

The model described in the previous documents creates an obvious question:

**How can a healthcare organization safely depend on critical technology produced by a very small team?**

Our answer is to reduce what must be trusted — technically and organizationally — and make the remainder independently verifiable.

## Security through simplicity

Modern software often depends on enormous stacks of frameworks, libraries and services.

Open source does not by itself solve this problem. Source code may be available while the complete system remains far too complicated for anyone to realistically understand or verify.

Our approach is the opposite.

**Make the trusted foundation as small as possible.**

We use standard C++ for the foundation and Lua for high-level interface logic. Lua is deliberately small, mature and understandable. Dependencies are kept to a minimum.

The objective is not to claim that any particular programming language is inherently secure.

It is to **reduce the amount of machinery that must be trusted.**

Less code. Fewer dependencies. Fewer moving parts. Smaller attack surface.

## Prove rather than trust

Simplicity makes a second principle possible: verification.

Builds should be reproducible. Source should correspond demonstrably to the software being deployed. Automated tests should continuously verify behavior.

For migrated interfaces, the regression system provides another layer of evidence: the replacement is continuously compared against the behavior of the system it replaces.

Security therefore becomes a continuous engineering process rather than a periodic compliance exercise.

**Make it smaller. Make it observable. Continuously prove that it works.**

## Business continuity requires the same thinking

A small organization creates another legitimate concern: dependence on key individuals.

We should address that directly rather than pretending it doesn't exist.

The solution is similar to the technical one.

Critical knowledge must increasingly reside in the architecture, source code, tests, build system and documentation rather than existing only in one person's head.

A capable third party must be able to reproduce the software, understand its important components and continue maintaining it if that ever becomes necessary.

This requires more than traditional source-code escrow.

A pile of source code is of limited value if nobody can reliably build, test or understand it.

**Continuity must itself be continuously tested.**

## Protecting both sides

There is an important balance.

Eliot's intellectual property has significant value and must be protected.

At the same time, customers operating critical healthcare infrastructure need confidence that they will never become dependent on something they cannot operate without its creator.

These interests do not have to conflict.

Customers don't necessarily need unrestricted ownership of intellectual property.

They need a credible and independently verifiable path to continuity if the organization or its key people can no longer support them.

That means establishing mechanisms around source access, reproducible builds, automated testing, documentation and clearly defined continuity rights.

## A model for the AI era

AI makes it possible for extraordinarily small teams to create and maintain systems that once required much larger organizations.

That is a powerful economic change.

But customers should not be asked to exchange the organizational risk of a large company for dependence on a single individual.

The technology and the commercial structure must evolve together.

Our goal is therefore straightforward:

**Minimize the technology that must be trusted.**

**Continuously verify the technology that remains.**

**Ensure that no individual is indispensable to its long-term operation.**

That is how a small, highly capable organization can responsibly provide critical infrastructure in the AI era.

