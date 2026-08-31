# Libtool

The difficulty of maintaining longevity in code bases.

**Libtool** is a crucial utility for building cross-platform C and C++ projects, helping manage the complexities of creating shared libraries such as `.so` files on Linux or `.dll` files on Windows. While Libtool works to smooth over these differences, issues can arise unexpectedly—especially when the libraries or tools you depend on are updated and change their use of Libtool behind the scenes. This is where frustration and confusion often start.

Personally, I would never use this tool. It came along for the ride with some third-party libraries like [iconv](iconv.md), which Iguana 6 uses.

Maintaining reliable C++ code that runs smoothly across Linux, macOS, and Windows is an ongoing challenge. Every operating system has its quirks—from compilers to folder structures—and keeping everything aligned takes meticulous attention to detail. For instance, the stability of the **Iguana** project is a result of this careful management of the build system, underscoring how much work goes into keeping code stable over time.

**Cross-platform code forces rigor, which is why Iguana is so stable.** You really, really have to simplify code to make it manageable.

Despite advances in automation and artificial intelligence, letting AI handle C++ builds isn’t practical—at least not yet. There’s too much nuance and risk involved, with context-specific knowledge required to keep things stable and portable. For now, the careful oversight of an experienced developer is irreplaceable.

A common stumbling block relates to a simple naming difference between **libtool** and **libtoolize**. Some build scripts expect an executable named **libtool**, which is responsible for compiling and linking shared objects. However, on certain systems or after updates, only **libtoolize** might be available—this tool is intended for setting up support files for libtool, not for the build itself. If build scripts don't find the expected tool, the process can break down entirely. Minor variations like this can cause significant disruption, leading to failed builds and manual troubleshooting.

The key takeaway is that cross-platform C++ development requires constant vigilance, especially as tools like Libtool continue to evolve. Seemingly insignificant changes—like a single tool’s name—can derail an entire build process. Automation isn’t foolproof, and careful, knowledgeable humans remain the essential safety net keeping complex build systems running smoothly everywhere.

My goal is ultimately to see if I can eliminate this tool and make Iguana 6 like Iguana X, which is just a single binary.

Simplicity is important for making stable infrastructure. It’s a profound responsibility.

