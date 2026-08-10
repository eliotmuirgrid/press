# Links

## Links in Markdown

Markdown allows you to create **links** (also called **hyperlinks**) between documents/files. This is very useful when you want to reference or jump between related documentation, pages, or resources.

### How Markdown Link Syntax Works

The basic syntax for creating a link in Markdown is:
```markdown
[Link Text](target-path)
```
- **Link Text:** The text that will be displayed as clickable.
- **target-path:** The location or address where the link should go when clicked (can be a file path or a URL).

---

## Understanding File Paths for Links

Markdown links work very much like [file paths you’d use in your file system](../files). The path in your link tells Markdown where to "find" the document you want to link to.

- **Relative Paths**: Link to files relative to the current document’s location.
    - `./otherpage.md` – The file is in the same directory as your current file.
    - `../readme.md` – The file is in the parent directory.
    - `docs/guide.md` – The file is in a `docs` folder inside your current directory.

- **Absolute Paths**: Less commonly seen in Markdown repositories, but can be used on certain websites.
    - `/docs/guide.md` – This means from the root directory.

- **Web URLs**: You can also link to external websites.
    - `[Google](https://www.google.com)`

In [Flow Publish](/flow/publish) links do not need to have the ".md".  If that is omitted the
linking system is able to figure it out.  Ideally links should be very tolerant to human users.

Our vision is to make linking systems which don't require the human user to distinguish between
using the word "remove" or "delete" or "add" or "create" since they mean the same thing. See [semantic linking](../files/semantic.md).

---


## Examples

| Markdown                                   | Result                            |
|---------------------------------------------|-----------------------------------|
| `[Home](README.md)`                        | Links to `README.md`              |
| `[Guide](docs/guide.md)`                    | Links to `docs/guide.md` file     |
| `[Up one level](../readme.md)`              | Links to parent dir's `readme.md` |
| `[Google](https://google.com)`              | Links to the Google website       |

---

## Key Takeaways

- Markdown links work like file system paths.
- The path you specify tells Markdown where to find the linked document.
- Use `./` for the current directory, `../` for parent directories.
- You can link to both local files and external web pages.

