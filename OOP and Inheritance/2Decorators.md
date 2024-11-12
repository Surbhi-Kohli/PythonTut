# Python Decorators

Python decorators are a powerful and versatile tool that allow you to modify the behavior of functions and methods. They are a way to extend the functionality of a function or method without modifying its source code. Decorators are often used to add functionality to functions and methods, such as logging, memoization, and access control.

A decorator is a function that takes another function as an argument and returns a new function that modifies the behavior of the original function.
The new function is often referred to as a "decorated" function.

```
 def greet(fx):
  def mfx():
    print("Good morning")
    fx()
    print("Thanks for using this function")
 return mfx

@greet # greet is a decorator, which accepts hello as argument here
def hello():
 print("hello,world")

hello()
# Output:
# Good morning
# hello,world
# Thanks for using this function
```
The ```@decorator_function``` notation is just a shorthand for the following code:
```
def my_function():
    pass
my_function = decorator_function(my_function)

```
So we can re-write the greet and hello as:
```
def greet(fx):
  def mfx():
    print("Good morning")
    fx()
    print("Thanks for using this function")
 return mfx

def hello():
 print("hello,world")

greet(hello)()

```
### Practical use case
One common use of decorators is to add logging to a function. For example, you could use a decorator to log the arguments and return value of a function each time it is called:

```
import logging
def log_function_call(func):
    def decorated(*args, **kwargs):
        logging.info(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        logging.info(f"{func.__name__} returned {result}")
        return result
    return decorated

@log_function_call
def my_function(a, b):
    return a + b
```
In this example, the log_function_call decorator takes a function as an argument and returns a new function that logs the function call before and after the original function is called.

#### Easier example to understand the passing of *args and *kwargs here:
 ```
def greet(fx):
  def mfx():
    print("Good morning")
    fx()
    print("Thanks for using this function")
 return mfx

@greet
def add(a,b):
  print(a+b)

add()
# Output for above add()
# python test.py
# Good morning
# Traceback (most recent call last):
#  File "/Users/surbhikohli/src/test.py", line 12, in <module>
#    add()
#  File "/Users/surbhikohli/src/test.py", line 4, in mfx
#    fx()
# TypeError: add() missing 2 required positional arguments: 'a' and 'b'


# in case u do:
greet(add)(1,2)
#    Output
#    greet(add)(1,2)
#    TypeError: greet.<locals>.mfx() takes 0 positional arguments but 2 were given
 ```
So we need to have the function within the decorator that accepts the passed arguments

```
def greet(fx):
  def mfx(*args, **kwargs):
    print("Good morning")
    fx(*args, **kwargs)
    print("Thanks for using this function")
 return mfx

@greet
def add(a,b):
  print(a+b)

add(1,2)
# Good morning
# 3
# Thanks for using this function
```
Or without the '@'way
```
def greet(fx):
  def mfx(*args, **kwargs):
    print("Good morning")
    fx(*args, **kwargs)
    print("Thanks for using this function")
 return mfx

def add(a,b):
  print(a+b)

greet(add)(1,2) # Currying
# Good morning
# 3
# Thanks for using this function

```
### Conclusion
Decorators are a powerful and flexible feature in Python that can be used to add functionality to functions and methods without modifying their source code. They are a great tool for separating concerns, reducing code duplication, and making your code more readable and maintainable.

In conclusion, python decorators are a way to extend the functionality of functions and methods, by modifying its behavior without modifying the source code. They are used for a variety of purposes, such as logging, memoization, access control, and more. They are a powerful tool that can be used to make your code more readable, maintainable, and extendable.
