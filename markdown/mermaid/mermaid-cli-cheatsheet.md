# Mermaid CLI Cheat Sheet

Quick reference for creating and rendering Mermaid diagrams with **Mermaid CLI**.

---

## Check Installation

```bash
node --version
npm --version
mmdc --version
```

If all three return version numbers, Mermaid CLI is ready to use.

---

## Install Mermaid CLI

```bash
npm install -g @mermaid-js/mermaid-cli
```

Check installation:

```bash
mmdc --version
```

---

## Create Diagram Folder

```bash
mkdir -p assets/diagrams
```

Recommended structure:

```text
project/
├── assets/
│   └── diagrams/
├── notebooks/
└── README.md
```

---

## Create a Mermaid File

```bash
touch assets/diagrams/workflow.mmd
```

Example `workflow.mmd`:

```text
flowchart LR
    A[Start] --> B[Finish]
```

> `.mmd` files contain Mermaid code directly.  
> Do not include Markdown ` ```mermaid ` fences.

---

## Render Mermaid → SVG

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

### Command Breakdown

| Part | Meaning |
|---|---|
| `mmdc` | Run Mermaid CLI |
| `-i` | Input |
| `workflow.mmd` | Mermaid source |
| `-o` | Output |
| `workflow.svg` | Generated image |

Think:

```text
mmdc -i INPUT -o OUTPUT
```

or:

```text
workflow.mmd → workflow.svg
```

---

## Display SVG in Markdown

If the Markdown file is in the project root:

```markdown
![Workflow](assets/diagrams/workflow.svg)
```

---

## Display SVG in Jupyter

If the notebook is inside:

```text
notebooks/
```

use:

```markdown
![Workflow](../assets/diagrams/workflow.svg)
```

`..` means:

> Go up one directory.

---

## Update a Diagram

1. Edit the `.mmd` file
2. Save it
3. Run `mmdc` again

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

The existing SVG will be regenerated.

---

## Typical Workflow

```text
Edit .mmd
    ↓
Save
    ↓
Run mmdc
    ↓
Generate .svg
    ↓
View in Markdown / Jupyter
```

---

## Keep Both Files

```text
assets/
└── diagrams/
    ├── workflow.mmd
    └── workflow.svg
```

### `.mmd`

Editable Mermaid source.

### `.svg`

Rendered diagram used in Markdown, Jupyter, and GitHub.

---

## Git

Check changes:

```bash
git status
```

Add diagrams:

```bash
git add assets/diagrams/
```

Commit:

```bash
git commit -m "docs: add workflow diagram"
```

Usually commit **both** the `.mmd` and `.svg`.

---

## Useful Mermaid Examples

### Left → Right

```text
flowchart LR
    A[Start] --> B[Finish]
```

### Top → Bottom

```text
flowchart TD
    A[Start]
    B[Process]
    C[Finish]

    A --> B
    B --> C
```

### Branching

```text
flowchart TD
    A[Start] --> B{Condition}

    B -->|Yes| C[Continue]
    B -->|No| D[Stop]
```

---

## Direction Codes

| Code | Direction |
|---|---|
| `LR` | Left → Right |
| `RL` | Right → Left |
| `TD` | Top → Bottom |
| `BT` | Bottom → Top |

Example:

```text
flowchart LR
```

---

## Main Commands

```bash
# Check Mermaid
mmdc --version

# Create folder
mkdir -p assets/diagrams

# Create source file
touch assets/diagrams/workflow.mmd

# Render SVG
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

---

## Mental Model

```text
Mermaid code
     ↓
    .mmd
     ↓
    mmdc
     ↓
    .svg
     ↓
README / Markdown / Jupyter
```

---

## Remember

> `.mmd` = source  
> `.svg` = rendered output  
> `mmdc -i INPUT -o OUTPUT` = convert between them