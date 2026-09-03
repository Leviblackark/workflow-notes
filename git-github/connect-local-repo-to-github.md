#### Connect local repo to Github

Your local repository does not need to already be on GitHub to use Git. But for a `fine-grained token`, GitHub can only offer you repositories that already exist on GitHub when you choose “Only select repositories.”

```text
LOCAL GIT REPOSITORY
        ↓
connect it to
        ↓
GITHUB REPOSITORY
        ↓
authenticate yourself
        ↓
push commits
```

---

#### Get your local repo ready first

Inside your local project:

```bash
git status
```

Make sure you've got your .gitignore sorted out so you aren't about to upload things such as:
```text
.venv/
.env
__pycache__/
.ipynb_checkpoints/
```

Then make your first commit if you haven't already:
```bash
git add .
git commit -m "Initial project setup"
```
At this point you have:
```text
Laptop
└── Git repository ✅

GitHub
└── nothing yet
```

---

#### Create an EMPTY repository on GitHub

Go to GitHub and choose:

```text
+ → New repository
```

Give it the name you want, for example:

myrepo-on-local

Because you already have the files locally, GitHub specifically recommends that you do not initialise the GitHub repository with a **README**, `.gitignore`, or **licence** at this stage. Otherwise GitHub creates its own first commit and you've then got two independent histories to reconcile.

So you'd create:

GitHub
```text
myrepo-on-local
└── empty repository
```

Now something important has changed:

> The repository exists on GitHub, even though none of your local files have been pushed yet.

And therefore it can now appear in the repository list when creating a fine-grained token.

---

#### Create the fine-grained token

Now go:
```text
Settings
↓
Developer settings
↓
Personal access tokens
↓
Fine-grained tokens
↓
Generate new token
```

For **Resource owner**, choose your GitHub account.

Then at Repository access, you can choose:
```text
Only select repositories
```

and your newly created:
```text
myrepo-on-local
```

should be available.

For normal Git push/pull work, you can give the token only the repository permissions it needs rather than broad account-wide access. GitHub explicitly recommends choosing the minimum repository access necessary.

---

#### But what if you're going to have lots of repos?

This is where I wouldn't create a new token for every little repository.

You might eventually have:
```text
GitHub
├── workflow-notes
├── python-for-finance-cookbook-research
├── quantconnect-strategies
├── data-analysis-project
├── sql-project
└── finance-dashboard
```

You have three practical approaches.
```text
One token per repo
Token A → workflow-notes
Token B → finance-cookbook
Token C → quant-project
Token D → SQL-project
```

This gives very strong separation, but it becomes annoying to manage.

For personal learning repositories, I think this is overkill.

#### One fine-grained token covering your selected development repos

Much more practical:
```text
Personal Git token
       │
       ├── workflow-notes
       ├── python-for-finance-cookbook-research
       ├── quant-project
       └── data-analysis-project
```

You still avoid:
```text
All repositories
```

if you don't need it, but one credential can cover the handful of repositories you're actively developing.

That's a reasonable balance between:
```text
Security ←──────────────→ Convenience
```

---

#### Connect your local repo to GitHub

After creating the empty GitHub repository, GitHub gives you an HTTPS address like:

```text
https://github.com/YOUR-USERNAME/python-for-finance-cookbook-research.git
```

From inside your local repository, run:
```bash
git remote add origin https://github.com/YOUR-USERNAME/python-for-finance-cookbook-research.git
```

Break that down:
```text
git remote
    ↓
I'm dealing with another repository

add
    ↓
Save a new remote

origin
    ↓
Give that remote this nickname

https://github...
    ↓
This is its actual address
```

You can verify it:
```bash
git remote -v
```

You'll see something resembling:
```text
origin  https://github.com/.../python-for-finance-cookbook-research.git (fetch)
origin  https://github.com/.../python-for-finance-cookbook-research.git (push)
```
GitHub documents this exact git remote add origin workflow for adding existing local repositories.

---

#### Push your existing commits

If your branch is already called `main`

```bash
git push -u origin main
```

The first push is slightly special.
```text
git push
    ↓
send commits to GitHub

-u
    ↓
set the upstream/tracking relationship

origin
    ↓
GitHub remote

main
    ↓
your local branch
```

After that first command:
```text
local main
    ↕
origin/main
```

are associated with each other.

So future pushes can usually just be:
```bash
git push
```

and pulls:
```bash
git pull
```

GitHub's current instructions for adding an existing local repository use this same workflow.

---

#### Your whole first-repo process

