### lean library add
##### Packages Already Included With LEAN

The official LEAN Docker environment already contains many common Python libraries.

For example, commonly used libraries may already be available.

So first try:

```text
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
If a package is already part of the LEAN environment, you do not need to install another copy just because you would normally install it into a `.venv`.

---

#### Adding a Package the LEAN Way

When a LEAN project needs an additional third-party Python package, use:

```bash
lean library add "project-name" package-name
```
For example:

```bash
lean library add "project-name" statsmodels
```
or:

```bash
lean library add "project-name" altair
```
LEAN then manages that library as a dependency of the project.

Add specific version:
```bash
lean library add "project-name" package-name --version VERSION
```
---

#### What lean library add Actually Does

For a Python project:

```bash
lean library add
        ↓
checks package compatibility
        ↓
adds package to project's requirements.txt
        ↓
makes it available to the LEAN project
```
For example:

```bash
lean library add "project-name" altair
```

may result in something like:

```
project-name/
│
├── main.py
├── research.ipynb
└── requirements.txt
```

with:
```
altair==x.x.x
```
inside requirements.txt.

This means the project records:<br>
`This LEAN project depends on this package.`

---

### `requirements.txt` in LEAN

This is still a normal Python `requirements.txt` file.

However, the workflow is slightly different.

#### Ordinary Python project

You might manually create:

```text
requirements.txt
```
and then run:

```bash
python -m pip install -r requirements.txt
```

which installs those packages into the currently selected Python environment, usually `.venv`.

### LEAN project

Prefer:

```text
lean library add "project-name" package-name
````

LEAN adds the package to the project's:

```
requirements.txt
```

and handles the dependency for the LEAN environment.

So you generally do not need to manually enter the Docker container and run `pip install`.

---

#### The Extra Local Installation

There is one part of `lean library add` that can initially be confusing.

By default, LEAN may also install the package into your local computer's Python environment.

Why?

For things such as:

```text
VS Code
   ↓
Pylance
   ↓
autocomplete / type information
```

This local installation is primarily there to help your editor understand the package.

It is not the Python environment executing the LEAN Research notebook.

Think of it as:

```text
lean library add
      │
      ├──────────────→ LEAN project dependency
      │                requirements.txt
      │                used by LEAN
      │
      └──────────────→ local Python copy
                       autocomplete/editor support
```

These serve different purposes.

---
#### Is That Local Installation Isolated Like .venv?

Not automatically.

`lean library add` does not create a `.venv` for you.

The local autocomplete installation uses the local Python environment available to the CLI.

Therefore, do not think:

```text
lean library add
        =
create isolated .venv
```
It does not.

The actual LEAN execution environment is isolated because Docker is running it.

---

#### Avoid the Local Installation With --no-local

If you only want to add the dependency to the LEAN project and do not want LEAN modifying your host Python environment:

```bash
lean library add "project-name" package-name --no-local
```
For example:
```bash
lean library add "project-name" statsmodels --no-local
```
This means roughly:

Add it to LEAN project ✅<br>
Install local autocomplete copy ❌

The project dependency is still recorded.

The downside is that local VS Code autocomplete for that third-party package may be less complete unless your editor has another environment containing it.

---
### Removing a LEAN Package

Use:
```bash
lean library remove "project-name" package-name
```
For example:
```bash
lean library remove "project-name" altair
```
LEAN removes the dependency from the project configuration / `requirements.txt`.

---

### Clarification on a few points

`lean library add` is doing two jobs at once, while `.venv` and `--no-local` concern a different part of the setup

Metal model:

```text
                    LEAN PROJECT
                        │
             lean library add pandas
                        │
             ┌──────────┴──────────┐
             ↓                     ↓
   requirements.txt         Local Python copy
             │                     │
             ↓                     ↓
      LEAN / Docker          VS Code autocomplete
      actually runs it       editing convenience
```

`lean library add` adds the package to the project's `requirements.txt`, and unless `--no-local` is specified, it also installs the package into the local Python environment so your editor can provide autocomplete.

In VS Code, Pylance can show you the function parameters and documentation.

