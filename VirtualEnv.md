## 1. Why Virtual Environments Exist

Every Python project depends on packages (Flask, Django, pandas, etc.). Without isolation, all projects share one global set of packages. The problem:

- Project A needs `pandas==1.5`, Project B needs `pandas==2.0`
- Upgrading globally for one project breaks the other
- Installing packages globally may require admin/root permissions

A **virtual environment** solves this by giving each project its own isolated folder of dependencies and a dedicated Python binary. You can install, upgrade, or remove packages in one project without affecting anything else.

---


## Why Do We Need virtualenv in Python
* Isolated Environment: A virtualenv (short for "virtual environment") creates an isolated environment for Python projects. This means that each project can have its own dependencies (libraries, modules, etc.), independent of other projects and the system-wide Python installation. This isolation helps avoid conflicts between packages and their versions when multiple projects are being developed simultaneously.

* Version Control: Different projects may require different versions of the same package. For example, one project may need Django 3.2 while another may require Django 4.0. By using virtual environments, you can manage different package versions for different projects without conflict.

* Avoiding Permission Issues: Installing packages globally (at the system level) may require administrative or root permissions. Virtual environments allow you to install packages locally for a specific project without needing special permissions.


## 2. `venv` vs `virtualenv`

| Feature              | `venv`                        | `virtualenv`                     |
|----------------------|-------------------------------|----------------------------------|
| Install needed?      | No — built into Python 3.3+   | Yes — `pip install virtualenv`   |
| Python 2 support     | No                            | Yes                              |
| Speed                | Slightly slower               | Faster (caches packages)         |
| Features             | Basic, sufficient             | More flags and options           |
| **Recommendation**   | **Use this by default**       | Only if you need Python 2        |

---
## 3. The Full Workflow (End to End)

### Step 1: Create the environment (2 ways)
```bash
# Using venv (recommended)
python -m venv ./venv
#   python           — invokes the Python interpreter
#   -m venv          — runs the built-in venv module as a script
#   ./venv           — target directory name (convention, not required)

# Using virtualenv (alternative)
pip install virtualenv                       # one-time install
virtualenv project1_env                      # create environment
virtualenv -p /usr/bin/python2.6 myproject   # with a specific Python version
```

This creates a folder containing its own Python binary, its own `pip`, and an isolated `site-packages/` directory.

We can make a couple of virtual environments. For that we will create an Environments folder

```
   mkdir Environments
   cd Environments
   virtualenv project1_env # first environment
```
### Step 2: Activate the environment

| OS                       | Command                          |
|--------------------------|----------------------------------|
| **macOS / Linux**        | `source venv/bin/activate`       |
| **Windows (cmd)**        | `venv\Scripts\activate.bat`      |
| **Windows (PowerShell)** | `venv\Scripts\Activate.ps1`      |

After activation your prompt changes to **show the env name**, and `python`/`pip` now point to the venv's copies:
<img width="617" alt="Screenshot 2024-08-31 at 9 03 36 PM" src="https://github.com/user-attachments/assets/cdc49fb2-4e29-488d-911c-1ff603048295"> 

```bash
which python
# /Users/surbhikohli/Environments/project1_env/bin/python  (inside venv, not system)
```

### Step 3: Install packages

```bash
pip install fastapi                    # install a package
pip install "fastapi[all]"             # install with all optional extras
pip install "fastapi[standard]"        # install with standard extras
pip install -r requirements.txt        # install from a saved requirements file
```

> **zsh note:** Square brackets `[]` are glob patterns in zsh. Always quote them: `"fastapi[all]"` not `fastapi[all]`.


When u run ```pip list``` u see packages only within ur environment: 
<img width="696" alt="Screenshot 2024-08-31 at 9 05 26 PM" src="https://github.com/user-attachments/assets/d4ff9a53-4d37-4edc-8a03-700e697d892e">  

### Step 4: Work on your project

