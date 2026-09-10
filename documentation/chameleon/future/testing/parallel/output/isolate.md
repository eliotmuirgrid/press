# Isolate

**How would one take a traditional Chameleon application implemented using `CHM_LIB3.dll` and rebuild to isolated it say as a single binary?**

This is an important question when developing a safe maintenance strategy for patching a large body of existing HL7 interfaces.

The best approach would be to **statically link the application logic with the Chameleon library**, producing a single executable rather than an executable that depends on `CHM_LIB3.dll`.

This is technically quite feasible since this is how Iguana 6 was done. The Chameleon source code uses a prefixing convention for functions and classes, giving its symbols distinctive names. That should make it easier to link the Chameleon code and the application code together into a single binary without symbol collisions.

However, the practicality of doing this depends heavily on the structure and condition of the customer's application source code. It really needs to be evaluated against the actual application and the Chameleon source.  Some challenges could emerge from say the Python C code which has different naming conventions which might result in a name clash.

If static linking proves difficult because of the way a particular application was written, there is a simpler fallback: **build a uniquely named version of the Chameleon DLL and package it in the same isolated directory as that particular HL7 application.**

The important principle is the same in either case: **the patched implementation must be completely isolated from the existing production implementation.** Installing or testing the new version should not alter shared DLLs, PATH settings, configuration, or anything else that could change the behaviour of the existing system.

So there are essentially two approaches:

1. **Preferred:** statically link Chameleon and the application into a single self-contained executable.
2. **Fallback:** use a uniquely named Chameleon DLL packaged alongside the application in its own isolated deployment directory.

Which approach is appropriate can only really be determined by looking at the customer's application source code together with the Chameleon source code.

**Slowly, slowly is the key here.** Given the risk of disrupting interfaces that have been running reliably for many years, each change should be isolated, measurable and independently testable before it goes anywhere near production.

