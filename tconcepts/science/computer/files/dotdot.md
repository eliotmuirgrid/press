# Dot Dot

**What does .. mean in file paths?**

## **Explanation:**

- **`.`** (single dot): refers to the **current directory**.
- **`..`** (double dots): refers to the **parent directory**.

---

### **Examples**

Suppose you are in the directory:

```
/home/user/documents
```

- **`..`** would refer to:
  ```
  /home/user
  ```
- **`../photos`** would refer to:
  ```
  /home/user/photos
  ```
- **`./report.txt`** refers to a file in the **current directory** (`/home/user/documents/report.txt`).

---

## **Usage in Commands**

Let's say you are in the directory `/home/user/documents` and you want to go up one level:

- **In Linux/macOS Terminal or the Windows Command Prompt:**
  ```
  cd ..
  ```
  (Moves you to `/home/user`)

---

## **Summary Table**

| Notation | Meaning             | Example Path                   |
|----------|---------------------|-------------------------------|
| `.`      | current directory   | `./file.txt`                  |
| `..`     | parent directory    | `../file.txt`                 |

---

**In short:**  
> The `..` in file paths always points up one folder, or the "parent directory.


