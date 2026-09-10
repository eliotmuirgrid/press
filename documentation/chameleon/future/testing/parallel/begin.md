# Phased Plan

**Before modernizing an existing HL7 interface, first establish exactly how you will duplicate its input, isolate a new implementation, and prove that the outputs are equivalent.**

Even patching an interface that has been running unchanged for years can carry significant risk. The interface may be poorly documented, its original developers may no longer be available, and seemingly minor changes can have unexpected consequences.

The purpose of this phased approach is to remove as much of that risk as possible **before changing the production interface**.

The goal is not to begin by rewriting interfaces or introducing new technology. The first goal is to create a safe, repeatable way to make and test changes while leaving the existing implementation untouched.

Once that capability exists, patches, security updates, and eventually replacement technologies can all be tested using the same process.

A practical starting plan is:

## Phase 1 — Understand and get a global picture of the inputs

For each interface, determine:

* Can we assume that every interface is just using the standard LLP protocol - encrypted or unencrypted?
* Do we have a global database of this information?  This is really important.
* Is the ACKnowledgement simply confirming receipt and safe storage?
* Can the same input be safely copied to a second implementation without affecting the sender?

See [Input](input.md).

## Phase 2 — Determine the true outputs

Before comparing implementations, identify what the current interface actually does.

Ask:

* Does it generate another message?
* Does it write to a database?
* Does it invoke stored procedures?
* Does it create or modify files?
* Does it call another service?
* Are there any other side effects?

Do not assume the answer is known.

Use institutional knowledge, static analysis, and ultimately runtime tracing to build confidence.

See [Output](output.md) and [Detection](detection.md).

## Phase 3 — Design the splice

Determine how the same input can be delivered to both implementations.

The splice should be:

* simple
* deterministic
* independent of the interface implementation
* minimally invasive to the production path

The existing production implementation must continue to operate normally.

The parallel implementation should receive the same input without being able to interfere with production.

## Phase 4 — Isolate the parallel implementation

Confirm that the new or patched implementation can run completely independently.

It should have:

* its own directory
* its own configuration
* its own logging
* its own runtime state
* no shared DLL or PATH dependencies that could affect production

Ideally, package the implementation as a single self-contained binary where practical.

## Phase 5 — Decide how outputs will be captured

For every output discovered in Step 2, answer:

* How will this output be observed?
* How will it be logged?
* How will it be associated with the original input message?
* Can it be captured without allowing the parallel implementation to affect downstream production systems?

This needs to be solved before meaningful comparison can begin.

## Phase 6 — Define equivalence

Decide what it means for the old and new implementations to behave the same way.

For example:

* Must the output be byte-for-byte identical?
* Are formatting differences acceptable?
* Are database changes logically equivalent even if SQL differs?
* Does message ordering matter?
* Which differences are significant and which can safely be ignored?

Without a definition of equivalence, comparison produces data but not confidence.

## Phase 7 — Run in parallel

Once the above is understood:

**capture → duplicate → run independently → observe → compare**

The existing implementation remains authoritative.

The new implementation runs in parallel and produces only observable test results until its behaviour has been demonstrated to be equivalent.

## Phase 8 — Promote only when there is business justication

Only after the organization can reliably answer the questions above should a patched or replacement implementation become authoritative.

There is as much risk and danger putting a patched implementation into production as a complete new implemenation.  Also it adviseable to nail down Phases 1 to 7 before introducing more risk into the plan.

The important shift is that modernization is no longer:

**replace it and hope**

It becomes:

**measure → isolate → compare → prove → promote**

