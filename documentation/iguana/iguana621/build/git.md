# Git History

I’m quietly happy to be working on streamlining the structure of Iguana 6. It’s deeply satisfying to enhance how the system is built, making it more maintainable and easier for others—and myself—to understand. As I move through this process, I’m dedicated to taking the utmost care—ensuring that the rich history of all the static files bundled with the product is meticulously preserved. This attention to detail isn’t just for me; it’s an investment that will pay off for anyone who works on the codebase in the future.

My guiding principle is simple: leave the codebase better than I found it—much like restoring a classic car, aiming to make it run smoother and look sharper than ever before. With every change, I’m focused on improvements and clear documentation, so the next maintainer will find the code in a simple easy to understand shape much more so than typical C++ projects. 

For context, Iguana 6 originally kept some JavaScript resources in `~/shared_web_docs`. This was intended to make it easier to share resources between the experimental version of the translator, as it was being developed, and Iguana itself. Now, however, this structure no longer makes sense. By moving that code into `~/iguana_complete/web_docs/js`, we can make ongoing development faster and safer, with fewer potential points of failure. At the same time, I’m committed to preserving the Git history, so changes and origins remain easy to trace.

That’s why "pole pole"—going slowly, carefully, and deliberately—is key here. Each step is thoughtful, so the transition brings real improvements while maintaining the integrity of the project’s history and spirit.

Let’s keep making things better, one careful step at a time.

The other source of files was `~/DBD/web_docs`. DBD stood for "DataBase Direct," which was what Iguana was called before it was renamed Iguana. Until my refactoring, the DBD directory was where everything was collected in a messy way—it worked, but it was fragile for ongoing development. It's really important to have clear, obvious logic on how things are built. That makes for clean, efficient, and, above all, safe maintenance of a software program like Iguana.

It's always been my attention to detail that has made Iguana a stable product.