```text
LOCAL

workflow-notes/
└── .git/
      ↓

1. Check .gitignore
      ↓
2. git add .
      ↓
3. git commit
      ↓

GITHUB

4. Create EMPTY workflow-notes repository
      ↓
5. Set up authentication
      ↓

LOCAL

6. git remote add origin <URL>
      ↓
7. git remote -v
      ↓
8. git push -u origin main
      ↓

GITHUB

9. Refresh page
      ↓
Your files appear 🎉
```

---

#### Full Breakdown Explained

There are only two actual repositories in the basic setup:

1. The Git repository on your laptop
2. The Git repository on GitHub

`remote`, `origin`, and `upstream` are not additional repositories. They are just Git's way of remembering how those two repositories relate to each other.

---

#### 1. You start with a normal folder on your laptop

Suppose you have:
```text
YOUR LAPTOP

Documents/
└── generalised-research/
    └── workflow-notes/
        ├── README.md
        ├── venv-walkthrough.md
        └── git-guide.md
```

At this point it's just a folder.

Git isn't doing anything yet.

Then you run:
```bash
git init
```

Git creates:
```text
workflow-notes/
├── .git/
├── README.md
├── venv-walkthrough.md
└── git-guide.md
```

Now:
```text
workflow-notes/
        ↓
LOCAL GIT REPOSITORY
```

The word local just means:

> It's on your computer.

GitHub still has absolutely nothing to do with this yet.

---

#### 2. You make commits locally

You might run:
```bash
git add .
```

then:
```bash
git commit -m "Set up workflow notes"
```

Now Git has stored your first snapshot.

Think:
```text
YOUR LAPTOP

workflow-notes/
│
├── Your actual files
│
└── .git/
    └── Git history
         │
         └── Commit A
```

If you now disconnect your Wi-Fi, Git still works.

You can continue:
```bash
git add .
git commit
git status
git log
```

because all of this is happening on your laptop.

So far:
```bash
LAPTOP

Local Git repo ✅


GITHUB

Nothing ❌
```

---

#### 3. Now you create a repository on GitHub

You go to GitHub and create:
```text
workflow-notes
```

Because your project already exists locally, you'd normally create an empty GitHub repository.

Now you have:
```text
YOUR LAPTOP                         GITHUB

workflow-notes/                    workflow-notes
┌──────────────────┐              ┌──────────────────┐
│ Local repository │              │ GitHub repository│
│                  │              │                  │
│ Commit A         │              │ currently empty  │
└──────────────────┘              └──────────────────┘
```

These are now two separate Git repositories.

But here's the important part:

**They don't know about each other yet.**

Your laptop doesn't automatically know:

> "Oh, that GitHub repository belongs to me."

You have to connect them.

---

#### 4. This is where remote comes in

You run something like:
```bash
git remote add origin https://github.com/YOUR-NAME/workflow-notes.git
```

This command does **not upload anything**.

It simply tells your local Git repository:

> There is another Git repository located at this address.

That's what remote means.

A remote is essentially:

> Another Git repository that my local repository knows how to reach.

In your case, that other repository is hosted on GitHub.

So:
```text
YOUR LAPTOP

workflow-notes/
┌──────────────────────────┐
│ Local Git repository     │
│                          │
│ Knows about another repo │
│                          │
│         ↓                │
│ GitHub URL stored        │
└─────────┬────────────────┘
          │
          │ Internet
          ▼
          
GITHUB

workflow-notes
┌──────────────────────────┐
│ Remote Git repository    │
└──────────────────────────┘
```

So remote does not mean GitHub itself.

**A remote is the connection information your local Git repository stores about another repository.**

---

#### 5. Then what is origin?

This is where Git terminology sounds much scarier than it is.

Look again:
```text
git remote add origin https://github.com/YOUR-NAME/workflow-notes.git
```

Break it down:
```text
git remote
    ↓
I'm dealing with another repository

add
    ↓
Save a new remote

origin
    ↓
Give that remote this nickname

https://github...
    ↓
This is its actual address
```

So:
```text
origin
```

**is literally just a nickname.**

Your local Git repository stores something roughly like:
```text
Remote nickname:
origin

Actual address:
https://github.com/YOUR-NAME/workflow-notes.git
```

Think of your phone contacts.

Instead of remembering:
```text
+44 7123 456789
```
you save
```text
Mum
```

Then:
```text
Mum
   ↓
+44 7123 456789
```

Git does something similar:
```text
origin
   ↓
https://github.com/YOUR-NAME/workflow-notes.git
```

That's really all `origin` is.

---

#### 6. So now what does your setup look like?

After:

