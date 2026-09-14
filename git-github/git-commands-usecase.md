> [BACK](../README.md)

### **Commit whenever you complete one meaningful unit of work.**

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

### **How to start a project**

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
---

### **A good workflow for your own projects**

```
                YOUR LAPTOP
                     │
                   main
                     │
              create a branch
                     ↓
             feature/new-work
                     │
              make changes
                     │
                 commit
                     │
                test/check
                     │
               merge to main
                     │
                     ↓
                  git push
                     │
                     ▼
                   GITHUB
```

#### **1. Keep main as the stable version**

Think of:
```
main
```
as:

> "The current good version of my project."

Try not to use `main` as your scratchpad.

Suppose you want to add a new section to your finance research.

Instead of immediately editing `main`, you could do:
```bash
git switch -c yahoo-data-analysis
```

Now:
```
main
 │
 └── yahoo-data-analysis
```

You're working on another branch.

#### **2. Work on the branch**

Edit files normally.

Then:
```bash
git status
git add .
git commit -m "Add Yahoo Finance data analysis"
```

You may make several commits:
```text
main
  │
  └── yahoo-data-analysis
        │
        ├── Commit 1: Add download code
        ├── Commit 2: Add data cleaning
        └── Commit 3: Add charts
```

Meanwhile main hasn't changed.

That's the safety benefit of branching.

#### 3. When you're happy, return to main
```bash
git switch main
```

Now merge your work:
```bash
git merge yahoo-data-analysis
```

You get:
```text
BEFORE

main
  │
  A
   \
    B ── C ── D
        yahoo-data-analysis


AFTER MERGE

main
  │
  A ── B ── C ── D
                  ↑
                 main
```
Now your completed work is part of `main`.

#### **4. Push the completed `main` to GitHub**

Then:
```bash
git push
```

Direction:
```text
YOUR LAPTOP                         GITHUB

main                               main

A ─ B ─ C ─ D ─────────────────→ A ─ B ─ C ─ D
```

That's probably the simplest workflow for you initially.

#### **So why did IBM push branches to GitHub?**

Because you can push branches independently.<br>
Suppose locally you've got:

```text
main
│
└── yahoo-data-analysis
```

You could push that branch before merging it:
```bash
git push -u origin yahoo-data-analysis
```

Then GitHub gets:
```text
GITHUB

main

yahoo-data-analysis
```

but the new work still isn't in GitHub's `main`.

That has several uses.

#### **Backup**

Your unfinished branch now exists on GitHub too.

If your laptop dies:
```text
local branch ❌

GitHub branch ✅
```

#### **Working across computers**

You can continue the same branch elsewhere.

#### **Collaboration**

Someone else can see/review your branch.

#### **Pull requests**

GitHub can compare:
```text
yahoo-data-analysis
        ↓
      merge into
        ↓
       main
```

and create a Pull Request.

### **Recommended**

1. main is stable

2. Create branch for meaningful new work

3. Work locally

4. Commit as you go

5. Finish/test the work

6. Merge locally into main

7. Push main to GitHub

8. Delete old branch when finished

```text
PERSONAL PROJECT WORKFLOW

                LOCAL COMPUTER

                    main
                      │
                      ↓
                create branch
                      │
                      ↓
                   work
                      │
                      ↓
                  commit(s)
                      │
                      ↓
                   finish
                      │
                      ↓
              switch back to main
                      │
                      ↓
                  merge branch
                      │
                      ↓
                   git push

                      │
                      ▼

                    GITHUB
                 updated main
```

> [BACK](../README.md) 😮 [TOP](#commit-whenever-you-complete-one-meaningful-unit-of-work)