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