That's autocomplete / IntelliSense. <br>
It gives you things like:

* suggestions while typing
* function parameters
* hover documentation
* import recognition
* fewer "import could not be resolved" warnings

---

#### What --no-local means

Normally:

```bash
lean library add "my-project" some-package
```
does approximately this:

```
1. Check for a LEAN-compatible version

2. Add it to:
   my-project/requirements.txt

3. Install a copy into local Python
   for autocomplete
```
If instead you do:

```bash
lean library add "my-project" some-package --no-local
``` 
you are saying:

```text
Do step 1 ✅
Do step 2 ✅
Skip step 3 ❌
```
QuantConnect describes `--no-local` as "Skip making changes to your local environment."

```text
lean library add package --no-local
             │
             ↓
requirements.txt ✅
             │
             ↓
LEAN Docker can use dependency ✅

Local Python installation ❌
             │
             ↓
Local autocomplete may be reduced
```

---

#### The important .venv distinction

When you do:
```bash
python -m venv .venv
```
you deliberately create an isolated Python environment.

Then:
```bash
source .venv/Scripts/activate
```

makes that terminal use:

```text
.venv Python
.venv pip
.venv packages
```

So:
```bash
python -m pip install pandas
```

goes into:

```text
my-project/
└── .venv/
    └── pandas etc.
```
That's nice and controlled.

--- 

When you run:
```bash
lean library add "my-project" pandas
```

LEAN does not create an isolated `.venv`.

The official docs say that if `pip` is available on your PATH, LEAN installs the autocomplete copy into your local Python environment.

Without a virtual environment, you can think of it roughly as:

```text
lean library add
      │
      ├── requirements.txt
      │       ↓
      │    Docker
      │    isolated ✅
      │
      └── Local Python
              ↓
           potentially global
```
So the LEAN execution side is isolated.

The optional autocomplete installation isn't automatically isolated.

---

#### My Choice ,`.venv` for editor + Docker for LEAN

You keep these concepts deliberately separate:
```text
LEAN Workspace
│
├── .venv/
│      │
│      └── LOCAL ONLY
│          VS Code autocomplete
│          local Python tooling
│
├── project/
│      ├── main.py
│      ├── research.ipynb
│      └── requirements.txt
│
└── Docker
       │
       └── ACTUAL LEAN EXECUTION
```
Now you get isolation on both sides:
```text
HOST SIDE                         LEAN SIDE


.venv                             Docker
  ↓                                  ↓
VS Code / autocomplete            Research
local tooling                     Backtests
                                     ↓
                                  requirements.txt
```
But here's the really important point:

> The .venv still does not run LEAN.

You're only using it to keep the local/editor side clean.

Docker remains the actual LEAN runtime. lean research itself runs JupyterLab in QuantConnect's research Docker container.

---

#### What could be done

I would not create a `.venv` inside every LEAN project because LEAN needs one.

LEAN doesn't.

Instead, I'd think of the workspace like this:
```text
lean-workspace/
│
├── .venv/                   ← optional LOCAL tooling environment
│
├── project-one/
│   ├── main.py
│   ├── research.ipynb
│   └── requirements.txt     ← LEAN dependencies
│
├── project-two/
│   └── ...
│
└── data/
```
And of course:
```text
.venv/
```

The .venv is not part of your algorithm.

It's just:

> A clean place for local Python/editor packages to live.

---

#### `Problem 2` I guess

The important thing is that a `.venv` does not have to be a Jupyter kernel to be useful. In a LEAN project, you can use the `.venv` purely as the local Python environment that VS Code/Pylance looks at for autocomplete, while the actual notebook code continues to run inside the LEAN Docker kernel.

So you can deliberately have this setup:

```text
                    VS CODE
                       │
            ┌──────────┴──────────┐
            ↓                     ↓
     EDITING / PYLANCE        RUNNING CODE
            ↓                     ↓
          .venv              LEAN Docker
            ↓                     ↓
       autocomplete          Jupyter kernel
```

Those two environments have different jobs.

