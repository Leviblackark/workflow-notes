# README Guide

A `README.md` explains what a repository or folder contains and how it should be used.

It is usually the first thing someone sees when opening a GitHub repository.

---

## Main Repository README

The root `README.md` should explain the project as a whole.

Example structure:

```markdown
# Project Name

Short description of what this repository is for.

## Purpose

Explain the main goal of the project.

## Contents

- `folder-1/` — description
- `folder-2/` — description
- `folder-3/` — description

## Tools

- Python
- LaTeX
- Jupyter
- Git

## Notes

Any useful information about how the repository is organised or used.
```

---

## Folder-Level README

It is perfectly fine to have additional `README.md` files inside folders.

Example:

```text
project/
├── README.md
│
├── maths/
│   └── README.md
│
└── research/
    └── README.md
```

The root README explains the whole repository.

A folder-level README explains only that section.

Example:

```markdown
# Folder Name

Brief description of what this folder contains.

## Purpose

Explain why this section exists.

## Contents

- `file-1.ext` — description
- `file-2.ext` — description
- `subfolder/` — description

## Notes

Any important information about working with the files in this folder.
```

---

## Recommended Hierarchy

```text
README.md
    ↓
Explains the whole repository

folder/README.md
    ↓
Explains that specific folder

subfolder/README.md
    ↓
Explains that specific subsection
```

Only add another README when a folder contains enough material that it benefits from its own explanation.

---

## Good README Habits

- Keep the title clear.
- Explain the purpose early.
- Describe important folders and files.
- Use headings to keep information organised.
- Keep descriptions concise.
- Update the README when the structure changes.
- Avoid documenting information that is obvious from the filename alone.
- Write for someone who has never seen the project before.

---

## Simple Template

```markdown
# Name

Short description.

## Purpose

What this project or folder is for.

## Contents

- `example/` — description
- `example.ext` — description

## Tools

- Tool 1
- Tool 2

## Notes

Anything else worth knowing.
```

The main rule is:

```text
README.md
= orientation and explanation

Project files
= the actual work
```