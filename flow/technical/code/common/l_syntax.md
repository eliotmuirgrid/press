# Glob Expressions

Several Flow commands accept simple glob expressions for matching names, such as the `--trace` option.

Unlike regular expressions, Flow globs support only a small number of operators, making them fast and easy to understand.

| Pattern             | Description                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `*`                 | Matches zero or more characters.                                                                                                     |
| `+pattern`          | Explicitly includes matching names. (Equivalent to `pattern`.)                                                                       |
| `-pattern`          | Excludes matching names.                                                                                                             |
| `pattern1 pattern2` | Multiple patterns separated by spaces. A match against any positive pattern is accepted unless later excluded by a negative pattern. |

## Examples

```text
APP*
```

Matches:

```
APP
APPinstall
APPserver
```

---

```text
APP* -APPtest*
```

Matches everything beginning with `APP` except names beginning with `APPtest`.

---

```text
APP* TEST*
```

Matches anything beginning with either `APP` or `TEST`.

## Limitations

Flow glob expressions are **not** regular expressions. The following features are **not** supported:

* `?` (single-character wildcard)
* Character classes (`[abc]`)
* Character ranges (`[A-Z]`)
* Regular expression operators (`|`, `()`, `+`, etc.)

Only the `*` wildcard is recognized.

I think it's worth trying to make Flow really deliberately simple. Some developers get very
excited about regular expressions - those arcane bug prone complex matching things.  I think
I will be happy to consider removing those exciting capacities including the string matching
library in Lua - or may be I will keep those - only 600 lines of code.  I want to understand
everything so if I can remove things I will.