You need to actually activate the environment:
```bash
source .venv/Scripts/activate
```
Then verify:
```bash
python -c "import sys; print(sys.executable)"
```
You want something containing:
```bash
lean-workspace/.venv/Scripts/python.exe
```
and:
```bash
python -m pip --version
```
should also show a path inside .venv.

Activation changes the terminal's PATH, so the .venv versions of Python and pip are found first.

Then `lean library add`

Suppose you've activated:

```text
lean-workspace/.venv
```
and run:

```bash
lean library add "my-project" statsmodels
```
Two relevant things happen for a Python library:
```text
lean library add
        │
        ├── adds statsmodels to:
        │
        │   my-project/requirements.txt
        │
        │        ↓
        │   used by LEAN
        │
        └── installs a local copy
             using pip on PATH
             ↓
          your active .venv
```

hat local installation is specifically there to provide autocomplete.

So your `.venv` might now contain:

```text
lean-workspace/
│
├── .venv/
│   └── statsmodels        ← local/editor copy
│
└── my-project/
    ├── main.py
    ├── research.ipynb
    └── requirements.txt   ← LEAN dependency

And this is the key:

You do NOT need to register that .venv as a Jupyter kernel for LEAN Research.

That's where your normal .venv workflow and your LEAN workflow split apart.
```

---

#### In a normal Python project

Your `.venv` does everything:
```text
.venv
 │
 ├── packages
 ├── VS Code autocomplete
 │
 └── Jupyter execution
       ↑
   ipykernel

So you install:
python -m pip install ipykernel

register it:
python -m ipykernel install ...

and choose it as the notebook kernel.
```

---

In a LEAN project

You don't need that last part.

Your `.venv` can simply be:

```text
.venv
 │
 └── local packages
        ↓
   VS Code / Pylance
   autocomplete only
```
While:
```text
LEAN Docker
     │
     └── Jupyter kernel
             ↓
        actually runs
        research.ipynb
```
`lean research` runs JupyterLab inside the QuantConnect Research Docker container.

So do not register/select the `.venv` as your LEAN Research notebook kernel just because you've installed the autocomplete packages there.

---

# How does VS Code know to use .venv for autocomplete?

> VS Code has a Python interpreter selection, which is separate from a Jupyter notebook's kernel selection.

In VS Code:

```text
Ctrl + Shift + P
```
search:
```text
Python: Select Interpreter
```
Then select something like:
```text
.venv\Scripts\python.exe
```

Now Pylance can inspect the packages installed in `.venv`.

For example, you've installed:

```text
statsmodels
```
into `.venv`. 

You type:

```python
import statsmodels.api as sm

sm.
```
Pylance can look inside your .venv and provide suggestions.

But when you press Run Cell in your LEAN Research notebook:

```text
Run Cell
   ↓
LEAN Jupyter kernel
   ↓
Docker
```
not:
```text
Run Cell
   ↓
.venv
```
```text
PYTHON INTERPRETER
        ↓
.venv
        ↓
Used locally by VS Code/Pylance
for autocomplete and analysis


JUPYTER KERNEL
        ↓
LEAN Research server
        ↓
Docker
        ↓
Actually executes notebook code
```

They do not need to be the same Python environment.

That's different from your ordinary Python/Jupyter projects, where it's generally convenient for both to point to `.venv`.

---

#### Quick set up
```text
                  lean library add
                         │
             ┌───────────┴───────────┐
             ↓                       ↓
project/requirements.txt           .venv
             ↓                       ↓
       LEAN Docker             VS Code/Pylance
             ↓                       ↓
       RUNS the code              autocomplete
```

When you're going to add a new library and want autocomplete:
```bash
cd path/to/lean-workspace
source .venv/Scripts/activate
```
Verify:
```bash
python -m pip --version
```
Then:
```bash
lean library add "project-one" statsmodels
```

In VS Code:
```text
Ctrl + Shift + P
```
search:
```text
Python: Select Interpreter
```
Then select something like:
```text
.venv\Scripts\python.exe
```

---

Things to look into: 
1. If changing the isolated environment affects the current autocomplete. Is it using Global in which case this works and if not then boom I guess. 