> [BACK](../README.md)

# Moving Files in a Git Repository

When working inside a Git repository, files can be moved in several ways:

- Drag and drop in VS Code or File Explorer
- The normal `mv` command
- The Git-specific `git mv` command

All three can ultimately produce the same result in Git, but they behave slightly differently before the changes are staged.

---

## 1. Normal File Movement

A file can be moved normally using:

```bash
mv old-file.md new-folder/
```

or by dragging and dropping the file in VS Code/File Explorer.

For example:

```bash
mv local-git.md git-github/
```

The operating system moves the file.

However, Git does not initially receive an instruction saying:

> "This file was renamed."

Git instead notices that:

```text
local-git.md
```

has disappeared and:

```text
git-github/local-git.md
```

has appeared.

Before staging, `git status` may therefore show something similar to:

```text
deleted:    local-git.md

Untracked files:
    git-github/local-git.md
```

This does **not** mean anything has gone wrong.

Git simply sees:

```text
old file disappeared
+
new file appeared
```

---

# 2. Staging a Normal Move

After using `mv` or drag and drop, stage the changes:

```bash
git add -A
```

Then check:

```bash
git status
```

Git may now recognise the two changes as a rename:

```text
renamed:
    local-git.md -> git-github/local-git.md
```

The move can then be committed:

```bash
git commit -m "Organise Git documentation"
```

---

# 3. Using `git mv`

Git provides its own move command:

```bash
git mv <source> <destination>
```

For example:

```bash
git mv local-git.md git-github/
```

This moves the file **and stages the change at the same time**.

Therefore:

```bash
git status
```

will usually immediately show:

```text
renamed:
    local-git.md -> git-github/local-git.md
```

There is no separate `git add` required for that move.

---

# 4. `mv` vs `git mv`

## Normal `mv`

```bash
mv local-git.md git-github/
```

Does:

```text
Move file on computer
        ↓
Git notices filesystem changes
        ↓
Changes still need staging
```

Then:

```bash
git add -A
```

---

## `git mv`

```bash
git mv local-git.md git-github/
```

Does:

```text
Move file
    +
Stage the move
```

in one command.

Conceptually:

```text
git mv
≈
move file
+
stage old and new locations
```

---

# 5. Which Should I Use?

When deliberately moving or renaming files that are already tracked by Git:

```bash
git mv
```

is convenient because Git immediately stages the change.

Example:

```bash
git mv old-name.md new-name.md
```

or:

```bash
git mv old-name.md docs/new-name.md
```

However, normal `mv` and drag-and-drop are **not wrong**.

These are also perfectly valid:

```bash
mv old-name.md docs/
git add -A
```

or:

```text
Drag file into another folder
        ↓
git add -A
```

The final committed repository can be exactly the same.

---

# 6. How Git Actually Handles Renames

An important detail is that Git does not permanently store a special:

```text
RENAME FILE A TO FILE B
```

instruction.

Git primarily stores snapshots of repository contents.

When Git later compares commits, it can detect that:

```text
file A disappeared

and

file B appeared with very similar contents
```

and infer that the file was probably renamed.

This is why both:

```bash
git mv file.md docs/file.md
```

and:

```bash
mv file.md docs/file.md
git add -A
```

can eventually appear in Git history as:

```text
renamed: file.md -> docs/file.md
```

---

# Understanding `git add -A`

`git add -A` means:

> Stage all changes in the repository.

This includes:

```text
New files
Modified files
Deleted files
Moved files
Renamed files
```

Example:

```bash
git add -A
```

could stage:

```text
modified:   README.md
new file:   git-github/git-guide.md
deleted:    old-guide.md
renamed:    notes.md -> git-github/notes.md
```

---

# `git add -A` vs `git add .`

These commands often appear to do the same thing:

```bash
git add .
```

and:

```bash
git add -A
```

but there is an important conceptual difference.

## `git add .`

```bash
git add .
```

means:

> Stage changes from the current directory downward.

The `.` means:

```text
current directory
```

If the command is run from the repository root, this often stages almost everything you expect.

