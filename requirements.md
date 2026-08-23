## requirements.txt 

Option 1 - Flow

```text
NEW PROJECT

Create .venv
    ↓
Activate .venv
    ↓
Create requirements.txt
    ↓
List direct packages
    ↓
python -m pip install -r requirements.txt
    ↓
Connect .venv to Jupyter if needed
```
Option 2 - Flow

```
EXPERIMENTAL PROJECT

Create + activate .venv
    ↓
Install packages as needed
    ↓
python -m pip list
    ↓
Write important packages into requirements.txt
             OR
pip freeze > requirements.txt
```

---
#### What is a `requirments.txt` file
It lists the Python libraries your project needs, one per line. 


Example: 

```text
Pandas
numpy
matplotlib 
```
It allows the same project environment to be recreated later.

---
#### Quick setup

Create an environment:

```bash
python -m venv .venv
```
Activate it in Git Bash:
```bash
source .venv/Scripts/activate
```

Check which Python is being used:
```
which python
```
Then install everything listed in requirements.txt:
```
python -m pip install -r requirements.txt
```

---
#### Quick Setup Flow
```text
Create .venv
    ↓
Activate .venv
    ↓
Install requirements.txt
    ↓
Packages are installed into .venv
```
---

#### `Method 1` — Write requirements.txt first

Create - `requirements.txt`

Manually add the packages your project needs:
```text
pandas
numpy
matplotlib
yfinance
```
Then:
```bash
python -m pip install -r requirements.txt
```

This gives you:
```
requirements.txt
        ↓
pip installs packages
        ↓
.venv
```
---

#### `Method 2` — Install packages first

Sometimes you're experimenting and don't know what you'll need yet.

Activate the environment:
```bash
source .venv/Scripts/activate
```
Then install normally:
```bash
python -m pip install pandas
python -m pip install numpy
python -m pip install matplotlib
```
To see what's currently installed:
```bash
python -m pip list
```
You'll get something along the lines of:
```
Package       Version
------------- -------
matplotlib    3.x.x
numpy         2.x.x
pandas        2.x.x
pip           xx.x
...
```
#### Then you have two choices

1. Keep requirements.txt simple

Manually write the important libraries:
```
pandas
numpy
matplotlib
```
Generally recommend while you're learning.

#### Or 
generate it automatically
```bash
python -m pip freeze > requirements.txt
```

This might produce:
```text
contourpy==1.3.3
cycler==0.12.1
fonttools==4.59.0
matplotlib==3.10.5
numpy==2.3.2
pandas==2.3.1
python-dateutil==2.9.0.post0
...
```

Notice how there's suddenly a lot more stuff.

That's because pip freeze records packages that your packages depend on too, not just the ones you personally installed.

For example:

```
You install:
matplotlib
     ↓
matplotlib needs:
numpy
pillow
cycler
fonttools
...
```
So `pip freeze` records the whole environment.

---

#### Useful inspection commands

I'd definitely keep this tiny section because it'll answer the exact question you just had.

```bash
# Show installed packages
python -m pip list

# Show exact installed versions
python -m pip freeze

# Information about one package
python -m pip show pandas
```
And a really useful check:
```bash
python -m pip --version
```
It will show a path. If your `.venv` is active, you should see something referring to your project environment, such as:

`...\work-flow\.venv\Lib\site-packages\pip`

That tells you where pip is actually installing things.

---

#### Jupyter Notebook

```text
Terminal .venv          Jupyter
     │                      │
     └──── ipykernel ───────┘
                ↓
       Select .venv kernel
```
If the notebook has the `.venv` kernel selected, I recommend installing from inside the notebook with:
```bash
%pip install pandas
```
or:
```bash
%pip install -r requirements.txt
```
`%pip` is useful because Jupyter installs into the environment associated with the current notebook kernel.