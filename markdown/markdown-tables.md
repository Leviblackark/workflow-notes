> [BACK](../README.md)

# Markdown Tables

Markdown tables are useful for displaying information in a structured way using **rows and columns**.

They work well for:

- comparisons
- quick-reference guides
- definitions
- commands and explanations
- features
- organised notes

---

## Basic Table Structure

A Markdown table is created using:

- `|` to separate columns
- `-` to create the header divider

Example:

```markdown
| Name | Description |
|---|---|
| Item A | First item |
| Item B | Second item |
```

This renders as:

| Name | Description |
|---|---|
| Item A | First item |
| Item B | Second item |

---

## How It Works

The first row contains the **column headings**:

```text
| Name | Description |
```

The second row separates the headings from the table contents:

```text
|---|---|
```

The remaining rows contain the data:

```text
| Item A | First item |
| Item B | Second item |
```

---

## Adding More Columns

Add another section separated with `|`.

```markdown
| Name | Type | Description |
|---|---|---|
| Item A | Example | First item |
| Item B | Example | Second item |
```

Which produces:

| Name | Type | Description |
|---|---|---|
| Item A | Example | First item |
| Item B | Example | Second item |

---

## Column Alignment

You can control how text is aligned using `:` in the header divider.

### Left aligned

```text
|:---|
```

### Centred

```text
|:---:|
```

### Right aligned

```text
|---:|
```

Example:

```markdown
| Left | Centre | Right |
|:---|:---:|---:|
| A | B | C |
| 1 | 2 | 3 |
```

Result:

| Left | Centre | Right |
|:---|:---:|---:|
| A | B | C |
| 1 | 2 | 3 |

---

## Formatting Inside Tables

Normal Markdown formatting can often be used inside table cells.

### Bold

```markdown
| Command | Meaning |
|---|---|
| **Start** | Begins the process |
```

### Inline Code

Use backticks:

```markdown
| Command | Meaning |
|---|---|
| `example` | Example command |
```

Result:

| Command | Meaning |
|---|---|
| `example` | Example command |

---

## Using the Pipe Character Inside a Table

The `|` character normally separates columns.

If you need to display a literal pipe character inside a cell, escape it with a backslash:

```text
\|
```

Example:

```markdown
| Symbol | Meaning |
|---|---|
| `\|` | Pipe character |
```

---

## Keeping Tables Readable

Markdown does not require all columns to have exactly the same width.

This works:

```markdown
| Name | Description |
|---|---|
| A | First example |
| B | Second example |
```

You can also space things out:

```markdown
| Name   | Description    |
|--------|----------------|
| A      | First example  |
| B      | Second example |
```

Both render the same way.

Use whichever version is easier for you to read while editing.

---

## Good Example for Notes

Tables are useful for quick-reference information.

```markdown
| Symbol | Meaning | Example |
|---|---|---|
| `>` | Greater than | `10 > 5` |
| `<` | Less than | `5 < 10` |
| `=` | Equal to | `x = 10` |
```

Result:

| Symbol | Meaning | Example |
|---|---|---|
| `>` | Greater than | `10 > 5` |
| `<` | Less than | `5 < 10` |
| `=` | Equal to | `x = 10` |

---

## Table vs List

Use a **table** when several items share the same categories.

For example:

```text
Command | Purpose | Example
```

Use a **list** when the information does not naturally fit into columns.

Example:

```markdown
- First step
- Second step
- Third step
```

A good rule is:

> Use tables for comparison and structured reference information.  
> Use lists for steps, ideas, and simple collections of information.

---

## Quick Reference

| Syntax | Purpose |
|---|---|
| `|` | Separates columns |
| `---` | Creates the header divider |
| `:---` | Left align |
| `:---:` | Centre align |
| `---:` | Right align |
| `\|` | Display a pipe character |
| `` `text` `` | Inline code |
| `**text**` | Bold text |

---

## Basic Template

Copy this when starting a new table:

```markdown
| Heading 1 | Heading 2 | Heading 3 |
|---|---|---|
| Value | Value | Value |
| Value | Value | Value |
```

---

## Tips

- Keep headings short where possible.
- Avoid putting very large paragraphs inside tables.
- Use inline code for commands, filenames, or syntax.
- Use tables when they make information easier to scan.
- If a table starts becoming difficult to read, consider using headings and bullet points instead.

> [BACK](../README.md) 😮 [TOP](#markdown-tables)