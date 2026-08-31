# HFS

## Understanding HFS and UTF-8 Complications

There’s real care involved in maintaining legacy code that’s evolved alongside the quirks of the array of operating systems we support.

One small—but significant—change I made with the release of Iguana 6.2.1 was to remove support for a legacy file system: Apple’s HFS (Hierarchical File System). HFS dates all the way back to 1985, and Apple formally phased it out around the release of macOS High Sierra (10.13) in 2017, when APFS became the default file system. HFS was finally dropped altogether in macOS Catalina (10.15) in 2019.

One peculiarity of HFS lies in the way it stores file names with accented characters using a unique form of Unicode normalization (specifically, a variant of **NFD**, or decomposed form). This meant, for example, that the filename “café.txt” could be stored on HFS as `café.txt` (with the “é” as an “e” followed by a combining accent), while on NTFS or APFS, it might appear as the single codepoint “é”. Comparing file names across systems frequently led to confusing bugs—as an example:

- **On HFS**: `"café.txt"` (decomposed, U+0065 U+0301)
- **On APFS/NTFS/EXT4**: `"café.txt"` (single character, U+00E9)

To work around this, code had to normalize file names before comparing, adding both complexity and the potential for subtle mismatches.

With HFS now gone from supported versions of macOS, I was delighted to simplify the Iguana 6 codebase and drop this special-case handling in version 6.2.1.

Cleaning up these legacy complexities is important groundwork as we prepare to bring enhancements from Iguana X into Iguana 6—such as the improved HL7 grammar parser.

Maintaining critical infrastructure code is itself a form of stewardship—taking care to safeguard the trust users place in us over decades. Thank you for your continued support as we modernize and heal our foundation.

