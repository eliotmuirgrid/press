# Path

How do your find a file - you have to find a pathway to it.

## What is a File Path?

A **file path** is a string of text that describes the location of a file or folder within a file system. It shows the “route” you need to take, starting from a specific point (such as the root directory or current directory), to get to a particular file or folder.

---

### Key Points

- **File System**: Computers organize files and folders (directories) in a structure called a file system, which is often compared to a tree with branches.
- **Path**: A path is like giving directions to a destination in this tree. It tells the system (and you) exactly where a file or folder is located.

---

### Types of File Paths

1. **Absolute Path**
   - Shows the full, complete address to the file/folder, starting from the root directory.
   - Example (Windows):  
     ```
     C:\Users\Alice\Documents\Report.docx
     ```
   - Example (Linux/macOS):  
     ```
     /home/alice/Documents/report.txt
     ```

2. **Relative Path**
   - Shows the address relative to your current directory.
   - Example:  
     If you’re already in `C:\Users\Alice`, a relative path to the document above would be:  
     ```
     Documents\Report.docx
     ```

---

### Path Separators

- **Windows** uses a backslash (`\`)
- **Linux/macOS** use a forward slash (`/`)

---

### Components of a Path

- **Directories/Folders**: Containers that can store files and other folders.
- **Filename**: The name of the file you want to access (which may also include its extension, like `.txt`, `.docx`).

**Example:**  
`/Users/beth/photos/vacation.jpg`  
Here, `Users`, `beth`, and `photos` are directories, and `vacation.jpg` is the file.

---

### Visual Example

Given a structure like:
```
/
 └── home/
       └── alice/
               ├── Documents/
               │      └── notes.txt
               └── Pictures/
                       └── photo.jpg
```
- Absolute path to `notes.txt`: `/home/alice/Documents/notes.txt`
- Relative path from `alice` directory to `photo.jpg`: `Pictures/photo.jpg`

---

### Summary 

A file path tells you (and your computer) precisely where a file lives in your file system. It’s like an address for a file!


