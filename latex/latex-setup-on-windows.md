# LaTeX Setup Guide — Windows + VS Code

This guide documents the full LaTeX setup used on Windows with VS Code, including the programs installed, why they are needed, how they work together, and how the project files were organised.

---

## 1. What LaTeX Is

LaTeX is a **typesetting system** used to create professionally formatted documents.

It is especially useful for:

- mathematics
- statistics
- scientific writing
- research papers
- technical documentation
- reports containing equations

A LaTeX source file normally uses the extension:

```text
.tex
```

For example:

```text
01-latex-part-1.tex
```

The `.tex` file contains the instructions used to create the finished document.

A basic example:

```latex
\documentclass{article}

\begin{document}

Hello, LaTeX!

\[
E = mc^2
\]

\end{document}
```

LaTeX compiles this source code into a PDF.

---

# 2. LaTeX in Jupyter vs Full LaTeX

Jupyter Notebook already supports mathematical LaTeX inside Markdown cells.

For example:

```markdown
$R_t = \frac{P_t - P_{t-1}}{P_{t-1}}$
```

No separate LaTeX installation is required for this.

However, creating actual:

```text
.tex
```

files requires a full LaTeX installation.

Therefore there are two different setups:

```text
.ipynb Markdown
      ↓
LaTeX maths rendering
      ↓
No MiKTeX required
```

versus:

```text
.tex
      ↓
Full LaTeX document
      ↓
LaTeX compiler required
      ↓
PDF
```

---

# 3. Software Installed

The complete Windows setup consists of:

```text
VS Code
   ↓
LaTeX Workshop
   ↓
latexmk
   ↓
Perl
   ↓
MiKTeX / pdflatex
   ↓
PDF
```

Each component has a different job.

---

## 4. VS Code

VS Code is the editor used to write the `.tex` files.

It does **not** contain LaTeX itself.

It provides the environment in which the files are edited.

Example:

```text
01-latex-part-1.tex
```

---

# 5. LaTeX Workshop

Installed from the VS Code Extensions marketplace.

Extension:

```text
LaTeX Workshop
Publisher: James Yu
```

### Why it is needed

LaTeX Workshop connects VS Code to the LaTeX tools installed on Windows.

It provides features such as:

- compiling `.tex` files
- displaying the resulting PDF
- LaTeX syntax highlighting
- autocomplete
- error messages
- build commands
- PDF/source synchronisation

LaTeX Workshop is **not itself the LaTeX compiler**.

It controls the compiler installed separately on Windows.

---

# 6. MiKTeX

MiKTeX was installed separately from VS Code.

MiKTeX provides the actual LaTeX system on Windows.

During installation:

```text
Install MiKTeX only for me
```

was selected.

The following settings were used:

```text
Preferred paper: A4

Install missing packages on-the-fly: Yes
```

### Why A4?

A4 is the standard paper size used in the UK.

### Why automatically install missing packages?

LaTeX has thousands of optional packages.

If a document contains something such as:

```latex
\usepackage{amsmath}
```

MiKTeX can automatically obtain the required package if it is not already installed.

---

# 7. Testing MiKTeX

After installing MiKTeX, VS Code was completely restarted.

This is important because VS Code terminals that were already running may still contain the old Windows `PATH`.

MiKTeX was tested from Git Bash using:

```bash
pdflatex --version
```

A successful installation returned something similar to:

```text
MiKTeX-pdfTeX
```

This confirmed that Windows and Git Bash could locate the LaTeX compiler.

The executable can also be located using:

```bash
where.exe pdflatex
```

---

# 8. Understanding PATH

Windows uses an environment variable called:

```text
PATH
```

to locate installed programs.

When the command:

```bash
pdflatex
```

is entered, Windows searches the directories listed in `PATH` for:

```text
pdflatex.exe
```

MiKTeX normally adds its executable directory to PATH during installation.

This is why restarting VS Code after installing command-line software is often necessary.

---

# 9. latexmk

LaTeX Workshop attempted to compile the document using:

```text
latexmk
```

but initially returned:

```text
'latexmk' is not recognized
```

or:

```text
spawn latexmk ENOENT
```

This meant LaTeX Workshop was trying to use `latexmk`, but it was not yet available.

---

## Installing latexmk

MiKTeX Console was opened.

Under:

```text
Packages
```

the following package was searched for:

```text
latexmk
```

Only the main package was required:

```text
latexmk
```

The following were not necessary:

```text
latexmk__doc
latexmk__source
```

After installation, VS Code was restarted.

The installation was tested with:

```bash
latexmk --version
```

A successful result displayed the installed `latexmk` version.

---

# 10. Why latexmk Is Useful

A LaTeX document sometimes needs to be compiled more than once.

For example:

```text
references
citations
bibliographies
cross-references
table of contents
```

may require multiple compilation passes.

