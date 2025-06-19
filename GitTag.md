
## Git offers two types of tags:

### Lightweight Tags

* **Simplest form** of a tag.
* It's like a branch that doesn’t move — just a pointer to a specific commit.
* Does **not store any extra information** (like tagger name, date, message).


#### Usage:

```bash
git tag v1.0.0
```

This creates a lightweight tag named `v1.0.0` pointing to the current commit.

You can also tag a specific commit:

```bash
git tag v1.0.0 <commit-hash>
```

---

### Annotated Tags

* **Recommended for public releases**.
* Stores metadata like:

  * Tagger name
  * Tag date
  * Tag message
* Internally, it’s stored as a full Git object.

#### Usage:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

`-a` stands for annotated and `-m` is the tag message.

You can also annotate a specific commit:

```bash
git tag -a v1.0.0 <commit-hash> -m "Tagging the first release"
```

---

### Pushing Tags to Remote

By default, tags are **not pushed** with `git push`. You need to explicitly push them:

* Push a specific tag:

```bash
git push origin v1.0.0
```

* Push all tags:

```bash
git push --tags
```

---

### Listing Tags

```bash
git tag
```

### Viewing Tag Details

* For **annotated tags**:

```bash
git show v1.0.0
```

---

