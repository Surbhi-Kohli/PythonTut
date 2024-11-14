# Inheritance in python
When a class derives from another class. The child class will inherit all the public and protected properties and methods from the parent class. In addition, it can have its own properties and methods,this is called as inheritance.

# Python Inheritance Syntax
```
class BaseClass:
  Body of base class
class DerivedClass(BaseClass):
  Body of derived class
```  


## Basic example:
```
 class Employee:
    def _ _ init_ _(self, name, id) : 
      self.name = name
      self.id = id
    def showDetails(self):  
      print(f"The name of Employee: {self.id} is {self.name}"
      
 class Programmer(Employee):
    def showLanguage():
      print("The default langage is Python")

 e1 = Employee("Rohan",400)
 e1.showDetails()

 e2 = Employee("Harry",4100)
 e2.showDetails()
 e2.showLanguage()# AttributeError: 'Employee' object has no attribute 'showLanguage'  
 
 p1 = Programmer("Tom",2000)
 p1.showLanguage() #The default langage is Python
```
Derived class inherits features from the base class where new features can be added to it. This results in re-usability of code.

Types of inheritance:
   * Single inheritance
   * Multiple inheritance
   * Multilevel inheritance
   * Hierarchical Inheritance
   * Hybrid Inheritance
     
We will see the explaination and example of each type of inheritance in the later tutorials
