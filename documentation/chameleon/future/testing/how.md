# How

**How does a vendor that has, say, 1000 interfaces implemented remotely, get all the configurations in a central place?**

The answer is automation. And the key phrase here is "slowly, slowly."

Let’s imagine a customer that has used Chameleon for over a decade. They might literally have thousands of `CHM_LIB3.dll` objects, which is the core library in Chameleon. Unfortunately, those DLLs won’t necessarily be 100% compatible with each other—there could be very minor differences with a meaningful impact on production.

I remember one of our clients had some Python code that relied on undocumented behavior. When we upgraded the embedded Python version, it broke all their code because their interfaces depended on a specific library call. This caused a major outage since everything was upgraded at once.

So, before you make changes to such a system, it’s crucial to archive all configurations and ensure they’re safely and neatly organized, for example, in Git repositories. This enables automated tests to verify any alterations made to the code.

Any changes to production must be carefully tested and compared, with the new system running in parallel for an extended period before having the confidence to switch over.

The good news is that, once you have a framework like this in place, the ability to continuously test and improve security becomes much more achievable.