git remote add origin https://github.com/YOUR-NAME/workflow-notes.git

you have:
```text
YOUR LAPTOP

workflow-notes
┌───────────────────────────┐
│ Local Git repository      │
│                           │
│ Commit A                  │
│                           │
│ Remote saved:             │
│                           │
│ origin                    │
│   ↓                       │
│ github.com/.../workflow   │
└─────────────┬─────────────┘
              │
              │
              ▼
              
GITHUB

workflow-notes
┌───────────────────────────┐
│ GitHub repository         │
│                           │
│ Currently empty           │
└───────────────────────────┘
```

Still nothing has been uploaded.

You've simply told Git where GitHub is.

---

#### 7. `git remote -v`

Now this command should make much more sense:
```bash
git remote -v
```

You're essentially asking:

> **"Local Git, show me the other repositories you know about and their addresses."**

You might get:
```text
origin  https://github.com/YOUR-NAME/workflow-notes.git (fetch)
origin  https://github.com/YOUR-NAME/workflow-notes.git (push)
```

In plain English:
```text
I have a remote called:
origin

It points to:
https://github.com/YOUR-NAME/workflow-notes.git
```
The **(fetch)** and **(push)** parts mean:
```text
fetch
Git can receive information from here

push
Git can send information here
```

So you were basically right before:

> `git remote -v` checks that I've connected it.

I'd word it slightly more precisely:

> **It confirms that your local repository has the GitHub repository's address saved correctly.**

It doesn't actually test your token or prove GitHub is online.

---

#### 8. Now we finally send something to GitHub

At this stage:
```text
LAPTOP

Commit A ✅


GITHUB

Nothing ❌
```

Now run:
```bash
git push -u origin main
```

This is the command that actually sends your commits over the internet to GitHub.

Let's follow it physically.
```text
LOCAL LAPTOP

workflow-notes
      │
      │
      │ git push
      ▼
Git takes your commits
      │
      │
      ▼
Looks up "origin"
      │
      ▼
https://github.com/...
      │
      │ Internet
      ▼
GitHub asks:
"Are you allowed to do this?"
      │
      ▼
Authentication
PAT / Git Credential Manager
      │
      ▼
GitHub accepts the push
      │
      ▼
GITHUB REPOSITORY
now receives your commits
```

This is where your token fits.

The token isn't `origin`.

The token isn't the repository.

It's just the **proof of permission during communication**:
```text
Laptop
   │
   │ git push
   ▼
Authentication
   │
   │ "Yes, this is Morgan and they're allowed"
   ▼
GitHub
```

---

#### 9. Breaking down git push -u origin main

Now each part:
```bash
git push -u origin main
```

**`git`**

Use Git.

**`push`**

Send commits from my laptop to another repository.

Direction:
```text
LOCAL → GITHUB
```

**`origin`**

Which other repository?

Git looks up:
```text
origin
   ↓
https://github.com/YOUR-NAME/workflow-notes.git
main
```

Which local branch should I send?

Your branch is:

**`main`**

So:
```bash
git push origin main
```

basically means:

> **Send my local `main` branch to the GitHub repository whose nickname is `origin`.**

That's already most of the command.

---

#### 10. Then what does `-u` mean?

This is the piece that confused you before.

Imagine you didn't use `-u`.

You could do:
```bash
git push origin main
```

and it would work.

But next time Git might again need you to specify:
```text
Where?
→ origin

Which branch?
→ main
```

So instead you use:
```bash
git push -u origin main
```

The -u tells Git:

> **"Also remember that when I'm on my local `main` branch, I normally want it connected to the `main` branch at `origin`."**

So Git remembers:
```text
LOCAL

main
 │
 │ normally communicates with
 ▼
origin's main
 │
 ▼
GITHUB
```

That's the **upstream relationship**.

---

#### 11. Forget the word upstream for a second

A much easier phrase is:
```text
Default partner branch
```

After:
```bash
git push -u origin main
```

Git remembers:
```text
My local main
        ↕
GitHub main
```

So next time, while you're on main, Git already knows:
```text
Which remote?
→ origin

Which branch?
→ main
```

That's why you can now simply type:
```bash
git push
```

instead of:
```bash
git push origin main
```

---

#### 12. What has happened after the first push?

Before:
```text
YOUR LAPTOP                         GITHUB

main                               main

Commit A                           empty
```

After:
```bash
git push -u origin main
```

you now have:
```text
YOUR LAPTOP                         GITHUB

main                               main

Commit A ───────────────────────→ Commit A
```

And Git remembers:
```text
local main
    ↕
GitHub main
```

