> [BACK](../README.md)

## Virtual Environment Walkthrough

#### Do Not Upload .venv to Git

Add this to .gitignore:

```
.venv/
```
> .gitignore is just a normal text file, but its job is to tell Git: <br>
> `Do not track these files or folders.`

The virtual environment can be recreated, so it normally should not be stored in Git.

Instead, Git should contain files such as:
```
my-project/
│
├── main.py
├── requirements.txt
├── README.md
└── .gitignore
```
Someone can then recreate the environment using:

```
python -m venv .venv
```

followed by:
```
python -m pip install -r requirements.txt
```

---

#### Create the Virtual Environment

First, navigate to the project folder:

```bash
cd path/to/my-project
```
Create the environment:

```bash
python -m venv .venv
```

This creates:

```text
my-project/
│
└── .venv/
```

> At this point the environment exists, but the terminal is not necessarily using it yet.

--- 

#### Activate the Environment

Git Bash - My set up
```bash
source .venv/Scripts/activate
```

Windows PowerShell
```bash
.venv\Scripts\Activate.ps1
```
Windows Command Prompt
```bash
.venv\Scripts\activate
```
macOS / Linux
```bash
source .venv/bin/activate
```

After activation, the terminal usually shows:
```text
(.venv)
```
before the command prompt.

---

#### What Activation Actually Does

Activating `.venv` does not turn global Python off.

Instead, it changes where that terminal looks first when commands such as these are used:


python <br>
pip

Before activation:
```text
python
   ↓
Global Python
```
After activation:

```text
python
   ↓
Project .venv Python
```
The same applies to pip.
```text
Terminal
   ↓
Activate .venv
   ↓
python / pip now point to .venv
```

#### Important

`Activation only affects the current terminal session.` <br>
If two terminals are open:

```
Terminal 1
└── .venv activated
    └── uses .venv Python

Terminal 2
└── not activated
    └── may still use global Python
```

Activating .venv in one terminal does not automatically change another terminal.

---

#### Check Which Python Is Being Used

A useful check is:

```bash
python -c "import sys; print(sys.executable)"
```
When .venv is active, the path should point somewhere inside:

```text
my-project/.venv/...
```
You can also check pip:
```
python -m pip --version
```
The displayed path should contain:
```text 
.venv
```
This confirms that packages will be installed into the virtual environment.

Also using `which` shows you the path:
```bash
which python 
which pip
```

---

#### Install Project Packages

When .venv is active:

```bash
python -m pip install pandas
```

installs pandas into:

```text
my-project/.venv/
```

rather than the global Python environment.

For several project dependencies, use:
```
python -m pip install -r requirements.txt
```

See the separate requirements.txt guide for:

* creating `requirements.txt`
* installing from it
* `pip freeze`
* viewing installed packages

---

#### Jupyter Is Separate From Terminal Activation

This is an important distinction.

Activating .venv changes the Python used by the terminal.

It does not automatically change the Python kernel being used by an already-open Jupyter notebook.

Think of them as two separate choices:
```text
Terminal environment
        │
        └── Which Python does the terminal use?

Jupyter kernel
        │
        └── Which Python runs notebook cells?
```
You want them both pointing to the same .venv.

---

#### Install `ipykernel`

Activate the environment first:

```bash
source .venv/Scripts/activate
```
Then install ipykernel inside it:
```bash
python -m pip install ipykernel
```
#### What is `ipykernel`?

ipykernel allows this Python environment to run code as a Jupyter kernel.

Without it, Jupyter may not be able to use the environment as a notebook kernel.

---

#### Register the .venv as a Jupyter Kernel

While the .venv is still active:

```bash
python -m ipykernel install --user --name project-venv --display-name "Project (.venv)"
```
Breakdown:
```
python -m ipykernel install
│
└── Run ipykernel using the currently active Python

--user
│
└── Register the kernel for the current user

--name project-venv
│
└── Internal name used by Jupyter

--display-name "Project (.venv)"
│
└── Friendly name shown in the Jupyter kernel menu
```

The `--name` should ideally be unique for each project. <br>
For example:
```bash
python -m ipykernel install --user --name finance-project --display-name "Finance Project (.venv)"
```
---

#### Select the Kernel

After registration, open the notebook and choose the new kernel.

For example:
```text
Select Kernel
    ↓
Finance Project (.venv)
```
Now:
```text
Notebook
    ↓
Finance Project (.venv)
    ↓
Python inside that project's .venv
```
This is what actually determines which Python runs notebook code.

---

#### Why Activating the Terminal Is Not Enough

Suppose the terminal has:

```text
(.venv)
```
That means:
```text
Terminal → .venv
```
But the notebook could still be using:
```text
Jupyter → Global Python
```
So this is possible:
```text
Terminal
└── .venv Python ✅

Jupyter Notebook
└── Global Python ❌

Selecting the correct kernel fixes this:

Terminal
└── .venv Python ✅

Jupyter Notebook
└── .venv Kernel ✅
```

---

#### Normal First-Time Setup

The full process for a new project is:

```text
Create project folder
        ↓
Create .venv
        ↓
Activate .venv
        ↓
Verify Python/pip point to .venv
        ↓
Install project requirements
        ↓
Install ipykernel
        ↓
Register/select .venv as Jupyter kernel
        ↓
Start working
```

Commands:
```bash
cd path/to/my-project

python -m venv .venv

source .venv/Scripts/activate

python -m pip install -r requirements.txt

python -m pip install ipykernel

python -m ipykernel install --user --name project-venv --display-name "Project (.venv)"
```

Then select:

```text
Project (.venv)
```
as the notebook kernel.

---

#### Normal Daily Use

Once the environment and kernel have already been created, you do not need to register the kernel again every day.

#### Using the terminal

Navigate to the project:

```bash
cd path/to/my-project
```
Activate:
```bash
source .venv/Scripts/activate
```
Then work normally.

#### Using Jupyter

Open the notebook and check that the correct kernel is selected:

```text
Project (.venv)
```

The kernel can use the .venv even if a separate terminal is not currently activated.

---

#### Deactivate the Terminal Environment

When finished:

```bash
deactivate
```
This returns the terminal to its normal Python environment.

It does not delete .venv.

---

#### Full Breakdown

Create the cheeky file
```bash
python -m venv .venv
```
Check the path:
```bash
which python
```

Turn it on - Using Gitbash
```bash
source .venv/Scripts/activate
```

Check the path for python and pip:
```bash
which python
```


Install while activate:
```text
python -m pip install <package_name>

or 

python -m pip install -r requirements.txt

If using requirements refer to requirements.md
```

Install Jupyter kernel support:
```bash 
python -m pip install ipykernel 
```

Register kernel 
```bash
python -m ipykernel install --user --name project-venv --display-name "Project (.venv)"
```
Deactivate

```bash 
deactivate
```

---

> [BACK](../README.md) 😮 [TOP](#virtual-environment-walkthrough)