Instead of manually running:

```text
pdflatex
pdflatex
pdflatex
```

`latexmk` determines what needs to be run automatically.

Therefore:

```text
latexmk
```

acts as a build manager for LaTeX.

---

# 11. Strawberry Perl

After installing `latexmk`, another error appeared:

```text
MiKTeX could not find the script engine 'perl'
```

This happened because `latexmk` is written in **Perl**.

Windows does not normally include Perl by default.

Therefore an additional Perl installation was required.

---

## Installing Strawberry Perl

The Windows distribution used was:

```text
Strawberry Perl
```

The normal:

```text
64-bit MSI installer
```

was selected.

The default installation directory was kept:

```text
C:\Strawberry\
```

The MSI installer was preferred over:

```text
Portable ZIP
PDL ZIP
```

because a normal Windows installation automatically configures the environment correctly.

After installation, VS Code was completely restarted.

Perl was tested with:

```bash
perl --version
```

If version information appears, Windows can locate Perl.

`latexmk` was then tested again:

```bash
latexmk --version
```

---

# 12. Complete Windows LaTeX Toolchain

The final working setup is:

```text
.tex source file
       ↓
VS Code
       ↓
LaTeX Workshop
       ↓
latexmk
       ↓
Strawberry Perl
       ↓
MiKTeX
       ↓
pdflatex
       ↓
PDF
```

The important distinction is:

```text
VS Code
= editor
```

```text
LaTeX Workshop
= VS Code integration
```

```text
latexmk
= automatic build manager
```

```text
Perl
= script engine required by latexmk
```

```text
MiKTeX
= LaTeX installation/package system
```

```text
pdflatex
= compiler that turns .tex into PDF
```

---

# 13. Building a LaTeX File in VS Code

A basic `.tex` file:

```latex
\documentclass{article}

\begin{document}

Hello, LaTeX!

\[
E = mc^2
\]

\end{document}
```

Save the file.

Then build it using:

```text
Ctrl + Alt + B
```

LaTeX Workshop will compile the document.

---

# 14. Files LaTeX Creates

Originally, compiling:

```text
hello.tex
```

produced several files:

```text
hello.tex
hello.pdf
hello.aux
hello.fdb_latexmk
hello.fls
hello.log
hello.synctex.gz
```

These files have different purposes.

```text
hello.tex
```

is the source file written manually.

```text
hello.pdf
```

is the compiled document.

Files such as:

```text
.aux
.log
.fls
.fdb_latexmk
.synctex.gz
```

are generated automatically during compilation.

These normally do not need to be edited manually.

---

# 15. Keeping LaTeX Build Files Organised

Allowing all the generated files to sit beside the `.tex` file quickly becomes messy.

Therefore LaTeX Workshop was configured to place generated files inside a dedicated:

```text
build/
```

directory.

---

## VS Code Setting

Open:

```text
VS Code
→ Settings
```

Search for:

```text
latex outdir
```

Find:

```text
LaTeX-workshop › LaTeX: Out Dir
```

Set it to:

```text
%DIR%/build
```

### What `%DIR%` Means

`%DIR%` means:

> the directory containing the main `.tex` file.

Therefore:

```text
latex/
└── 01-latex-part-1.tex
```

compiles into:

```text
latex/
├── 01-latex-part-1.tex
│
└── build/
    ├── 01-latex-part-1.pdf
    ├── 01-latex-part-1.aux
    ├── 01-latex-part-1.log
    ├── 01-latex-part-1.fls
    ├── 01-latex-part-1.fdb_latexmk
    └── 01-latex-part-1.synctex.gz
```

This keeps the working directory much cleaner.

---

# 16. Recommended Folder Structure

The LaTeX files were organised into their own directory.

Example:

```text
quantitative-foundations/
│
├── latex/
│   ├── 01-latex-part-1.tex
│   ├── 02-latex-part-2.tex
│   ├── 03-latex-part-3.tex
│   ├── latex.ipynb
│   │
│   └── build/
│       ├── PDFs
│       ├── logs
│       └── temporary LaTeX files
│
├── .gitignore
├── .gitattributes
├── README.md
├── LICENSE
└── requirements.txt
```

The important separation is:

```text
.tex
.ipynb
```

are source/learning files that are maintained manually.

Whereas:

```text
build/
```

contains files generated automatically.

---

# 17. Organising Existing Files with Git Bash

From the repository root:

```bash
pwd
```

Check Git status:

```bash
git status --short
```

Create the LaTeX and build directories:

```bash
mkdir -p latex/build
```

Move the manually created files:

```bash
mv hello.tex latex/
mv latex.ipynb latex/
```

Because these files were still untracked at the time, normal:

```bash
mv
```

was appropriate.

If Git had already been tracking them, using:

```bash
git mv
```

would have made the intention clearer to Git.

---

