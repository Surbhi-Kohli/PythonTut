## Exception Handling
Exception handling is the process of responding to unwanted or unexpected events when a computer program runs. Exception handling deals with these events to avoid the program or system crashing, and without this process, exceptions would disrupt the normal operation of a program.

### Exceptions in Python
Python has many built-in exceptions that are raised when your program encounters an error (something in the program goes wrong).

When these exceptions occur, the Python interpreter stops the current process and passes it to the calling process until it is handled. If not handled, the program will crash.

### Python try...except
try….. except blocks are used in python to handle errors and exceptions. The code in try block runs when there is no error. If the try block catches the error, then the except block is executed.

Syntax:
```
try:
     #statements which could generate 
     #exception
except:
     #Soloution of generated exception
```
Example:

```
try:
    num = int(input("Enter an integer: "))
except ValueError: # Handling specific type of error
    print("Number entered is not an integer.")
Output:
Enter an integer: 6.022
Number entered is not an integer.
```


Side Example of printing a table: Problem when not used int( not related to exception handling)
```
a = input("Enter the number: ")
print(f"Multiplication table of {a} is: ")
for i in range(1, 11):
    print(f"{a} X {i} = {a*i}")
# Output:
# Enter the number: 7
# Multiplication table of 7 is: 
# 7 X 1 = 7
# 7 X 2 = 77
# 7 X 3 = 777
# 7 X 4 = 7777
# 7 X 5 = 77777
# 7 X 6 = 777777
# 7 X 7 = 7777777
# 7 X 8 = 77777777
# 7 X 9 = 777777777
# 7 X 10 = 7777777777
```
Correct way:
```
a = input("Enter the number: ")
print(f"Multiplication table of {a} is: ")
for i in range(1, 11):
  print(f"{int(a)} X {i} = {int(a)*i}")
# Output:
Enter the number: 8
Multiplication table of 8 is: 
8 X 1 = 8
8 X 2 = 16
8 X 3 = 24
8 X 4 = 32
8 X 5 = 40
8 X 6 = 48
8 X 7 = 56
8 X 8 = 64
8 X 9 = 72
8 X 10 = 80
```
Now what if a user gives input as a string instead of a number, you will get an error in your output
```
Enter the number: sk
Multiplication table of sk is: 
Traceback (most recent call last):
  File "main.py", line 4, in <module>
    print(f"{int(a)} X {i} = {int(a)*i}")
ValueError: invalid literal for int() with base 10: 'sk'
```


```
= input("Enter the number: ")
print(f"Multiplication table of {a} is: ")
try:
   for i in range(1, 11):
     print(f"{int(a)} X {i} = {int(a)*i}")
except Exception as e:
 print(e)

print("some important lines of got get executed even when above code fails")
print("Program ends")

# Output:
# Enter the number: sk
# Multiplication table of sk is: 
# invalid literal for int() with base 10: 'sk'
# some important lines of got get executed even when above code fails
# Program ends

```
You can have multiple except blocks(like multiple catch blocks in js):
```
try:
    num = int(input("Enter an integer: "))
    a=[6,3]
    print(a[num])
except ValueError: # Handling specific type of error
    print("Number entered is not an integer.")
except IndexError:
   print("index error")

#Terminal:
Enter an integer: aa
Number entered is not an integer.
Enter an integer: 3
index error

```
