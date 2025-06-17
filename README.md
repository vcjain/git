

## **What is `git revert`?**

> `git revert` **creates a new commit that undoes** the changes introduced by a previous commit — without rewriting history.

**When to Use `git revert`**

* To **undo a change** that was already pushed to a shared branch (like `main`).
* To **safely fix mistakes** without rewriting history.
* During production issues where you need to roll back one or more commits cleanly.


```bash
git revert <commit-hash>
```

This creates a **new commit** that undoes the effect of the specified commit.

**Example Scenario**

Suppose your commit history looks like this:

```
A -- B -- C -- D (main)
```

Now you realize that commit **C** introduced a bug.

Step 1: Revert commit C

```bash
git revert <commit-hash-of-C>
```

Git will create a new commit **E**:

```
A -- B -- C -- D -- E (main)
```

Commit **E** undoes changes from commit C.

> You’ll still have commit C in history, but its changes are canceled out by E.

---


<br><br>
## **Git Merge vs Git Rebase**

> Both are used to **integrate changes from one branch into another**, but they work differently.

Let's say we have:

* A `main` branch
* A `feature` branch created from `main`

```
# Initial state
        A---B---C (feature)
       /
D---E---F (main)
```

## 1. **Git Merge**

> Combines two branches and creates a **new merge commit** to preserve both histories.

### Command

```bash
git checkout main
git merge feature
```

### Resulting History

```
        A---B---C (feature)
       /         \
D---E---F---------M (main)
```

* `M` is a new **merge commit**
* History is **non-linear**
* No commits are rewritten


## 2. **Git Rebase**

> **Moves commits** from one branch onto another by **replaying them**.

### Command

```bash
git checkout feature
git rebase main
```

### Resulting History

```
D---E---F---A'---B'---C' (feature)
```

Now if we do:

```bash
git checkout main
git merge feature
```

Final result:

```
D---E---F---A'---B'---C' (main)
```

* History is **linear**
* Looks like all work happened sequentially

---

<br><br>

## **Workflow: Working with a Forked Repository**

> You fork a project, make changes in your fork, and want to sync with the original repo and submit your changes for review (usually via a pull request).

###  Terminology

* **Upstream**: The original repository you forked from.
* **Origin**: Your forked version (remote on your GitHub account).


### Set Up Remotes

After forking and cloning your repo locally:

```bash
git clone https://github.com/your-username/project-name.git
cd project-name
```

Add the original repo as **upstream**:

```bash
git remote add upstream https://github.com/original-owner/project-name.git
```

Verify remotes:

```bash
git remote -v
```

You should see:

```
origin    https://github.com/your-username/project-name.git (fetch)
upstream  https://github.com/original-owner/project-name.git (fetch)
```

---

### Fetch and Sync with Upstream 

#### Fetch changes from upstream:

```bash
git fetch upstream
```

#### Merge into your local main branch:

```bash
git checkout main
git merge upstream/main
```

> OR use rebase for a clean history:

```bash
git rebase upstream/main
```

### Create a Feature Branch

Never work directly on `main`. Create a new branch:

```bash
git checkout -b feature/my-changes
```

Make your code changes, then:

```bash
git add .
git commit -m "Add feature/fix"
```


### Push Changes to Your Fork

```bash
git push origin feature/my-changes
```


### Create a Pull Request (PR)

1. Go to your fork on GitHub.
2. You’ll see a “Compare & pull request” button — click it.
3. Ensure the base repo is **original repo** and the base branch is `main`.
4. Add title, description, and click **Create pull request**.

---


