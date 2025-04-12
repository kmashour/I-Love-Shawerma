https://khambud.medium.com/head-and-head-in-git-655681c3237e

**Semantics:**

- `HEAD` : The current reference point in a git log.
- `HEAD~` : shorthand for `HEAD~1` . It means reference `HEAD`'s first parent.
- `HEAD~2` : means reference `HEAD`'s grandparent, or first parent’s parent.
- `HEAD~3` : means reference `HEAD`'s great-grandparent, or first parent’s parent’s parent. So you see the pattern… 👍
`~` is used to go number of generation back and is generally linear in appearance.



git reset HEAD~