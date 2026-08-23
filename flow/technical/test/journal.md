# Journal

**Easily Testing Functions that Modify the File System**

Testing functions that alter the file system can be challenging. One effective solution is to introduce a "journal mode" for fundamental file operations such as:

- Writing files  
- Deleting files or directories  
- Renaming files or directories  

This journal can use a straightforward, human-readable format like JSON. Binary content may be safely represented in base64 encoding.

Another useful enhancement is implementing a virtual file system as an overlay on the real file system. This overlay can also be described in JSON, allowing easy tracking and manipulation of file system changes without affecting the actual environment.

Such an approach is particularly valuable for writing automated unit tests with a clear, declarative structure. By running in test mode and reviewing the intended changes before applying them, developers gain significantly greater control and confidence.

Overall, this technique would benefit both the development workflow and, later on, sandboxing customer code as it’s migrated to the new framework. It opens the door to safer experimentation and more reliable code transitions.

