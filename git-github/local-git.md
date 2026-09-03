## Local Git Workflow

#### One-time Git setup
These commands normally only need to be run once on each computer or user account:

```bash
git config --global init.defaultBranch main
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
The email should be attached to your GitHub account, or it can be your GitHub-provided noreply email.

Check the settings:

```bash
git config --global user.name
git config --global user.email
git config --global init.defaultBranch
```
View all global Git settings:<br>
```bash
git config --global --list
```
---
#### Create a local repository
Create a new directory:
```
mkdir myrepo
```

Enter the directory:
```bash
cd myrepo
```
Initialise the directory as a Git repository:
```bash
git init
```
Check the repository status:
```bash
git status
```
For learning purposes, the hidden .git directory can be viewed with:
```bash
ls -la
```
> The .git directory contains Git’s internal repository information and history.
---

#### Create and commit a file
Create a file:
```bash
touch newfile
```
Check what Git can see:
```bash
git status
```
Add the file to the staging area:
```bash
git add newfile
```

Commit the staged change:
```bash
git commit -m "Add newfile"
```

View the commit history:
```bash
git log
```
Press Q to exit the full git log display.
A shorter history view is:
```bash 
git log --oneline
```
A useful view showing branches is:
```bash
git log --oneline --graph --all
```
---

#### Regular edit-and-commit cycle
After editing or creating files:
```bash
git status
git add <filename>
git commit -m "Describe the change"
```
To stage all current changes:
```bash
git add .
```

> Check `git status` before committing so that you know exactly what will be included

---
#### Create and use a branch
Create a new branch and immediately switch to it:
```bash
git switch -c newbranch
```
Older equivalent:
```bash
git checkout -b newbranch
```

List the branches:
```bash
git branch
```
The active branch is marked with an asterisk:
```bash
* newbranch
  main
```
Switch to an existing branch:
```
git switch main
```
> Older equivalent: `git checkout main`


---
#### Work on the new branch
Switch to the branch:

```bash
git switch newbranch
```

Create a file:
```bash 
touch newbranchfile
```

Stage and commit it:
```bash
git add newbranchfile
git commit -m "Add newbranchfile"
```

Check the history:
```bash
git log --oneline
```
---
#### Revert a committed change
To reverse the most recent commit while preserving the project’s history:

```bash
git revert HEAD --no-edit
```

This creates a new commit that reverses the changes introduced by the previous commit.
It does not remove the original commit from Git’s history. However, if the previous commit added a file, the revert commit will remove that file from the current version of the project.
Without --no-edit, Git may open an editor so that you can confirm or edit the revert commit message.

---
#### Merge a branch into main
Before merging, switch to the branch that should receive the changes:
```bash
git switch main
```
Merge the other branch into main:
```bash
git merge newbranch
```
Check the result:
```bash
git status
git log --oneline --graph --all
```
After the branch has been successfully merged, delete it:
```
git branch -d newbranch
```
The `-d` option safely refuses to delete a branch if Git believes it contains unmerged work.

---
#### Practice exercise
1. Create a branch called `newbranch` and switch to it:
```
git switch -c newbranch
```
2. Create an empty file:
```bash
touch newbranchfile
```
3. Stage and commit it:
```bash
git add newbranchfile
git commit -m "Add newbranchfile"
```
4. Revert the last commit:
```bash
git revert HEAD --no-edit
```
5. Create another file:
```bash
touch newgoodfile
```
6. Stage and commit it:
```bash
git add newgoodfile
git commit -m "Add newgoodfile"
```
7. Switch to `main`:
```bash
git switch main
```
8. Merge the branch:
```bash
git merge newbranch
```
9. Check the result:
```bash
git log --oneline --graph --all
git status
```
10. Delete the merged branch:
```bash
git branch -d newbranch
```

---
#### Extra commands that help

Shows all the files your note tracking:
```bash
git status --untracked-files=all 
```