```
my_project/
├── app/                  <- your code lives here
│   └── main.py
├── requirements.txt      <- dependency list
├── venv/                 <- virtual env (gitignored, disposable)
│   ├── bin/
│   ├── lib/
│   └── ...
```

**Important:** Never put your project files inside the `venv/` folder. The venv is disposable — you should be able to delete it and recreate it anytime from `requirements.txt`. The environment is only for dependencies and packages, not for actual project files.

### Step 5: Save dependencies

```bash
pip list                                   # human-readable table of installed pkgs
pip freeze                                 # machine-readable format (pkg==1.2.3)
pip freeze --local > requirements.txt      # save venv-local deps to file --local adds only the dependencies that are local to ur virtaul env in the requirement.txt file  
```
<img width="820" alt="Screenshot 2024-08-31 at 9 17 16 PM" src="https://github.com/user-attachments/assets/5d61a3fb-f398-4b31-893d-b50b71615097">  

`pip freeze` vs `pip freeze --local` — only matters if you created your venv with `--system-site-packages`:

| Command              | Standard venv      | `--system-site-packages` venv |
|----------------------|--------------------|-------------------------------|
| `pip freeze`         | Venv packages only | Venv + global packages        |
| `pip freeze --local` | Venv packages only | **Only** venv packages        |

For standard venvs both give the same output. `--local` is a good habit.

### Step 6: Deactivate when done

```bash
deactivate
```

Restores your original `PATH`, prompt, and removes the `VIRTUAL_ENV` variable.

### Deleting an environment

```bash
rm -rf project1_env
```

Since a venv is just a folder, deleting it is all you need. Recreate anytime from `requirements.txt`.
### Cheat sheet

```bash
python -m venv venv                        # 1. Create  (once per project)
source venv/bin/activate                   # 2. Activate (every terminal session)
pip install -r requirements.txt            # 3. Install  (once, or after git pull)
# ... work ...
pip freeze --local > requirements.txt      # 4. Save     (after adding new packages)
deactivate                                 # 5. Done for the day
```

---
# Part 2: Deeper Knowledge

## 4. What Activation Actually Does Under the Hood

Activation is **not** starting a process or booting anything."Activating" a virtual environment just means reconfiguring your current shell session to use the venv's Python and packages instead of the system ones. It reconfigures your current shell session by doing three things:

1. **Changes `PATH`** — Prepends `venv/bin/` so `python` and `pip` resolve to the venv's copies first
2. **Sets `VIRTUAL_ENV` variable** — Points to the venv directory; tools use this to detect the active venv
3. **Updates your prompt** — Adds `(venv)` as a visual indicator

It is purely a convenience so you don't have to type full paths:

```bash
# Without activation — works, but tedious
/Users/surbhikohli/MyPersonal/fastapi/venv/bin/python app/main.py
/Users/surbhikohli/MyPersonal/fastapi/venv/bin/pip install fastapi

# With activation — same thing, just shorter
python app/main.py
pip install fastapi
```
And deactivate  just undoes all of this — restores the old PATH, old prompt, and removes VIRTUAL_ENV.
### Why `source` specifically?

`source` is a **shell built-in** that runs a script **in your current shell session**. Without it, the script runs in a child process and all environment changes (PATH, etc.) vanish when that subprocess exits.

```bash
source venv/bin/activate   # changes stick in your current terminal
sh venv/bin/activate       # changes happen in a subprocess and vanish
```

### About the `bin/activate` file

- Located at `venv/bin/activate` — no file extension, which is common for Unix scripts meant to be sourced
- Variants exist for other shells: `activate.csh`, `activate.fish`, `Activate.ps1`
- On Unix, file extensions are optional — the OS doesn't use them to determine how to run a file

---
## 5 What is `--system-site-packages`?

By default, a venv is **fully isolated** — it can only see packages you install inside it. If you create the venv with this flag, it **also** gets access to your global/system Python packages:

```bash
python -m venv --system-site-packages ./venv
```