---

## `git add -A`

```bash
git add -A
```

means:

> Stage all changes across the entire repository.

This makes it especially useful after reorganising or moving several tracked files.

---

# Example

Suppose the repository originally contains:

```text
workflow-notes/
├── README.md
├── local-git.md
└── docker-commands.md
```

Create folders:

```bash
mkdir git-github docker
```

Move the files normally:

```bash
mv local-git.md git-github/
mv docker-commands.md docker/
```

Now:

```bash
git status
```

may initially show:

```text
deleted:
    local-git.md
    docker-commands.md

untracked:
    git-github/local-git.md
    docker/docker-commands.md
```

Stage everything:

```bash
git add -A
```

Check again:

```bash
git status
```

Git may now show:

```text
renamed:
    local-git.md -> git-github/local-git.md

renamed:
    docker-commands.md -> docker/docker-commands.md
```

Then commit:

```bash
git commit -m "Organise workflow notes by topic"
```

---

# The Same Example Using `git mv`

Instead:

```bash
mkdir git-github docker

git mv local-git.md git-github/
git mv docker-commands.md docker/
```

Then:

```bash
git status
```

The moves are already staged.

Commit them:

```bash
git commit -m "Organise workflow notes by topic"
```

---

# A Safe Workflow

When reorganising files:

```bash
git status
```

Check the repository before making changes.

Then move files:

```bash
git mv old-file.md new-folder/
```

or:

```bash
mv old-file.md new-folder/
```

If normal `mv` or drag-and-drop was used:

```bash
git add -A
```

Check exactly what will be committed:

```bash
git status
```

Then commit:

```bash
git commit -m "Organise documentation"
```

---

# Important: Check Before Using `git add -A`

Because:

```bash
git add -A
```

stages **all changes**, it may also stage unrelated work.

Always use:

```bash
git status
```

before and after staging.

For example, if this appears:

```text
modified: README.md
modified: unfinished-note.md
renamed: local-git.md -> git-github/local-git.md
```

but the unfinished note should not be part of the commit, do not blindly commit everything.

Git allows individual files to be staged instead.

For example:

```bash
git add git-github/local-git.md
```

The general principle is:

```text
Stage together
        ↓
changes that belong together
        ↓
Commit together
```

---

# Quick Reference

| Action | Command | Staged automatically? |
|---|---|---:|
| Move using File Explorer | Drag and drop | ❌ |
| Move using VS Code | Drag and drop | ❌ |
| Move using Bash | `mv file folder/` | ❌ |
| Move using Git | `git mv file folder/` | ✅ |
| Stage changes in current path | `git add .` | ✅ |
| Stage all repository changes | `git add -A` | ✅ |

---

# Rule of Thumb

For tracked files inside a Git repository:

```text
Deliberately moving/renaming a file
            ↓
          git mv
```

For normal filesystem movement:

```text
mv / drag-and-drop
        ↓
    git add -A
```

Both are valid.

`git mv` is simply a convenient Git-aware workflow for moving tracked files.

---

## Renaming a Directory with Git

To rename a directory that contains Git-tracked files, use:

```bash
git mv old-folder new-folder
```

Example:

```bash
git mv vscode vs-code
```

This will:

1. Rename the directory on your computer.
2. Move the tracked files inside it to the new path.
3. Stage those changes automatically.

Check the result with:

```bash
git status
```

Git may show the files inside the directory as renamed:

```text
renamed: vscode/setup.md -> vs-code/setup.md
renamed: vscode/extensions.md -> vs-code/extensions.md
```

### Move and Rename a Directory

You can also move a directory somewhere else and rename it at the same time:

```bash
git mv old-folder new-location/new-folder-name
```

Example:

```bash
git mv images assets/documentation-images
```

### Important

Git does not track directories themselves.

Git tracks:

```text
files
+
their paths
```

So when a directory is renamed, Git is really recording the new paths of the files inside it.

Empty directories are not normally tracked by Git.

---

> [BACK](../README.md) 😮 [TOP](#moving-files-in-a-git-repository)
