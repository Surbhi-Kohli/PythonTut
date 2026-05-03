## Module and PIP in python

Module is like a code library which can be used to borrow code written by somebody else in our python program. 
There are two types of modules in python:

* **Built-in modules** - These modules are ready to import and use,shiped with the python interpreter. There is no need to install such modules explicitly. 
* **External modules** - These modules are imported from a third party file or can be installed using a package manager like pip or conda. Since this code is written by someone else, we can install different versions of a same module with time.


```
pip help
```
```
pip search Pympler
 // gives package  name and description

ERROR: XMLRPC request failed [code: -32500]
RuntimeError: PyPI no longer supports 'pip search' (or XML-RPC search). Please use https://pypi.org/search (via a browser) instead. See https://warehouse.pypa.io/api-reference/xml-rpc.html#deprecated-methods for more information.
(base) surbhikohli@SURKOHLI-M-9YXF ~ % 

pip install Pympler
pip install pandas
```

```pip list```  

<img width="254" alt="Screenshot 2024-08-31 at 5 37 10 PM" src="https://github.com/user-attachments/assets/8ae7cb4b-4a0b-404d-9701-37781fd21716">  


```pip uninstall Pympler```

## Using a module in Python (Usage)
We use the import syntax to import a module in Python. Here is an example code:
```
import pandas
# Read and work with a file named 'words.csv'
df = pandas.read_csv('words.csv')
print(df) # This will display first few rows from the words.csv file

``` 
How would you know if a package is outdated or latest?
```
pip list -o
```
To install updated version of a package

```pip install _u setuptools```  

what if u want to share the list of ur installed packages list to somoeone else?
```
pip freeze
pip freeze > requirements.txt
```
cat requirements.txt

Now u would share requirments file to someone, how would they install the packages using that file

```pip install -r requirements.txt```

```pip list --outdated```

To upgrade all packages, there is a suggestion by stack overflow that can be used 

## Using a built-in module
```
import pandas  # This is an example of external module
import hashlib  # This is an example of built in module

print("Hi")

# Dont worry about how to use these modules just yet!
pandas.read_csv("one.csv")
m = hashlib.sha256()

```
## pip Comes Bundled with Python

You don't need to install pip separately — it comes with Python (since Python 3.4).

```bash
pip --version
# or
python -m pip --version
```

| Situation | Fix |
|-----------|-----|
| System Python on Linux (Debian/Ubuntu) | `sudo apt install python3-pip` |
| Somehow missing | `python -m ensurepip` |

If you installed Python from python.org or via `brew` on Mac, pip is already there.

### Essential pip commands

```bash
pip install <package>       # install a package
pip uninstall <package>     # remove a package
pip list                    # show what's installed
pip show <package>          # details about one package
pip freeze                  # list installed with exact versions
pip install -r file.txt     # install from a file
pip --help                  # list all commands
pip install --help          # help for a specific command
```

---

## Installing with Extras: `pip install "fastapi[all]"`

The `[all]` is a **pip extras** specifier. It installs the package plus a named group of optional dependencies that the package author defined.

```bash
pip install fastapi              # just the core package
pip install "fastapi[all]"       # package + all optional extras
pip install "fastapi[standard]"  # package + standard extras only
pip install "celery[redis,msgpack]"  # multiple extras
```

### How authors define extras

In their `pyproject.toml`:

```toml
[project.optional-dependencies]
all = ["uvicorn", "jinja2", "python-multipart", "httpx", ...]
standard = ["uvicorn", "jinja2"]
dev = ["pytest", "ruff"]
```

The name `all` is just a convention — it's not special to pip. Authors can name extras anything.

### What `fastapi[all]` includes

| Package | Purpose |
|---------|---------|
| `uvicorn[standard]` | ASGI server |
| `jinja2` | Template rendering |
| `python-multipart` | Form/file upload parsing |
| `httpx` | Async HTTP client (for `TestClient`) |
| `email-validator` | Email field validation |
| `orjson` / `ujson` | Faster JSON serialization |

---

## `pyproject.toml` — The Modern Standard

`pyproject.toml` is the modern config file for Python projects, replacing the older `setup.py` and `setup.cfg` approach.

### What is TOML?

**Tom's Obvious Minimal Language** — a configuration file format (like JSON or YAML but designed to be human-friendly). It supports comments, is less ambiguous than YAML, and cleaner than JSON.

```toml
[project]
name = "my-app"
version = "1.0.0"
dependencies = [
    "fastapi>=0.100",
    "sqlalchemy>=2.0",
]

[project.optional-dependencies]
dev = ["pytest", "ruff"]

[tool.ruff]
line-length = 88
```

### `pyproject.toml` vs `requirements.txt`

