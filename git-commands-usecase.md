>### Commit whenever you complete one meaningful unit of work.

For example, with workflow-notes, this is probably too much:
```text
Add heading
Fix spelling
Add sentence
Add another sentence
Change file name
```

Instead, something like this is cleaner:

```text
Add virtual environment setup guide
Add LEAN package management notes
Improve Git workflow documentation
Add Markdown image examples
```
And for your finance-book research:

```text
Add Yahoo Finance download example
Add CSV saving workflow
Add return calculations
Add volatility analysis
Refactor data download notebook
```
A really useful pattern is:

```text
Work on something
      ↓
Reach a sensible checkpoint
      ↓
git status
      ↓
Review what changed
      ↓
git add ...
      ↓
git commit
      ↓
Continue working
```

### Rule

> If you can describe the change clearly in one short commit message, it’s probably a good point to commit.

For example:
```bash
git commit -m "Add requirements.txt setup guide"
```
That's a nice commit because you know exactly what happened.

Whereas:
```bash
git commit -m "updates"
```
doesn't tell future-you anything.

One more useful habit: before committing, run:
```bash
git status
```
and ideally:
```bash
git diff
```
That makes you review what you're actually about to record.

```text
Start work
   ↓
Make changes
   ↓
Finish one topic/task
   ↓
git status
   ↓
git diff
   ↓
git add .
   ↓
git commit -m "Clear description"
   ↓
Push when appropriate
```

A simple rule for where you are now would be: commit after each meaningful completed section, and push at the end of a work session or when you want the remote backup updated. That will give you good Git habits without making Git feel like constant admin.

---

#### how to start a project 

```text
New project folder
      ↓
git init
      ↓
Create/check .gitignore
      ↓
git status
      ↓
Review what Git wants to track
      ↓
git add .
      ↓
git commit -m "Initial project setup"
      ↓
Start normal development
```
