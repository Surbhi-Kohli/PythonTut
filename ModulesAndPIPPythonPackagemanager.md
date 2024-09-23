We can have 2 types of modules:
**Built-in modules** - Shipped with Python,you dont need to install these
**External modules** - Installed with the help of PIP.

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
```

```pip list```
<img width="254" alt="Screenshot 2024-08-31 at 5 37 10 PM" src="https://github.com/user-attachments/assets/8ae7cb4b-4a0b-404d-9701-37781fd21716">

```pip uninstall Pympler```

How would you know if a package is outdated or latest?
pip list -o

To install updated version of a package
```pip install _u setuptools```
what if u want to share the list of ur installed packages list to somoeone else?

pip freeze
pip freeze > requirements.txt

cat requirements.txt
Now u would share requirments file to someone, how would they install the packages using that file

```pip install -r requirements.txt```

```pip list --outdated```

To upgrade all packages, there is a suggestion by stack overflow that can be used 
