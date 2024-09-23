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
