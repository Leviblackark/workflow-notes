# Mermaid CLI Usage Guide

## Overview

This guide explains how to **use Mermaid CLI after installation**.

The basic idea is:

1. Write a Mermaid diagram in a `.mmd` file
2. Convert it into an `.svg`
3. Display the SVG in Jupyter, Markdown, or a README

---

## Key files to know

### `.mmd`
A Mermaid source file.

This is the editable diagram file.

Example:

```text
flowchart LR
    A[Start] --> B[Finish]
```

### `.svg`
The rendered image output.

This is what gets displayed in notebooks and Markdown.

---

## Recommended folder structure

```text
your-project/
├── assets/
│   └── diagrams/
│       ├── workflow.mmd
│       └── workflow.svg
├── notebooks/
│   └── notes.ipynb
└── README.md
```

---

## The basic workflow

```text
Write Mermaid code
        ↓
Save as .mmd
        ↓
Run mmdc
        ↓
Generate .svg
        ↓
Display in notebook / README
```

---

## Step 1: Create or edit a Mermaid file

Example file:

```text
assets/diagrams/workflow.mmd
```

Example content:

```text
flowchart LR
    A[Download Data] --> B[Clean Data]
    B --> C[Analyse Data]
    C --> D[Visualise Results]
```

---

## Step 2: Generate the SVG

Run:

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

This converts:

```text
workflow.mmd
```

into:

```text
workflow.svg
```

---

## Step 3: Display the SVG

### In a README or Markdown file

```markdown
![Workflow](assets/diagrams/workflow.svg)
```

### In a notebook inside a `notebooks/` folder

```markdown
![Workflow](../assets/diagrams/workflow.svg)
```

---

## Command breakdown

The main command is:

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

### What each part means

| Part | Meaning |
|---|---|
| `mmdc` | Mermaid CLI command |
| `-i` | input file |
| `assets/diagrams/workflow.mmd` | the Mermaid source file |
| `-o` | output file |
| `assets/diagrams/workflow.svg` | the generated SVG image |

### In plain English

This command means:

> Take the Mermaid file `workflow.mmd` and generate an SVG image called `workflow.svg`.

---

## Example: building a simple flowchart

### Mermaid source (`workflow.mmd`)

```text
flowchart LR
    A[Start] --> B[Finish]
```

### Render command

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

### Result

```text
assets/
└── diagrams/
    ├── workflow.mmd
    └── workflow.svg
```

---

## Editing workflow

When you want to update a diagram:

1. Open the `.mmd` file
2. Edit the Mermaid code
3. Save the file
4. Run the same `mmdc` command again

The `.svg` file will be updated with the new version.

### Example

#### Updated `.mmd`

```text
flowchart LR
    A[Download Data]
    B[Clean Data]
    C[Analyse Data]
    D[Visualise Results]

    A --> B
    B --> C
    C --> D
```

#### Regenerate the SVG

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

---

## Why this method is useful

This method works well because:

- Mermaid stays editable as text
- SVG renders cleanly in Jupyter and Markdown
- one diagram can be reused in multiple places
- Git can track both the source and output

---

## Why keep both `.mmd` and `.svg`?

### Keep the `.mmd` because:
- it is the source file
- you can edit the diagram later

### Keep the `.svg` because:
- it displays easily in notebooks and Markdown
- GitHub renders it nicely
- other people can see the diagram without needing Mermaid installed

---

## Git workflow

When you create or update a diagram, Git will often show both files changed:

```text
modified: assets/diagrams/workflow.mmd
modified: assets/diagrams/workflow.svg
```

That is normal.

Add and commit both files:

```bash
git add assets/diagrams/
git commit -m "docs: add workflow diagram"
```

---

## Path tips

### If your notebook is in the root folder

Use:

```markdown
![Workflow](assets/diagrams/workflow.svg)
```

### If your notebook is inside `notebooks/`

Use:

```markdown
![Workflow](../assets/diagrams/workflow.svg)
```

### Why?

Because `..` means:

> go up one folder level

---

## Mermaid vs Markdown

### In a `.md` file
You can often write Mermaid directly like this:

```markdown
```mermaid
flowchart LR
    A[Start] --> B[Finish]
```
```

### In this workflow
You are instead doing:

```text
.mmd file
   ↓
render to .svg
   ↓
display image
```

This is often more reliable in Jupyter notebooks.

---

## Useful mental model

Think of it like this:

```text
Mermaid text = editable source
SVG image    = display output
```

or:

```text
workflow.mmd  →  workflow.svg
```

---

## Quick usage summary

### Create diagram source

```bash
touch assets/diagrams/workflow.mmd
```

### Render SVG

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

### Show it in Markdown

```markdown
![Workflow](assets/diagrams/workflow.svg)
```

or from a notebook in `notebooks/`:

```markdown
![Workflow](../assets/diagrams/workflow.svg)
```

---

## What to remember

- write Mermaid in a `.mmd` file
- use `mmdc` to generate the `.svg`
- display the `.svg` in Markdown or Jupyter
- update the `.svg` whenever the `.mmd` changes
- commit both files to Git

---

## Final workflow

```text
Create .mmd
    ↓
Write Mermaid code
    ↓
Run mmdc
    ↓
Generate .svg
    ↓
Display in notebook / README
    ↓
Commit both files
```