#### In Git Bash

First make sure you're inside the correct folder:

```bash
pwd
```
Then you can confirm the repo root:
```bash
git rev-parse --show-toplevel
```
If that shows you current folder path, delete .git with:

```bash
rm -rf .git
```
Then:
```bash
git status
```
should return something like:
```text
fatal: not a git repository
```
Your normal files remain untouched.

---

#### Safest approach

Instead of permanently deleting it immediately, you can rename it first:

```bash
mv .git .git-backup
```
Now try:
```bash
git status
```
You should get something like:
```text
fatal: not a git repository
```
If you happy with it then you can proceed with the steps above

---
#### Command - `rm -rf  `
```
rm   = remove

-r   = recursive
       delete folders and everything inside them

-f   = force
       don't ask for confirmation / ignore some prompts
```