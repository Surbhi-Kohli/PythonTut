## Operator Overloading
Operator Overloading means giving extended meaning beyond their predefined operational meaning. For example operator + is used to add two integers as well as join two strings and merge two lists. It is achievable because ‘+’ operator is overloaded by int class and str class. You might have noticed that the same built-in operator or function shows different behavior for objects of different classes, this is called Operator Overloading. 

```
# Python program to show use of
# + operator for different purposes.

print(1 + 2)

# concatenate two strings
print("Geeks"+"For") 

# Product two numbers
print(3 * 4)

# Repeat the String
print("Geeks"*4)
```
Operator Overloading is a feature in Python that allows developers to redefine the behavior of mathematical and comparison operators for custom data types. This means that you can use the standard mathematical operators (+, -, *, /, etc.) and comparison operators (>, <, ==, etc.) in your own classes, just as you would for built-in data types like int, float, and str.

### Why do we need operator overloading?
Operator overloading allows you to create more readable and intuitive code. For instance, consider a custom class that represents a point in 2D space. You could define a method called 'add' to add two points together, but using the + operator makes the code more concise and readable:
```
p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2
print(p3.x, p3.y) # prints 4, 6
```
Consider that we have two objects which are a physical representation of a class (user-defined data type) and we have to add two objects with binary ‘+’ operator it throws an error, because compiler don’t know how to add two objects. So we define a method for an operator and that process is called operator overloading. We can overload all existing operators but we can’t create a new operator. 

### How to do operator overloading? 
To perform operator overloading, Python provides some special function or magic function that is automatically invoked when it is associated with that particular operator. For example, when we use + operator, the magic method __ add __ is automatically invoked in which the operation for + operator is defined.

You can overload an operator in Python by defining special methods in your class. These methods are identified by their names, which start and end with double underscores (__). Here are some of the most commonly overloaded operators and their corresponding special methods:
```

+ : __add__
- : __sub__
* : __mul__
/ : __truediv__
< : __lt__
> : __gt__
== : __eq__

```
 if you want to overload the + operator to add two instances of a custom class, you would define the add method:
```
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)
```
It's important to note that operator overloading is not limited to the built-in operators, you can overload any user-defined operator as well.

```
# Python Program illustrate how 
# to overload a binary + operator
# And how it actually works

class A:
    def __init__(self, a):
        self.a = a

    # adding two objects 
    def __add__(self, o):
        return self.a + o.a 
ob1 = A(1)
ob2 = A(2)
ob3 = A("Geeks")
ob4 = A("For")

print(ob1 + ob2)
print(ob3 + ob4)
# Actual working when Binary Operator is used.
print(A.__add__(ob1 , ob2)) 
print(A.__add__(ob3,ob4)) 
#And can also be Understand as :
print(ob1.__add__(ob2))
print(ob3.__add__(ob4))

```
```
class Vector:
  def __init__(self, i, j, k):
    self.i = i
    self.j = j
    self.k = k

  def __str__(self):
    return f"{self.i}i + {self.j}j + {self.k}k"

  def __add__(self, x):
    return Vector(self.i + x.i,  self.j+x.j, self.k+x.k)

v1 = Vector(3, 5, 6)
print(v1) # 3i + 5j + 6k

v2 = Vector(1, 2, 9)
print(v2) # 1i + 2j + 9k

print(v1 + v2) # 4i + 7j + 15k
print(type(v1 + v2)) # <class '__main__.Vector'>
```
