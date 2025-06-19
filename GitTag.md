
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


## Checkout a Tag


```bash
git checkout <tag-name>
```

> Example:

```bash
git checkout v1.0.0
```

This puts you in a **detached HEAD state**, meaning you’re not on a branch — you’re just viewing the code at that tag.

### Want to work from that tag?

If you want to make changes or create a new branch:

```bash
git checkout -b new-branch-name v1.0.0
```

---

## 2. Delete a Tag

### Delete a **local tag**:

```bash
git tag -d <tag-name>
```

> Example:

```bash
git tag -d v1.0.0
```

### Delete a remote tag:

```bash
git push origin --delete <tag-name>
```

> Example:

```bash
git push origin --delete v1.0.0
```

### If you updated a tag (e.g. force-retagging):

Delete and re-push:

```bash
git tag -d v1.0.0
git tag -a v1.0.0 -m "Updated release notes"
git push --force origin v1.0.0
```

---


