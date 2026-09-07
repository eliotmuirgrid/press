# Source

**How do we provide the security that healthcare needs in today's increasingly challenging world?**

The real business problem is continuity.

We have substantial value in deep engineering knowledge of HL7 and an intimate understanding of the history, architecture and practical realities of Chameleon and Iguana. The challenge is how we preserve the value of that expertise without making customers dependent on any one person.

We believe a shared-source model provides a practical answer.

Security requirements are increasing. Attackers are becoming more sophisticated, particularly with the growing use of AI. Our response should not simply be to add more security products and processes. We need to simplify the system, reduce the amount of code and infrastructure that must be trusted, and make the complete software supply chain understandable and defensible.

Having source code is only one part of that.

What really matters is having a reliable, repeatable and deterministic way of translating that source code into the exact software that runs in production, together with strong regression testing that demonstrates compatibility.

That is particularly difficult with HL7.

Almost no healthcare organization has a comprehensive set of production-equivalent test data that can be replayed through every interface to prove that a replacement behaves identically. Patient confidentiality makes retaining and sharing real production data difficult, while every HL7 interface tends to become its own snowflake after years of local assumptions and modifications.

This makes modernization unusually difficult. It is not enough for new software to be theoretically correct. We have to reproduce decades of accumulated production behaviour without breaking interfaces that organizations depend on.

So how do we provide genuine business continuity while still taking advantage of the specialized engineering knowledge required to solve these problems?

The shared-source model is one answer.

Under this model, significant customers participating in the program would have access to the source and, critically, the ability to operate their own independent build infrastructure.

A build server should be disposable. It should begin from a clean operating-system image and install every tool and dependency required to produce the software through an automated and documented process.

In infrastructure terminology, **the build server should be cattle, not a pet**.

If the machine disappears, nothing important should be lost. We should be able to provision another clean machine and reproduce the same build.

That sounds simple, but it is a significant engineering undertaking. Some operating systems—Windows in particular—make fully automated installation and configuration of development tools surprisingly difficult. That gives us another strong reason to simplify the build process and eliminate unnecessary tools and dependencies wherever possible.

This is exactly the kind of foundational engineering work that is worth doing.

The end result is not merely access to source code. It is something much stronger: a reproducible path from source code to production binary, independent verification that the software can still be built, regression testing that demonstrates compatibility, and a structure that allows our customers to continue operating even if circumstances around individual engineers or the company change.

That is a much more meaningful form of business continuity.

