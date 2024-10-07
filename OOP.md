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
