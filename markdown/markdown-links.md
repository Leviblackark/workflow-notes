# Markdown Links

Markdown links allow you to make text clickable.

They can be used to link to:

- websites
- other Markdown files
- folders and files in a repository
- sections within the same document
- sections inside another Markdown document

---

## Basic Link Syntax

The basic structure is:

```text
[Text to display](destination)
```

For example:

```markdown
[GitHub](https://github.com)
```

This displays as:

[GitHub](https://github.com)

The text inside:

```text
[ ]
```

is what the reader sees.

The destination inside:

```text
( )
```

is where the link goes.

A useful way to remember it is:

```text
[What the reader sees](Where the reader goes)
```

---

## Linking to a Website

Use the full website address as the destination.

```markdown
[Python Documentation](https://docs.python.org/3/)
```

You can make the visible text anything you want:

```markdown
[Read the official Python documentation](https://docs.python.org/3/)
```

This is usually cleaner than placing a long URL directly into your notes.

---

## Linking to Another File

Markdown files can link directly to other files.

Suppose your repository contains:

```text
workflow-notes/
├── README.md
└── markdown/
    ├── markdown-links.md
    ├── markdown-lists.md
    └── markdown-tables.md
```

From `README.md`, you could link to the tables guide with:

```markdown
[Markdown Tables](markdown/markdown-tables.md)
```

This is called a **relative link**.

It tells Markdown where the file is located relative to the file you are currently in.

---

## Relative Links

Relative links are very useful in GitHub repositories because they do not depend on the full GitHub website address.

For example:

```markdown
[Markdown Lists](markdown/markdown-lists.md)
```

is better than writing a long GitHub URL to the same file.

If the repository is moved, cloned, or renamed, the relative link can still work because it describes the file's location inside the repository.

---

## Linking to a File in the Same Folder

Suppose both files are here:

```text
markdown/
├── markdown-links.md
└── markdown-tables.md
```

Inside `markdown-links.md`, you can write:

```markdown
[Markdown Tables](markdown-tables.md)
```

Because both files are already in the same directory, you only need the filename.

---

## Linking to a Subfolder

Suppose you are in:

```text
README.md
```

and want to reach:

```text
markdown/markdown-links.md
```

Use:

```markdown
[Markdown Links](markdown/markdown-links.md)
```

Think of `/` as:

> Go inside this folder.

So:

```text
markdown/markdown-links.md
```

means:

```text
go into markdown/
        ↓
open markdown-links.md
```

---

## Going Back Up a Folder

Use:

```text
../
```

to move up one directory.

Suppose you are currently inside:

```text
markdown/markdown-links.md
```

and want to link back to:

```text
README.md
```

Your structure is:

```text
workflow-notes/
├── README.md
└── markdown/
    └── markdown-links.md
```

Use:

```markdown
[Back to README](../README.md)
```

The:

```text
../
```

means:

> Go up one folder.

You can think of it like:

```text
markdown-links.md
       ↓
      ../
       ↓
workflow-notes/
       ↓
   README.md
```

---

## Linking to a Heading

You can also link directly to a section of a Markdown document.

Suppose the document contains:

```markdown
## Relative Links
```

You can link to it with:

```markdown
[Go to Relative Links](#relative-links)
```

The `#` tells Markdown that you are linking to a heading in the current document.

---

## How Heading Links Are Created

A heading such as:

```markdown
## Basic Link Syntax
```

normally becomes:

```text
#basic-link-syntax
```

The heading is generally:

```text
Basic Link Syntax
```

and the link becomes:

```text
basic-link-syntax
```

So:

```markdown
[Jump to Basic Link Syntax](#basic-link-syntax)
```

will jump to that section.

Spaces normally become:

```text
-
```

and capital letters are normally treated as lowercase.

---

## Linking to a Heading in Another File

You can combine a file link and a heading link.

For example:

```markdown
[Go to Task Lists](markdown-lists.md#task-lists)
```

This means:

```text
markdown-lists.md
        +
   #task-lists
        ↓
Open that file directly at the Task Lists section.
```

This can be very useful when creating documentation.

---

## Creating a Contents Section

Links to headings can be used to create a table of contents.

For example:

```markdown
## Contents

- [Basic Link Syntax](#basic-link-syntax)
- [Linking to a Website](#linking-to-a-website)
- [Relative Links](#relative-links)
- [Linking to a Heading](#linking-to-a-heading)
```

Clicking one of the links jumps directly to that section.

This is particularly useful for longer Markdown files.

---

## Example: Connecting Documentation

Suppose your repository contains:

```text
workflow-notes/
│
├── README.md
│
└── markdown/
    ├── markdown-links.md
    ├── markdown-lists.md
    ├── markdown-tables.md
    └── markdown-mermaid-diagrams.md
```

Your main `README.md` could contain:

```markdown
## Markdown Guides

- [Markdown Links](markdown/markdown-links.md)
- [Markdown Lists](markdown/markdown-lists.md)
- [Markdown Tables](markdown/markdown-tables.md)
- [Mermaid Diagrams](markdown/markdown-mermaid-diagrams.md)
```

Now the README acts like a navigation page for the rest of your notes.

---

## Relative Link Mental Model

Think of relative links like navigating folders in the terminal.

```text
folder/file.md
```

means:

```text
go into folder
↓
open file.md
```

While:

```text
../file.md
```

means:

```text
go back one folder
↓
open file.md
```

This is very similar to navigating directories from the command line.

---

## Quick Reference

| Syntax | Meaning |
|---|---|
| `[Text](URL)` | Link to a website |
| `[Text](file.md)` | Link to a file in the same folder |
| `[Text](folder/file.md)` | Link to a file inside another folder |
| `[Text](../file.md)` | Go up one folder and open a file |
| `[Text](#heading)` | Link to a heading in the current file |
| `[Text](file.md#heading)` | Link to a heading in another file |

---

## Basic Templates

### Website

```markdown
[Link Name](https://example.com)
```

### File

```markdown
[File Name](file.md)
```

### File Inside a Folder

```markdown
[File Name](folder/file.md)
```

### Back One Folder

```markdown
[Back](../README.md)
```

### Heading

```markdown
[Section Name](#section-name)
```

### Heading in Another File

```markdown
[Section Name](file.md#section-name)
```

---

## Tips

Use descriptive link text rather than writing things such as:

```markdown
[Click here](...)
```

It is usually clearer to write:

```markdown
[Markdown Tables Guide](markdown-tables.md)
```

Relative links are usually the best choice when connecting files inside the same Git repository.

After moving or renaming a file, check any Markdown links pointing to it because the path may also need updating.