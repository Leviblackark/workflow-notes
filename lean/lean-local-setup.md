### Work Flow

#### Starting Lean - Research
From the LEAN workspace:

```bash
cd ~/path/to/lean-workspace
```
Start Research:
```bash
lean research "project-name"
```
If using VS Code and you do not want LEAN to automatically open JupyterLab in the browser:

```bash 
lean research "project-name" --no-open
```

If port 8888 is already busy, use another port:
```bash
lean research "test-project" --no-open --port 8890
```

`CTRL + c` - stops the container. Don’t use `docker stop <container_name>`; you will override the default shutdown.

---

#### Folder layout 
So instead of this:
```text
lean-workspace/
└── .git/              ← one repo for everything
```

you’d do this:
```text
lean-workspace/
├── project-one/
│   └── .git/          ← repo just for this project
│
├── project-two/
│   └── .git/          ← separate repo
│
└── project-three/
    └── .git/           ← separate repo
```

---

#### What Happens When lean research Runs?

The flow is:
```text
lean research "project-name"
             ↓
LEAN CLI talks to Docker
             ↓
Docker starts the LEAN Research image
             ↓
Your project folder is mounted into the container
             ↓
Jupyter runs inside the container
             ↓
Notebook code uses LEAN's Python environment
```
The notebook is not using your normal global Python.

It is also not using your project's `.venv`.

> It is using Python inside the LEAN Docker environment.

---

### LEAN Research vs Normal Jupyter

One of the most important differences.

#### Normal Jupyter Project

You might create:

```text
.venv
   ↓
install ipykernel
   ↓
register kernel
   ↓
select Project (.venv)

For example:

python -m venv .venv
source .venv/Scripts/activate
python -m pip install ipykernel
```

That is correct for an ordinary local Python/Jupyter project.


#### LEAN Research

You normally do not create and register your own .venv kernel.

Instead:

```text
lean research
      ↓
Docker starts Jupyter
      ↓
VS Code connects to that Jupyter server
      ↓
LEAN Docker kernel runs the notebook
```
In VS Code:

```text
Select Kernel
    ↓
Existing Jupyter Server
    ↓
http://localhost:8888/
    ↓
Select the LEAN / Foundation Python kernel
```
Therefore:

Ordinary project → select .venv kernel

LEAN Research     → connect to LEAN Docker Jupyter kernel

----