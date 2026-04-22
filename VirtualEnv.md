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
What does activation mean: "Activating" a virtual environment just means reconfiguring your current shell session to use the venv's Python and packages instead of the system ones. That's all it is.
activation is just a convenience so you don't have to type full paths like:
```
bash
# Without activation — works, but tedious
/Users/surbhikohli/MyPersonal/fastapi/venv/bin/python app/main.py
/Users/surbhikohli/MyPersonal/fastapi/venv/bin/pip install fastapi
 
# With activation — same thing, just shorter
python app/main.py
pip install fastapi
```
And deactivate (line 4–32 of the same file) just undoes all of this — restores the old PATH, old prompt, and removes VIRTUAL_ENV.

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


<img width="820" alt="Screenshot 2024-08-31 at 9 17 16 PM" src="https://github.com/user-attachments/assets/5d61a3fb-f398-4b31-893d-b50b71615097">  

#### Why We Need to Restart with the source Command:   
When you create a virtual environment, you need to "activate" it to use it. The source command is used to run the activation script.

#### What Happens When You Run source?
Modifies Environment Variables: Running the source command modifies the shell's environment variables, particularly the PATH variable, to prioritize the Python interpreter and libraries of the virtual environment over the system-wide ones. This ensures that when you run python or pip, it uses the versions from the virtual environment.

* Sets the Shell Context: The command changes the shell context so that all subsequent commands will be executed within the virtual environment. It essentially "tells" your terminal to use the isolated environment you've created.

* Updates the Prompt: Often, activating a virtual environment also updates the terminal prompt (e.g., (venv)) to indicate that you are working inside a virtual environment.

What Does <virtualenv>/bin/activate Represent?
<virtualenv>: This is a placeholder for the directory where your virtual environment is located. When you create a virtual environment, you typically specify a directory name for it. For example, if you created a virtual environment named myenv, then <virtualenv> would be myenv.

bin/activate:

bin: This is a subdirectory inside the virtual environment directory. On Unix-like systems (Linux and macOS), the bin directory contains executable files, including the Python interpreter and scripts needed to manage the environment.
activate: This is the script that is used to activate the virtual environment. Running this script with the source command sets up your shell to use the virtual environment's Python interpreter and libraries.



## To get out of ur virtual env
```deactivate```

To delete
``` rm -rm project1_env```

```vitualenv -p /usr/bin/python2.6(python version) <projectname>```
The environments that we have here are only meant for ur dependencies and packages and not for the actual project files . You should not build ur project files within the virtual env

## Newer version:
what is python -m venv ./venv    doing

```python -m venv ./venv```
 creates a Python virtual environment in a folder called venv in the current directory.

Breaking it down:

* python — invokes the Python interpreter
* -m venv — runs the built-in venv module as a script (-m means "run this module")
* ./venv — the target directory where the virtual environment will be created

#### What it actually creates
A ./venv folder containing:

  * Its own Python binary (a copy/symlink of the system Python)
  * Its own pip
  * An isolated site-packages directory for installing packages without affecting the global Python installation

Why use it  
It isolates your project's dependencies so that packages installed for one project don't conflict with another. After creating it, you activate it with:
```source ./venv/bin/activate   # macOS/Linux```
Once activated, pip install commands install packages only into that virtual environment.

### virtualenv vs venv
virtualenv is a third-party package (installed via pip install virtualenv) that predates Python's built-in venv. It's faster, supports older Python versions (like 2.6/2.7), and has more features — but both serve the same core purpose: isolating project dependencies.
