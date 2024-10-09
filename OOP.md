### Introduction to Object-oriented programming
## Introduction to Object-Oriented Programming in Python: In programming languages, mainly there are two approaches that are used to write program or code.

1). Procedural Programming
2). Object-Oriented Programming
The procedure we are following till now is the “Procedural Programming” approach. So, in this session, we will learn about Object Oriented Programming (OOP). The basic idea of object-oriented programming (OOP) in Python is to use classes and objects to represent real-world concepts and entities.

A class is a blueprint or template for creating objects. It defines the properties and methods that an object of that class will have. Properties are the data or state of an object, and methods are the actions or behaviors that an object can perform.

An object is an instance of a class, and it contains its own data and methods. For example, you could create a class called "Person" that has properties such as name and age, and methods such as speak() and walk(). Each instance of the Person class would be a unique object with its own name and age, but they would all have the same methods to speak and walk.

One of the key features of OOP in Python is encapsulation, which means that the internal state of an object is hidden and can only be accessed or modified through the object's methods. This helps to protect the object's data and prevent it from being modified in unexpected ways.

Another key feature of OOP in Python is inheritance, which allows new classes to be created that inherit the properties and methods of an existing class. This allows for code reuse and makes it easy to create new classes that have similar functionality to existing classes.

Polymorphism is also supported in Python, which means that objects of different classes can be treated as if they were objects of a common class. This allows for greater flexibility in code and makes it easier to write code that can work with multiple types of objects.

In summary, OOP in Python allows developers to model real-world concepts and entities using classes and objects, encapsulate data, reuse code through inheritance, and write more flexible code through polymorphism.

### Python Class and Objects
A class is a blueprint or a template for creating objects, providing initial values for state (member variables or attributes), and implementations of behavior (member functions or methods). The user-defined objects are created using the class keyword.

#### Creating a Class:
Let us now create a class using the class keyword.
```
class Details:
    name = "Rohan"
    age = 20

```
#### Creating an Object:
Object is the instance of the class used to access the properties of the class Now lets create an object of the class.

Example:
```
obj1 = Details()
Now we can print values:

Example:
class Details:
    name = "Rohan"
    age = 20
obj1 = Details()
print(obj1.name)
print(obj1.age)
Output:
Rohan
20
```

### self parameter
The self parameter is a reference to the current instance of the class, and is used to access variables that belongs to the class.
It must be provided as the extra parameter inside the method definition.

Example:
```
class Details:
    name = "Rohan"
    age = 20
    def desc(self):
        print("My name is", self.name, "and I'm", self.age, "years old.")
obj1 = Details()
obj1.desc()
Output:
My name is Rohan and I'm 20 years old.
```
```
class Person:
  name = "Harry"
  occupation = "Software Developer"
  networth = 10
  def info(self):
    print(f"{self.name} is a {self.occupation}")


a = Person()
b = Person()
c = Person()

a.name = "Shubham"
a.occupation = "Accountant"

b.name = "Nitika"
b.occupation = "HR"

# print(a.name, a.occupation)
a.info() # Shubham is a Accountant
b.info() # Nitika is a HR
c.info() # Harry is a Software Developer
```
## Constructors in Python
A constructor is a special method in a class used to create and initialize an object of a class. There are different types of constructors. Constructor is invoked automatically when an object of a class is created.

A constructor is a unique function that gets called automatically when an object is created of a class. The main purpose of a constructor is to initialize or assign values to the data members of that class. It cannot return any value other than None.

### Syntax of Python Constructor
```
def __init__(self):
	# initializations
```
init is one of the reserved functions in Python. In Object Oriented Programming, it is known as a constructor.

### Explanation with code:
```
class Person:
  name:"Harry"
  occupation:"Developer"

  def info(self): # **Very Important:Every method of a class should have self as paramter, with few exceptions
   print(f"{self.name} is a {self.occ}")

 a = Person() # Harry is a Developer
 print(a.name) # Harry
 a.info() # self is automatically considered as 'a' and passed

```
But what if we want to create multiple Persons, we will have to explicitly set their name , occupation etc. Better option would be to use a constructor.

```
class Person:

  def __init__(self,name,occupation):
   print("Hey I am a person constructor , called every time a new Person object is created")
   self.name = name
   self.occ = occupation

  def info(self): # **Very Important:Every method of a class should have self as paramter, with few exceptions
   print(f"{self.name} is a {self.occ}")

 a = Person("Harry","Aalsi developer")
 b = Person("Tom","Rotlu developer")
 
 a.info() # Harry is a Aalsi developer
 b.info() # Tom is a Rotlu developer
 c =  Person() # Error: __init__ missing 2 required positional arguments : "name"  and "occupation"
 c = Person(1,2 ,3)# TypeError: __init__ takes 3 positional arguments but 4 were given , (since self is auto passed, total arguments became 4)

```
### Types of Constructors in Python

1. Parameterized Constructor
2. Default Constructor
 ### Parameterized Constructor in Python
When the constructor accepts arguments along with self, it is known as parameterized constructor.
These arguments can be used inside the class to assign the values to the data members.

Example:
```
class Details:
    def __init__(self, animal, group):
        self.animal = animal
        self.group = group

obj1 = Details("Crab", "Crustaceans")
print(obj1.animal, "belongs to the", obj1.group, "group.")
```
### Output:
```
Crab belongs to the Crustaceans group.
```
### Default Constructor in Python
When the constructor doesn't accept any arguments from the object and has only one argument, self, in the constructor, it is known as a Default constructor.

Example:
```
class Details:
  def __init__(self):
    print("animal Crab belongs to Crustaceans group")
obj1=Details()
```
### Output:
```
animal Crab belongs to Crustaceans group
```
