
### our my_modules is in same directory as intro.py , so we would be able to directly import that
### when we import the file, it runs all the code of the imported file, even the print statement gets imported
```
import my_module
courses = ['History','Math','Physics']
 index= my_module.find_index(courses,'Math')
print(index)
#When u run the above code, u would get the following output: 
# Imported my_module...
# 1
```

 so the print statement got executed

 You could also do import my_module as mm
```
from my_module import find_index # this only gives access to find_index function and not anything else in the module, eg the test variable
won't be accessible
courses = ['History','Math','Physics']
index= my_module.find_index(courses,'Math')
print(index)
#### output:
# Imported my_module...
# 1
```

```
from my_module import find_index as fi
```
 to import everything
```
#from my_module import *
```
 But this is not preferred since it is difficult to track about what came from the imported 
 module and what did not

 When we import a module,how does it know where to find the module, we never told python the file path 
 So, the way it works is, when we import a module, python check multiple locations.And the locations are within a list named sys.path
##### we can see the list by importing that file
```
import sys
print(sys.path)  #Gives list of paths on machine where python looks for module when we run an import,
#and it looks in the order that this sys.path gives
```
 What alll directories are added to this sys.path list??
*  1st - directory where our current script resides, so u can always import modules residing in same directory
*  next:it adds the directories listed in the python path env variable
*  then it adds the standard libary directory
*  Lastly it adds the side packages directory for 3rd party packages

Now image in if the my_modules file was not present in the same directory, how can we go about import it
1 Append it to sys.path amnually in the file, where u want to import it
2.Add it to the environment variables python file
```
import sys
sys.path.append('/Users/surkohli/Desktop/My-Modules')
from my_module import find)index,text
....
```
But this is not a best approach, coz if we import this at multiple locations, we will have to append in all those files

2. setting python path env variable
```
nano ~/.bash_profile  # ~ takes to home directory
```
append:
export PYTHONPATH="/Users/surkohli/Desktop/My-Modules"
control x, control y to save and exit nano

Now u can either run a source command in terminal or reopen the terminal for the changes to be applicable

## Using some standard library in import

In Python, the standard library is a collection of modules and packages that come with Python by default. These modules provide ready-made functionality for tasks like file I/O, string manipulation, regular expressions, working with dates and times, networking, and more.

Some popular modules in the Python standard library include:

os (for interacting with the operating system)
sys (for system-specific parameters and functions)
json (for working with JSON data)
datetime (for working with dates and times)
math (for mathematical functions)
random (for generating random numbers)

You do not need to install the standard library—it comes bundled with Python when you install it. You can use these modules by simply importing them in your code.


```
import random
import datetime
import calendar
import os
import math
courses=['History','Math','Physics','CompSci']
random_course = random.choice(courses)
print(random_course)
rads = math.radians(90)
print(rads)
print(math.sin(rads))
today   = datetime.date.today()
print(today)
print(calendar.isleap(2017))
print(os.getcwd()) # gives current working directory
these modules are python files themselves and we can see their location  with __file__ attribute
print(os.__file__) # /opt/anaconda3/lib/python3.12/os.py


import antigravity