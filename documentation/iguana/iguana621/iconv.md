# ICONV

**iconv** is an essential utility commonly found on Unix-like systems. It stands for "international conversion," and its primary function is to convert text from one character encoding to another. This capability is particularly useful when dealing with files created in different regions or systems, where encoding formats may vary (for example, converting between UTF-8 and ISO-8859-1). By enabling seamless conversion of file encodings via the command line or within scripts, iconv helps ensure compatibility and proper display of text data across various platforms and applications.

On modern versions of MacOS, iconv is bundled as a standard part of the operating system—thoroughly tested and maintained by Apple. For Iguana, this means it can confidently rely on the system-supplied implementation of iconv on MacOS, which is likely better integrated and likely to receive timely updates and security fixes. As a result, it is preferable for Iguana to use the MacOS-provided version of iconv rather than including its own copy, which would only add unnecessary bloat and maintenance overhead.

The situation on Linux, however, requires more careful consideration. The availability and versions of iconv can differ widely between distributions, so shipping a bundled version could help ensure consistent behavior across all environments.

I first noticed a problem with iconv when I found that the initial build of Iguana 6.2.1 was crashing on my system. The crash was traced to file logic that invoked iconv to handle issues arising from an old Apple filing system called HFS.

To some, cross-platform development might seem an unnecessary complication, but it actually encourages a heightened awareness of simplicity. This focus on simplification is what has made Iguana so stable—and why our customers have trusted it for so many years. But it’s important to remember: simple doesn't come easy.

I hope to eventually remove the iconv library from Iguana 6, but first I’ll need to carefully determine if there is any customer code that still depends on it. Perhaps we can detect calls to iconv code and ask customers to report the usage to us?

Today things have standardized on UTF8 and so it may be that we say goodbye to this friction.