| Approach | Use when |
|----------|----------|
| `pyproject.toml` | Building a package/project (recommended default) |
| `requirements.txt` | Quick scripts, legacy projects, or deployment-only pin files |

```bash
# With requirements.txt
pip install -r requirements.txt

# With pyproject.toml
pip install .          # installs the project + dependencies
pip install ".[dev]"   # includes dev extras
pip install -e .       # editable/development mode
```

---

## Pinned vs Unpinned Dependencies

### Pinned = exact version locked

```
fastapi==0.115.0       # pinned — always this exact version
sqlalchemy==2.0.35     # pinned
```

### Unpinned = flexible version range

```
fastapi>=0.100         # any version 0.100 or above
sqlalchemy             # any version at all
requests>=2.0,<3.0     # range constraint, but not exact
```

### When to use which

| Context | Approach |
|---------|----------|
| **Apps/deployments** | Pin everything (stability) |
| **Libraries** | Unpin (let the consumer resolve versions) |
| **Development** | Unpin in `pyproject.toml`, pin in lock file |

---

## The Reproducibility Problem

Sharing `pyproject.toml` alone doesn't guarantee everyone gets identical installs, because versions are unpinned:

```
You (today):     fastapi>=0.100  ->  resolves to 0.115.0
Teammate (next month):           ->  resolves to 0.116.2
```

### Solution: Lock files

A lock file pins **every** package (including transitive dependencies) to exact versions.

```bash
# Generate a lock file
pip freeze > requirements.txt           # simple way
pip-compile pyproject.toml -o requirements.lock  # better way (from pip-tools)

# Install from lock file — identical everywhere
pip install -r requirements.lock
```

(`-r` is short for `--requirement` — it just means "read packages from this file")

### `pip freeze` vs `pip-compile`

| | `pip freeze` | `pip-compile` |
|--|--|--|
| Pins everything | Yes | Yes |
| Needs extra tool | No (built into pip) | Yes (`pip install pip-tools`) |
| Shows where each dep came from | No — flat list | Yes — annotates with comments |

`pip-compile` output:

```
annotated-types==0.7.0    # via pydantic
anyio==4.6.0              # via starlette
fastapi==0.115.0          # via pyproject.toml
pydantic==2.9.2           # via fastapi
starlette==0.40.0         # via fastapi
```

This makes it clear which packages you can remove when you drop a dependency.

### Lock file tools

| Tool | Lock command | Lock file |
|------|-------------|-----------|
| `pip-tools` | `pip-compile` | `requirements.lock` |
| `poetry` | `poetry lock` | `poetry.lock` |
| `uv` | `uv lock` | `uv.lock` |

### The standard workflow

```
pyproject.toml          -> declare dependencies (checked into git)
        |
   lock file            -> pin exact versions (checked into git)
        |
pip install -r lock     -> reproducible install
```

---

## Transitive Dependencies

A **transitive dependency** is a dependency of your dependency.

```
You install:     fastapi
fastapi needs:   starlette, pydantic
pydantic needs:  pydantic-core, typing-extensions
```

```
Your code -> fastapi -> starlette
                     -> pydantic -> pydantic-core
                                 -> typing-extensions
```

- **Direct dependency**: `fastapi` (you asked for it)
- **Transitive dependencies**: everything else (pulled in automatically)

A lock file pins all of these — not just your direct dependencies.

---

## Why Python Can't Have Multiple Versions of the Same Package

### The flat namespace problem

```python
import requests   # which version? Python can only resolve ONE
```

Python looks up packages by name in `sys.path` and **stops at the first match**. There's no way to say:

```python
import requests v2.25 as old_requests   # NOT possible
import requests v2.31 as new_requests   # NOT possible
```

One name = one folder = one version. That's why pip overwrites the old version when you install a new one.

### The problem is at import time, not install time

You *could* technically store both versions on disk somewhere. But Python's import system has no mechanism to pick which version to use. So pip prevents the issue earlier by only keeping one version installed.

### How other languages handle this

| Language | Multiple versions? | How |
|--|--|--|
| **Python** | No | Single flat namespace, one lookup path |
| **Java** | Yes | Classloaders isolate namespaces — each module gets its own loader |
| **Go** | Yes | Import path includes version: `import "github.com/lib/foo/v2"` |
| **Rust** | Yes | Cargo allows version aliasing in `Cargo.toml` |
| **Node** | Partially | Nested `node_modules` can have different versions for sub-dependencies |

Java can have both because each classloader is like its own virtual environment running inside one process. Python's import system predates modern package management and was never redesigned for this.

### Python's solution

Instead of multiple versions in one environment, Python uses **virtual environments** — one version per environment, one environment per project.
