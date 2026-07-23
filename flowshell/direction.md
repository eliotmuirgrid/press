# I’m getting into Flow.

Both the project itself and, quite literally, a state of flow.

Thankfully, the personal issues that were consuming my attention have begun to fade into the background. Having the space to think clearly again has made an enormous difference.

This project is turning out beautifully.

I’m taking a nap now because this is intellectually demanding work, and I need time to recharge. But every time I come back to it, the architecture feels more coherent.

I’m effectively bootstrapping my entire toolchain using the tool itself.

I suspect, the creator of Cosmopolitan, followed a similarly logical path. Where my approach differs is that I’ve spent most of my career building tools that help developers understand what their software is actually doing. I’m applying those same principles to my own development environment.

The Lua tracing system is coming together, but it will be very different from the tracing system in Iguana. Instead, I’m deliberately making it conceptually similar to how I have historically dones tracing in C++ although I am simplifying that also. The goal isn’t flashy visual interfaces—it’s giving developers complete control over what they see.

One of the lessons I’ve learned over the years is that graphical debugging environments often get in the way. If I need to inspect memory in hexadecimal, I want that view every single time I run the program—not after configuring a collection of stateful windows and clicking through menus.

The tools should adapt to the developer, not the other way around.

My workflow is built around complete transparency. Every function lives in its own file, every function has a globally unique name, and a very simple prefix system allows the dependency graph to emerge naturally. Once you remove unnecessary complexity, everything becomes dramatically easier to navigate, trace, and debug.

I expect to support IntelliSense inside Neovim as well. Rather than embedding everything into the editor, I plan to lightly couple Neovim to an external command-line process so it can leverage the much richer debugging and analysis environment I’m building.

It’s probably the most ambitious project I’ve ever attempted, but it’s also one of the cleanest designs I’ve worked on.

I almost feel like I needed to reach this stage of my career before I could build something like this.

Eventually you’ll be able to download a single binary, have it unpack itself, and automatically retrieve only the development tools you actually need. There won’t be an enormous SDK polluting the operating system.

Every dependency should be a Cosmopolitan binary—or another self-contained executable—downloaded only when required.

Those tools should live together in an isolated environment where they’re obvious, understandable, and trivial to replace if something goes wrong. They should never become entangled with the host operating system in ways that are difficult to understand or repair.

That’s rigorous engineering.

It’s also what produces systems that are simple, trustworthy, and secure.

I’m genuinely proud of how this is coming together.

Once I have socket support, the pace should accelerate dramatically. Initially I’ll probably use curl before implementing my own TLS/SSL implementation which will be very small and not huge like OpenSSL. Once networking is in place, implementing IMAP and SMTP becomes straightforward, allowing the platform to receive and send email natively.

Because the entire environment is transparent and command-line driven, debugging should remain exceptionally simple. That same simplicity also makes unit testing almost effortless to bootstrap.

Since writing C++ functions and exposing them directly to Lua is so lightweight, adding capabilities such as screen capture, mouse control, and keyboard automation becomes natural.

Once AI can inspect the screen and reason about what it’s seeing, the platform can automate workflows that traditional APIs simply can’t reach—including tasks such as navigating multi-factor authentication and interacting with legacy desktop software exactly as a human user would.

It won't be necessary not probably desirable for AI to be used in most production cases.  AI should augment, support and help develop human talent - not replace it.

Combined with browser automation and inspection, this becomes an extremely powerful integration platform.

In many enterprise environments, the idea that APIs are the universal answer simply isn’t true. APIs are often incomplete, overly complicated, or intentionally limited. Many business systems expose only a fraction of the functionality users actually need.

By interacting with software the same way a trusted user does, those limitations largely disappear.

The user can see exactly what’s happening.

Nothing is hidden.

Trust comes from transparency.

Combine that with signed packages, a secure credential store, self-contained deployment, and AI-assisted development, and the platform begins to bootstrap itself remarkably quickly.

Not everything even needs to be written in C++. Many components are perfectly suited to Lua.

That’s one of the strengths of the architecture.

I’m genuinely excited about where this is going.

More than anything, I’m grateful to finally have the mental space to focus on building it instead of being distracted by personal issues. I’m deliberately staying focused until the core architecture is complete.

I think this has the potential to become a platform that other people can build entire businesses on.

For example, someone could use it to distribute secure, sovereign AI models in completely self-contained, cryptographically signed packages that users can inspect and trust.

Everything should be optimized around security, transparency, and verifiability.

Every component should be signed.

Every dependency should be understandable.

Every back door should be impossible by design.

That’s the foundation of trusted private computing.
