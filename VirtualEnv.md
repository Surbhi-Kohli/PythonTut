
Virtual env is a way in which u can separate different python environments for different projects.
Why would u want to do something like this? eg say u have multiple projects that all rely on single package like flask or django. Each of these projects might be using different version of django or flask.
If u go and upgrade the version in ur global packages, it might break a couple of projects.It would be better if each of the projects had isolated environments where they had dependencies and packages that they need and the specific versions thats they needed.And thats what virtual env allows us to do .It allows us to make those different python environments.

## Why Do We Need virtualenv in Python
Isolated Environment: A virtualenv (short for "virtual environment") creates an isolated environment for Python projects. This means that each project can have its own dependencies (libraries, modules, etc.), independent of other projects and the system-wide Python installation. This isolation helps avoid conflicts between packages and their versions when multiple projects are being developed simultaneously.

Version Control: Different projects may require different versions of the same package. For example, one project may need Django 3.2 while another may require Django 4.0. By using virtual environments, you can manage different package versions for different projects without conflict.

Avoiding Permission Issues: Installing packages globally (at the system level) may require administrative or root permissions. Virtual environments allow you to install packages locally for a specific project without needing special permissions.

Install the virtual env package like so:
```pip install virtualenv```
We will make a couple of virtual environments
```mkdir Environments
   cd Environments
virtualenv project1_env
```
to activate the environment , 
```
source project1_env/bin/activate
```
```
which python  ->/Users/surbhikohli/Environments/project1_env/bin/python
```
Now ur prompt willhave name of ur virtual env
<img width="617" alt="Screenshot 2024-08-31 at 9 03 36 PM" src="https://github.com/user-attachments/assets/cdc49fb2-4e29-488d-911c-1ff603048295">  

When u run ```pip list`` u see packages only within ur environment
<img width="696" alt="Screenshot 2024-08-31 at 9 05 26 PM" src="https://github.com/user-attachments/assets/d4ff9a53-4d37-4edc-8a03-700e697d892e">

```pip freeze --local > requirements.txt```
--local adds only the dependencies that are local to ur virtaul env in the requirement.txt file  

<img width="820" alt="Screenshot 2024-08-31 at 9 17 16 PM" src="https://github.com/user-attachments/assets/5d61a3fb-f398-4b31-893d-b50b71615097">

Why We Need to Restart with the source Command
When you create a virtual environment, you need to "activate" it to use it. The source command is used to run the activation script.

What Happens When You Run source?
Modifies Environment Variables: Running the source command modifies the shell's environment variables, particularly the PATH variable, to prioritize the Python interpreter and libraries of the virtual environment over the system-wide ones. This ensures that when you run python or pip, it uses the versions from the virtual environment.

Sets the Shell Context: The command changes the shell context so that all subsequent commands will be executed within the virtual environment. It essentially "tells" your terminal to use the isolated environment you've created.

Updates the Prompt: Often, activating a virtual environment also updates the terminal prompt (e.g., (venv)) to indicate that you are working inside a virtual environment.

What Does <virtualenv>/bin/activate Represent?
<virtualenv>: This is a placeholder for the directory where your virtual environment is located. When you create a virtual environment, you typically specify a directory name for it. For example, if you created a virtual environment named myenv, then <virtualenv> would be myenv.

bin/activate:

bin: This is a subdirectory inside the virtual environment directory. On Unix-like systems (Linux and macOS), the bin directory contains executable files, including the Python interpreter and scripts needed to manage the environment.
activate: This is the script that is used to activate the virtual environment. Running this script with the source command sets up your shell to use the virtual environment's Python interpreter and libraries.



## To get out of ur virtual env
```deactivate```

To delete
``` rm -rm project1_env

```vitualenv -p /usr/bin/python2.6(python version) <projectname>```
The environments that we have here are only meant for ur dependencies and packages and not for the actual project files . You should not build ur project files within the virtual env