So both repositories now have the same commit.

---

#### 13. Now you continue working locally

Suppose you edit:
```text
venv-walkthrough.md
```

You save it.

GitHub doesn't immediately get that change.

Right now:
```text
YOUR LAPTOP                         GITHUB

File changed                       Old version
```

Then:
```text
git add venv-walkthrough.md
```

puts the change in staging.

Then:
```bash
git commit -m "Improve virtual environment guide"
```
creates a new local commit.

Now:
```text
YOUR LAPTOP                         GITHUB

Commit A                           Commit A
   │
   ▼
Commit B
```
Your laptop is now one commit ahead of GitHub.

---

#### 14. Then you type just:
```bash
git push
```

Git remembers from the first `-u`:
```text
I'm on local main.

Local main's partner is:
origin/main.

origin points to GitHub.

Therefore send Commit B there.
```

So:
```text
YOUR LAPTOP                         GITHUB

Commit A                           Commit A
   │                                 │
   ▼                                 ▼
Commit B ───────────────────────→ Commit B
```

Now they're matched again.

That's normal everyday push.

--- 

#### 15. Push always means this direction
```text
PUSH

LOCAL LAPTOP
     │
     │
     ▼
   GITHUB
```

So:
```bash
git push
```
means:

> **Send commits I have locally that GitHub doesn't have yet.**

Importantly, Git pushes commits.

Not merely whatever happens to be saved in VS Code.

So:
```text
Edit file
   ↓
git add
   ↓
git commit
   ↓
git push
```

---

### 16. Then what is git pull?

Now imagine something changes in the other direction.

For example, perhaps you use a second computer:
```text
Laptop A
Desktop B
GitHub
```

You push a change from Desktop B.

Now GitHub has:
```text
Commit C
```

but Laptop A only knows:
```text
Commit B
```

So:
```text
LAPTOP A                           GITHUB

A ── B                            A ── B ── C
```

You go to Laptop A and run:
```bash
git pull
```

Git remembers:
```text
This local main tracks GitHub main.
```

So it retrieves the new change:
```text
LAPTOP A                           GITHUB

A ── B ── C    ←───────────────   A ── B ── C
```

So:
```text
PULL

LOCAL LAPTOP
     ▲
     │
     │
   GITHUB
```

In beginner terms:

> **Push = send my changes to GitHub.**

> **Pull = bring GitHub's changes down to my laptop.**

---

#### When would you use git pull?

Suppose you're always working on one computer and never edit files directly on GitHub.

You might barely need it.

But imagine:
```text
Monday:
Laptop → make changes → push

Tuesday:
Another computer → make changes → push

Wednesday:
Back on laptop
```

Your laptop is now behind GitHub.

So before working:
```bash
git pull
```
brings down Tuesday's work.

Then you continue.

---

### Now let's place every confusing term on ONE diagram

This is the one I'd save in your Markdown notes:
```
                         YOUR LAPTOP
                         
                  workflow-notes/
                 ┌───────────────┐
                 │ Local Git repo│
                 │               │
                 │ Branch: main  │
                 └───────┬───────┘
                         │
                         │
              saved remote connection
                         │
                         │
              nickname: "origin"
                         │
                         │
                         ▼
          https://github.com/.../workflow-notes.git
                         │
                         │
                   INTERNET
                         │
                         ▼
                   Authentication
                 Token / Credential
                         │
                         ▼
                       GITHUB
                 ┌───────────────┐
                 │ workflow-notes│
                 │               │
                 │ Branch: main  │
                 └───────────────┘
```
The important thing is:
```text
LOCAL REPOSITORY
= actual repository on your computer


GITHUB REPOSITORY
= actual repository hosted on GitHub


REMOTE
= your local Git's reference to another repository


ORIGIN
= nickname you gave that remote


TOKEN
= proves you're allowed to access GitHub


MAIN
= branch containing your work


UPSTREAM
= remembers which remote branch your local branch normally
  pushes to / pulls from
```

---

#### Translate the commands into normal English

```bash
git remote add origin <GitHub URL>
```

means:

> **"Local Git, remember this GitHub repository and call it origin."**

---

```bash
git remote -v
```
means:

> **"Show me the remote repositories this local repo knows about."**

---

```bash
git push -u origin main
```
means:

> **"Send my local main branch to the GitHub repo called origin, and remember this as the normal relationship."**

---

```bash
git push
```

means:

> **"Send my new local commits to the GitHub branch you've already remembered."**

---

```bash
git pull
```

means:

> **"Bring down new work from the GitHub branch you've already remembered and integrate it into my local branch."**