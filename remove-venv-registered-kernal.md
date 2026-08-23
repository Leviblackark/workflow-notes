#### If its kernel was registered, deleting .venv does not automatically unregister the kernel

Suppose you previously did:
```bash
python -m ipykernel install --user \
    --name finance-course \
    --display-name "Finance Course (.venv)"
```
Jupyter created a small kernel specification elsewhere on your computer.

Conceptually:
```text
Jupyter kernels
      │
      └── Finance Course (.venv)
                │
                └── points to
                    my-work-space/.venv/Scripts/python.exe
```
If you simply delete:
```text
my-work-space/.venv/
```

the Jupyter registration can remain:

```text
Jupyter
  ↓
Finance Course (.venv)
  ↓
❌ Python executable no longer exists
```

So you'll potentially still see the kernel listed in VS Code/Jupyter, but selecting it will fail.

> That's called a `stale kernelspec`.

---

#### Clean removal process

Before deleting the old environment, I would do this.

First activate it if appropriate and check whether there's anything installed that you want to remember:

```bash
source .venv/Scripts/activate
```
Then:
```bash
python -m pip list
```
or:
```bash
python -m pip freeze
```

If this environment belongs to a real Python project, make sure that project's `requirements.txt` contains the dependencies you care about.

Then deactivate:
```bash
deactivate
```

Next, see your registered Jupyter kernels:
```bash
jupyter kernelspec list
```

If jupyter isn't directly available but you have global Jupyter installed, you can also use:
```bash
py -m jupyter kernelspec list
```

You'll get something resembling:

Available kernels:
```text
  python3              ...
  finance-course       ...
  another-project      ...
```

If the old .venv corresponds to:
```text
finance-course
```

remove just that registration:
```bash
jupyter kernelspec uninstall finance-course
```
It will ask you to confirm.

Then you can delete the actual environment:
```bash
rm -rf .venv
```
--- 

###  Guide

```text
Check packages
      ↓
Make sure requirements are saved
      ↓
List registered kernels
      ↓
Unregister old .venv kernel
      ↓
Delete old .venv
```