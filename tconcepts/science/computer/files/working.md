# Working 

**What is your focus?**

## What is a Working Directory?

When you use the command line (such as Bash, Command Prompt, or PowerShell), your session is always “operating” inside a particular folder on your computer. This folder is called the **working directory** (sometimes called the “current directory”).

---

## Why is it Important?

- **Command Context:** Any command you run that refers to files (e.g., `ls`, `cat`) will act on files *relative* to the working directory (unless you give the full path).
- **Navigation:** You can move your working directory using commands like `cd` (`change directory`).

---

## Example

Let’s say your current working directory is `/home/user/projects`:

- If you type `ls`, you'll see files **inside `/home/user/projects`**.
- If you type `cat notes.txt`, the computer will look for `notes.txt` **inside `/home/user/projects`**.

If you want to work in another directory, use `cd some-directory/` to **change your working directory**.

---

## Viewing the Working Directory

- On Unix/Linux/macOS: use `pwd` (print working directory)
- On Windows Command Prompt: use `cd` alone

---

## Summary: 
The working directory is your “current folder” in the command line, and it determines what files your commands interact with unless you specify a different path

