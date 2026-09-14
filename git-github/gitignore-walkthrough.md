> [BACK](../README.md)

#### How to create .gitignore in VS Code

Inside the project folder, you can create it in the VS Code Explorer:
1. Click New File.
2. Name it exactly:
```
.gitignore
```
3. Paste the ignore rules.
4. Save it.

In Git Bash, you can also create it with:
```bash
touch .gitignore
```
Then open it in VS Code:
```bash
code .gitignore
``` 

Create .gitignore before doing:
```bash
git add .
```
Your initial workflow would therefore be:
```bash
mkdir MyStrategy
cd MyStrategy

git init

touch .gitignore
code .gitignore
```

Add your ignore rules, then:
```bash
git status
git add .
git status
git commit -m "Create initial LEAN strategy project"
```
The second `git status` is important because it lets you verify exactly what git add . staged.

--- 
#### How to check whether an ignore rule is working
Run:
```bash
git status --ignored
```
This shows ignored files as well as normal files.

To test one particular file:
```bash
git check-ignore -v backtests/result.json
```

Git will show which `.gitignore` rule caused the file to be ignored. The official `git check-ignore` command is specifically designed for debugging ignore rules. example, it might output:

```bash
.gitignore:25:backtests/    backtests/result.json
```

That means line 25 of .gitignore ignored the file.

---
### What if you already staged the files?
Suppose you ran:
```bash
git add .
```
and only afterwards added `.venv/` to `.gitignore`.
If it has not been committed yet, unstage it:
```bash
git restore --staged .venv
```

The folder stays on your computer but is removed from the staging area.

Then check:
```bash
git status
```

---
#### What if it was already committed?
Adding this:
```bash
.venv/
```
will not stop Git tracking a `.venv` that has already been committed.

Use:
```bash
git rm -r --cached .venv
```

Then commit the change:
```bash
git add .gitignore
git commit -m "Stop tracking local virtual environment"
```
`--cached` means:<br>
Remove it from Git’s tracked index, but leave the actual folder on the computer.

Git’s official documentation recommends removing an already tracked file from the index before relying on .gitignore to keep it untracked. can do the same for backtests:

```bash
git rm -r --cached backtests
git commit -m "Stop tracking generated backtest results"
```

---
#### Template
```text
#Recommended .gitignore for your individual LEAN project 
# --------------------------------------------------
# Python-generated files
# --------------------------------------------------

__pycache__/
*.py[cod]
*$py.class


# --------------------------------------------------
# Local Python virtual environments
# --------------------------------------------------
.venv/
venv/
env/

# --------------------------------------------------
# Jupyter-generated files
# --------------------------------------------------
.ipynb_checkpoints/

# --------------------------------------------------
# LEAN-generated results
# Different LEAN versions/workflows may use
# backtest or backtests
# --------------------------------------------------
backtest/
backtests/
live/
optimizations/
report/
reports/
storage/

*.log

# --------------------------------------------------
# PyCharm
# --------------------------------------------------
.idea/

# --------------------------------------------------
# VS Code
#
# Ignore miscellaneous VS Code files, but keep the
# useful LEAN settings and debugging configuration.
# --------------------------------------------------

.vscode/
# --------------------------------------------------
# Environment variables and secrets
# --------------------------------------------------
.env
.env.*
!.env.example

*.key
*.pem
*.token
credentials.json
Secrets.json

# --------------------------------------------------
# Windows and macOS-generated files
# --------------------------------------------------
Thumbs.db
Desktop.ini
.DS_Store

# --------------------------------------------------
# Temporary files
# --------------------------------------------------

*.tmp
*.temp
*.bak
```

---

> [BACK](../README.md) 😮 [TOP](#how-to-create-gitignore-in-vs-code)