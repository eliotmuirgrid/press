# Build System Modernization

One huge improvement for the next release of Iguana 6 is the modernization of the build system. This is incredibly important for the long-term stability and maintainability of the product.

I had already developed this approach for Iguana X and am very proud of the result. Iguana 6 has very different dependencies, however, so very little of the actual build configuration could be reused. What could be reused was the methodology.

The old system spawned separate make processes for different directories, each with its own manually maintained list of source files. Every time a C or C++ file was added, removed or moved, those lists potentially needed to be updated.

The new system is fundamentally simpler. There is one makefile process. It uses wildcard matching to discover the source files, compiles the objects directly, and then links them all together.

This is somewhat counterintuitive compared with the way large C/C++ projects are typically structured. I arrived at the approach by working from first principles: removing unnecessary complexity and finding the simplest, most symmetrical representation of what the build actually needs to do.

It is also **much faster**.

Because the new approach doesn't continually spawn separate make processes for every directory, the whole product builds much more quickly.

That speed is not merely a developer convenience. **Iguana 6 needs active development.**

There is significant engineering work required to give Iguana 6 a long-term future: modernizing aging components, reducing unnecessary dependencies, improving security, and creating a practical migration path for interfaces that customers have spent years developing and validating.

Doing that safely requires a very tight development loop. I need to be able to make a small change, compile quickly, test it, understand the result and repeat. The faster and more transparent that cycle is, the more carefully I can make substantial changes without sacrificing the stability that customers depend on.

Applying this methodology also exposed a number of long-standing inconsistencies in the source tree that had been hidden by the old manually maintained build configuration. I had to investigate and resolve each problem in turn. That was a lot of work, but it was exactly the work required to properly understand the system.

The makefile itself can still look somewhat overwhelming because Iguana 6 has a number of third-party libraries, each with its own architecture and special build requirements. That complexity is real.

The important difference is that **the complexity is now visible**.

There is one place of truth where you can see the components going into Iguana, the external dependencies, the platform-specific requirements, and how everything ultimately comes together to produce the binary.

A fast development build is now working on macOS, and the core Iguana binary successfully links.

This work is ultimately about protecting the enormous investment that thousands of integration engineers and their organizations have made in Iguana over decades. They have built and validated interfaces that run critical healthcare workflows every day. The way forward cannot simply be to discard that investment and start again.

Critical infrastructure software doesn't become reliable by accident. There is a reason Iguana 6 has been so stable. It comes from meticulous work at this level: understanding the machinery, questioning unnecessary complexity, and simplifying it from the foundations upward.

**This is important work.**

Eliot Muir
