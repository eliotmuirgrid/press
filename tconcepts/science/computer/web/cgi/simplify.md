# Simplify

**How do we simplify the process of patching and supporting Iguana X and Iguana?**

One potential simple plan is as follows:

 - The slowest part of the process is obtaining certificates to sign the binaries. [So do that first.](/tconcepts/science/computer/security/key)
 - Then start with Iguana X, since it's the easiest one to build.
 - Give it a new, clean public/private key-based system for signing, with call-home capability. Customers can get longer licenses if they want—they just need to pay in advance.
 - Next, create a simple license code generator binary that supports both classic Iguana 6 and Iguana X.
 - Use a simple process for Iguana X development. Focus on (removing half-thought-out ideas, like security, from the product. We can revisit those ideas with Flow)[/system/remove].
 - Rebuild Iguana 6 using the same approach.
 - Remove features from Iguana 6 that make it insecure.
 - Implement the new features accordingly.

Then, implement a new queuing system in Flow and switch both products to use it.

