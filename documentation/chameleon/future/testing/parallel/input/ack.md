# ACKnowledge

**The first concern is understanding the ACKknowledge protocol receiving and safely duplicating the HL7 input.**

The important question is: **what does the existing interface actually mean when it ACKs a message?**

In the simplest and probably most common case, the ACK effectively means:

> I received your message and stored it successfully for subsequent processing.

If that is the contract, then the [splice can potentially be very simple](../i.md). It receives the message once, stores it safely, and makes the identical message available to both the existing production implementation and the new parallel implementation.

However, this behaviour needs to be verified.

Some interfaces may perform validation while receiving the message and return an error to the sending system based on its contents.

In practice this is less common, since the sending system often has little ability to do anything meaningful with an application-level error. But it cannot simply be assumed.

**The existing ACK behaviour needs to be understood and preserved.**

The goal is to duplicate the input without changing the behaviour that the sending system sees and without introducing unnecessary machinery into the production path.