# 18. Removing Old Generated Files

The old build files that were created in the repository root could safely be removed.

For example:

```bash
rm -f hello.aux hello.fdb_latexmk hello.fls hello.log hello.pdf hello.synctex.gz
```

These files can always be recreated by compiling the `.tex` source again.

The important file is:

```text
hello.tex
```

---

# 19. Updating `.gitignore`

The build directory should not normally be tracked by Git.

Add:

```gitignore
# LaTeX build output
latex/build/
```

This means Git will ignore all files generated inside:

```text
latex/build/
```

without needing to list every LaTeX extension individually.

For example, this avoids having to write:

```gitignore
*.aux
*.log
*.fls
*.fdb_latexmk
*.synctex.gz
```

Using the build directory keeps the rule much cleaner.

---

# 20. Why the Build Folder Is Ignored

The contents of:

```text
build/
```

can be regenerated from the `.tex` source.

Therefore Git generally needs to track:

```text
01-latex-part-1.tex
02-latex-part-2.tex
03-latex-part-3.tex
```

but does not need to track:

```text
.aux
.log
.fls
.synctex.gz
.fdb_latexmk
```

The principle is:

```text
SOURCE FILES
↓
Track with Git
```

```text
GENERATED BUILD FILES
↓
Ignore with Git
```

---

# 21. Checking Git Afterwards

After reorganising:

```bash
git status --short
```

The temporary LaTeX files inside:

```text
latex/build/
```

should no longer appear.

The actual source files should still appear if they have not yet been committed.

---

# 22. Committing the Setup

Once everything is organised:

```bash
git add -A
```

Check:

```bash
git status
```

Then commit:

```bash
git commit -m "Organise LaTeX learning files"
```

---

# 23. Normal LaTeX Workflow

After the initial setup, most of the installation details can be forgotten.

The normal workflow is simply:

```text
1. Open or create a .tex file
        ↓
2. Write LaTeX
        ↓
3. Save
        ↓
4. Ctrl + Alt + B
        ↓
5. LaTeX Workshop runs latexmk
        ↓
6. latexmk uses MiKTeX
        ↓
7. PDF appears inside build/
        ↓
8. View the PDF
        ↓
9. Edit the .tex file and repeat
```

---

# 24. Files to Pay Attention To

Most of the time, only two things matter:

```text
document.tex
```

This is the source file being written.

and:

```text
build/document.pdf
```

This is the finished output.

The other build files can normally be ignored.

The exception is:

```text
.log
```

which can be useful when diagnosing compilation errors.

---

# 25. Useful Commands

Check MiKTeX / pdfLaTeX:

```bash
pdflatex --version
```

Find the executable:

```bash
where.exe pdflatex
```

Check `latexmk`:

```bash
latexmk --version
```

Find `latexmk`:

```bash
where.exe latexmk
```

Check Perl:

```bash
perl --version
```

Check Git changes:

```bash
git status --short
```

Compile directly without VS Code:

```bash
pdflatex document.tex
```

Normally, however, LaTeX Workshop can handle compilation using:

```text
Ctrl + Alt + B
```

---

# 26. Troubleshooting

## `pdflatex: command not found`

Usually means Windows or the current terminal cannot locate MiKTeX.

First completely restart VS Code.

Then test:

```bash
where.exe pdflatex
```

---

## `spawn latexmk ENOENT`

Means LaTeX Workshop cannot find:

```text
latexmk
```

Check:

```bash
latexmk --version
```

If unavailable, install the `latexmk` package through MiKTeX Console.

---

## `MiKTeX could not find the script engine 'perl'`

Means `latexmk` exists but Perl is unavailable.

Install Strawberry Perl and restart VS Code.

Then test:

```bash
perl --version
```

---

## `Cannot find LaTeX root file`

Make sure the `.tex` file itself has focus before building.

The file should normally contain something such as:

```latex
\documentclass{article}
```

and:

```latex
\begin{document}

...

\end{document}
```

Then build from the `.tex` editor.

---

# 27. Final Setup Summary

The completed Windows LaTeX environment is:

```text
Windows
│
├── VS Code
│   └── LaTeX Workshop
│
├── MiKTeX
│   ├── pdflatex
│   └── latexmk package
│
└── Strawberry Perl
    └── Perl interpreter used by latexmk
```

Project layout:

```text
project/
│
├── latex/
│   ├── source.tex
│   └── build/
│
└── .gitignore
```

VS Code setting:

```text
LaTeX-workshop › LaTeX: Out Dir
```

set to:

```text
%DIR%/build
```

Git ignore rule:

```gitignore
# LaTeX build output
latex/build/
```

The main rule to remember is:

```text
.tex
= source code
= write/edit/commit
```

```text
build/
= generated output
= normally leave alone
= don't commit
```

Once this setup is complete, normal LaTeX work should require very little tooling management.