```
Standard venv (default):
  venv sees:       [venv packages only]
  system packages:  invisible

--system-site-packages venv:
  venv sees:       [venv packages] + [global/system packages]
  system packages:  visible as a fallback
```

**When would you use it?**
- A large package (like `numpy` or `torch`) is installed globally and you don't want to re-download it into every venv
- You're on a system where certain packages are installed via the OS package manager (e.g., `apt install python3-xyz` on Ubuntu)

**The catch:** This is exactly why `pip freeze --local` exists. Without `--local`, your `requirements.txt` gets bloated with global packages you didn't explicitly install for this project. Most people don't use this flag — full isolation (the default) is cleaner and avoids surprises.

---

## 6. What's Inside the Environment Folder

### Symlink vs Copy

| Component              | Symlink or Copy?   | Why                                        |
|------------------------|--------------------|--------------------------------------------|
| **Python binary**      | Symlink (shortcut) | Same interpreter, no need to duplicate     |
| **Installed packages** | Separate copies    | Isolation — the whole point of a venv      |

A **symlink** is a shortcut pointing to the original file. A **copy** is a fully independent duplicate.

```bash
ls -la venv/bin/python3
# Output with -> means it's a symlink:
# venv/bin/python3 -> ~/.pyenv/versions/3.12.4/bin/python3
```

Packages are always independent copies per environment, even if the same package exists globally. Different venvs can have different versions of the same package.

---

## 7. `source` vs `sh` 

| Command    | What it is             | Purpose                                          |
|------------|------------------------|--------------------------------------------------|
| `source`   | Shell built-in         | Runs a script in your **current** shell session  |
| `sh`       | Bourne Shell           | A shell interpreter / runs scripts in a **subprocess** |

### Shell family tree

| Shell   | Full Name          | Notes                                  |
|---------|--------------------|----------------------------------------|
| `sh`    | Bourne Shell       | Original Unix shell (1979), minimal    |
| `bash`  | Bourne Again Shell | Upgraded `sh`, default on most Linux   |
| `zsh`   | Z Shell            | Further upgraded, **default on macOS** |

---

## 8. Glob Patterns

A glob pattern is wildcard syntax for matching file/directory names. Relevant because pip extras use `[]` syntax and `.gitignore` uses globs.

| Pattern   | Matches                          | Example                         |
|-----------|----------------------------------|---------------------------------|
| `*`       | Any characters (one level)       | `*.py` matches `main.py`       |
| `?`       | Exactly one character            | `file?.txt` matches `file1.txt`|
| `**`      | Any number of directories        | `**/*.py` matches all `.py` files recursively |
| `[abc]`   | One character in the set         | `file[12].txt` matches `file1.txt` |
| `[!abc]`  | One character NOT in the set     | `file[!1].txt` matches `file2.txt` |

Used in: shell commands, `.gitignore`, Python's `glob` module.

---





#### What Happens When You Run source?
Modifies Environment Variables: Running the source command modifies the shell's environment variables, particularly the PATH variable, to prioritize the Python interpreter and libraries of the virtual environment over the system-wide ones. This ensures that when you run python or pip, it uses the versions from the virtual environment.

* Sets the Shell Context: The command changes the shell context so that all subsequent commands will be executed within the virtual environment. It essentially "tells" your terminal to use the isolated environment you've created.

* Updates the Prompt: Often, activating a virtual environment also updates the terminal prompt (e.g., (venv)) to indicate that you are working inside a virtual environment.

What Does <virtualenv>/bin/activate Represent?
<virtualenv>: This is a placeholder for the directory where your virtual environment is located. When you create a virtual environment, you typically specify a directory name for it. For example, if you created a virtual environment named myenv, then <virtualenv> would be myenv.

bin/activate:

bin: This is a subdirectory inside the virtual environment directory. On Unix-like systems (Linux and macOS), the bin directory contains executable files, including the Python interpreter and scripts needed to manage the environment.
activate: This is the script that is used to activate the virtual environment. Running this script with the source command sets up your shell to use the virtual environment's Python interpreter and libraries.






