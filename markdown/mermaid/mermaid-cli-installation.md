# Mermaid CLI Installation Guide

## Overview

This guide shows how to install **Mermaid CLI** on Windows using **VS Code** and **Git Bash**.

Mermaid CLI lets you turn Mermaid diagram files such as:

```text
flowchart LR
    A[Start] --> B[Finish]
```

into image files such as **SVG** that can be used in:

- Jupyter notebooks
- Markdown notes
- GitHub READMEs

---

## What gets installed

When setting this up, the main pieces are:

```text
Node.js
└── npm
    └── Mermaid CLI
        └── mmdc
```

### What each one does

- **Node.js** → the runtime needed to run JavaScript tools
- **npm** → Node's package manager
- **Mermaid CLI** → the tool that converts Mermaid diagrams into images
- **mmdc** → the command you actually run in the terminal

---

## Step 1: Check if Node.js is already installed

Open a terminal in **Git Bash** or **PowerShell** and run:

```bash
node --version
npm --version
```

### Expected result

You should see version numbers, for example:

```text
v24.19.0
11.17.0
```

If you instead see something like:

```text
bash: node: command not found
bash: npm: command not found
```

then Node.js is not installed yet.

---

## Step 2: Install Node.js

If Node.js is not installed, use this command in **PowerShell**:

```powershell
winget install OpenJS.NodeJS.LTS
```

### Notes

- This installs **Node.js**
- **npm** comes with Node.js automatically
- You do **not** need to install npm separately

After installation finishes:

1. Close VS Code completely
2. Reopen VS Code
3. Open a fresh terminal

Then check again:

```bash
node --version
npm --version
```

---

## Step 3: Install Mermaid CLI

Once `node` and `npm` are working, install Mermaid CLI globally:

```bash
npm install -g @mermaid-js/mermaid-cli
```

### Why `-g`?

The `-g` means **global** install.

That makes the Mermaid command available from any project on your machine.

---

## Step 4: Verify the installation

Check that Mermaid CLI was installed correctly:

```bash
mmdc --version
```

### Expected result

You should see a version number, for example:

```text
11.17.0
```

If that appears, the installation worked.

---

## Step 5: Create a diagrams folder in your project

From the root of your project, create a folder for Mermaid diagram files:

```bash
mkdir -p assets/diagrams
```

This gives you a clean structure such as:

```text
your-project/
├── assets/
│   └── diagrams/
├── notebooks/
└── README.md
```

---

## Step 6: Create your first Mermaid file

Create a Mermaid source file:

```bash
touch assets/diagrams/workflow.mmd
```

Open the file and add:

```text
flowchart LR
    A[Start] --> B[Finish]
```

### Important

Inside a `.mmd` file, you do **not** write:

```markdown
```mermaid
...
```
```

You only write the Mermaid diagram itself.

---

## Step 7: Convert the Mermaid file into an SVG

Run:

```bash
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

If successful, you should now have:

```text
assets/
└── diagrams/
    ├── workflow.mmd
    └── workflow.svg
```

---

## Step 8: Use the SVG in Markdown or Jupyter

### In a Markdown file

```markdown
![Workflow](assets/diagrams/workflow.svg)
```

### In a notebook Markdown cell

If your notebook is inside a `notebooks/` folder:

```markdown
![Workflow](../assets/diagrams/workflow.svg)
```

---

## Common installation notes

### `npm notice New major version available`
You can ignore this if everything works.

### `packages are looking for funding`
This is informational only. No action needed.

### `allow-scripts` warning
If Mermaid successfully creates the SVG, you usually do **not** need to change anything.

---

## Quick install summary

```bash
node --version
npm --version
npm install -g @mermaid-js/mermaid-cli
mmdc --version
mkdir -p assets/diagrams
touch assets/diagrams/workflow.mmd
mmdc -i assets/diagrams/workflow.mmd -o assets/diagrams/workflow.svg
```

---

## Result

You now have a working Mermaid setup where:

```text
workflow.mmd
     ↓
    mmdc
     ↓
workflow.svg
```

That SVG can be reused in:

- Jupyter notebooks
- Markdown notes
- GitHub README files