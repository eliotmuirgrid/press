# Home

**What is a HOME Directory?**

When you use a computer, especially a Linux or Mac computer (but Windows has something similar), you usually have a **user account**. Just like every person in a house might have their own room, every user on a computer gets their own **space**—this is their **HOME directory**.

## HOME directory 

This is simply a folder where all your stuff (your documents, music, pictures, configuration files, etc.) is kept. It helps keep everyone’s files separate and organized.

For example:
- If your username is **alice**, your home directory might be `/home/alice` on Linux.
- If your username is **bob**, it might be `/home/bob`.

---

## What is `~` (Tilde)?

The **tilde symbol** (`~`) is a shortcut. Instead of typing out your full HOME directory path (like `/home/alice`), you can just use `~` in the command line. For example:
```
cd ~
```
will take you straight to your HOME directory no matter what your username is.

---

## What is the HOME Environmental Variable?

**Environmental variables** are like little signs or labels that the computer uses to keep track of information.

The `HOME` environmental variable is a special variable that stores the path (the location) of your HOME directory. So, if your HOME directory is `/home/alice`, then:
- `HOME` = `/home/alice`

You can see what yours is by typing:
```
echo $HOME
```
This will print the location of your home directory.

---

## How Do `HOME` and `~` Relate?

- The tilde `~` *is a shortcut* that always means: "the folder whose path is stored in the HOME environmental variable".
- So, whether your HOME directory is `/home/alice` or something else, `~` will always take you there, because the computer checks the value of the `HOME` variable to know where "home" is.

Put simply:
- `~` lets YOU type less.
- `HOME` lets the COMPUTER keep track of where "your stuff" is.

---

## Summary

- **HOME directory:** the main folder for your account with all your files.
- **HOME environmental variable:** the computer’s way of remembering where your HOME directory is located.
- **`~` (Tilde):** a shortcut you can use that always means "my home directory" (whatever it may actually be).

So, when you type `cd ~`, the computer looks up the `HOME` environmental variable to figure out where to send you
