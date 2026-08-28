# Security

**A much smaller attack area.**

The simpler Iguana X design has an important security benefit: it dramatically reduces the **attack area**.

Every additional code path and special case is another place where unexpected behaviour and security vulnerabilities can hide.

By using a much smaller and more uniform implementation, there is less security-critical code to understand, test and maintain.

This is particularly important for an HL7 parser because it processes data coming from external systems. The smaller and simpler that boundary is, the easier it is to secure.

Simple software is not automatically secure. But reducing unnecessary complexity eliminates entire classes of potential bugs.

**The safest bug is one that the architecture makes impossible.**

