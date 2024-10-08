## What if a function being exported is also executed within that file??
Consider JS situation
main.js:
```

function print(){
    console.log("hello")
}
print()/**
module.exports = {
  print
  };
```


```
index.js:
const { print } = require('./main');
const message = 'See'; // Try edit me


print()
//Logs:
//hello
//hello 
```
hello is logged twice because once the print within main.js is executed and once when imported and called from index.js 

Same thing can happen in python:

```
harry.py:
def welcome():
  print("Hey you are welcome from harry")

welcome()

```

```
main.py:

import harry
harry.welcome()
# Hey you are welcome from harry
# Hey you are welcome from harry
# Printed twice

```
To solve this problem

```
harry.py:
def welcome():
  print("Hey you are welcome from harry")

print(__name__) #"__main__" in case this file is called as python harry.py or else if u run as python main.py , value is harry

if __name__ == "__main__":
  welcome() # Only execute welcome if __name__ == "main" , ie the welcome function is called from within this file only and not from outside

```  




If instead, in terminal, you run ``` python harry.py``` the output would be "Hey you are welcome from harry"

## if "__ name __ == "__ main __" in Python

The if __ name __ == "__ main __" idiom is a common pattern used in Python scripts to determine whether the script is being run directly or being imported as a module into another script.
In Python, the __ name __ variable is a built-in variable that is automatically set to the name of the current module. When a Python script is run directly, the __ name __ variable is set to the 
string __ main __ When the script is imported as a module into another script, the __ name __ variable is set to the name of the module.

Here's an example of how the if __ name __ == __ main __ idiom can be used:
```
def main():
    # Code to be run when the script is run directly
    print("Running script directly")
if __name__ == "__main__":
    main()
```

In this example, the main function contains the code that should be run when the script is run directly. The if statement at the bottom checks whether the __ name __ variable is equal to __ main __. 
If it is, the main function is called.


### Why is it useful?
This idiom is useful because it allows you to reuse code from a script by importing it as a module into another script, without running the code in the original script. For example, consider the following script:
```
def main():
    print("Running script directly")
if __name__ == "__main__":
    main()
```
If you run this script directly, it will output "Running script directly". However, if you import it as a module into another script and call the main function from the imported module, it will not output anything:
```
import script
script.main()  # Output: "Running script directly"
```

This can be useful if you have code that you want to reuse in multiple scripts, but you only want it to run when the script is run directly and not when it's imported as a module.

### Is it a necessity?
It's important to note that the if __ name __ == "__ main __ " idiom is not required to run a Python script. You can still run a script without it by simply calling the functions or running the code you want to execute directly. However, the if __ name __ == "__ main __" idiom can be a useful tool for organizing and separating code that should be run directly from code that should be imported and used as a module.

In summary, the if __ name __ == "__ main __" idiom is a common pattern used in Python scripts to determine whether the script is being run directly or being imported as a module into another script. It allows you to reuse code from a script by importing it as a module into another script, without running the code in the original script.

