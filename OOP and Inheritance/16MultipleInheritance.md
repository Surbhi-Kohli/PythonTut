## Multiple Inheritance in Python
Multiple inheritance is a powerful feature in object-oriented programming that allows a class to inherit attributes and methods from multiple parent classes. This can be useful in situations where a class needs to inherit functionality from multiple sources.

### Syntax
In Python, multiple inheritance is implemented by specifying multiple parent classes in the class definition, separated by commas.
```
class ChildClass(ParentClass1, ParentClass2, ParentClass3):
    # class body
```

In this example, the ChildClass inherits attributes and methods from all three parent classes: ParentClass1, ParentClass2, and ParentClass3.

It's important to note that, in case of multiple inheritance, Python follows a __method resolution order__ (MRO) to resolve conflicts between methods or attributes from different parent classes. The MRO determines the order in which parent classes are searched for attributes and methods.

Example
```
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
        
    def make_sound(self):
        print("Sound made by the animal")
        
class Mammal:
    def __init__(self, name, fur_color):
        self.name = name
        self.fur_color = fur_color
        
class Dog(Animal, Mammal):
    def __init__(self, name, breed, fur_color):
        Animal.__init__(self, name, species="Dog")
        Mammal.__init__(self, name, fur_color)
        self.breed = breed
        
    def make_sound(self):
        print("Bark!")
```
In this example, the Dog class inherits from both the Animal and Mammal classes, so it can use attributes and methods from both parent classes.

Example demonstrating use of MRO
```
class Employee:
    def __init__(self,name):
        self.name = name
    
    def share_detail(self):
        print(f"The name is {self.name}")
        

class Dancer:
    def __init(self,dance_form):
        self.dance_form = dance_form
    
    def share_detail(self):
        print(f"The dance form is {self.dance_form}")
        
class DancerEmployee(Dancer,Employee):
    def __init__(self,name,dance_form):
        self.name = name
        self.dance_form = dance_form

DE = DancerEmployee("Surbhi","Bhangra")
DE.share_detail()  # The dance form is Bhangra
print(DancerEmployee.mro()) # [<class '__main__.DancerEmployee'>, <class '__main__.Dancer'>, <class '__main__.Employee'>, <class 'object'>]
```

```
class Employee:
    def __init__(self,name):
        self.name = name
    
    def share_detail(self):
        print(f"The name is {self.name}")
        

class Dancer:
    def __init(self,dance_form):
        self.dance_form = dance_form
    
    def share_detail(self):
        print(f"The dance form is {self.dance_form}")
        
class DancerEmployee(Employee,Dancer):
    def __init__(self,name,dance_form):
        self.name = name
        self.dance_form = dance_form

DE = DancerEmployee("Surbhi","Bhangra")
DE.share_detail()  # The name is Surbhi
print(DancerEmployee.mro()) # [<class '__main__.DancerEmployee'>, <class '__main__.Employee'>, <class '__main__.Dancer'>, <class 'object'>]

```
## Multiple Inheritance and super keyword:

Basic Example:
```
class Parent1:
    def __init__(self):
        print("Parent1 initialized")


class Parent2:
    def __init__(self):
        print("Parent2 initialized")


class Child(Parent1, Parent2):
    def __init__(self):
        super().__init__()
        print("Child initialized")


child = Child()
# Output:
# Parent1 initialized
# Child initialized
```
Reason
When super().__init__() is used in the Child class, it follows the method resolution order (MRO) for the Child class. The MRO determines the order in which parent class constructors (__init__ methods) are called. The MRO ensures that:

Each class is called only once.
The order respects the linearization of the hierarchy.
MRO for Child
The MRO for Child is:
```
Child → Parent1 → Parent2 → object
```
 #### Step-by-Step Execution
 
1.Child's __init__ is executed, which calls super().__init__().
   super() looks at the next class in the MRO after Child, which is Parent1.
2. Parent1's __init__ is executed.
    Since Parent1 doesn't explicitly call super().__init__(), the chain stops here for the __init__ calls.
3. Control returns to Child's __init__, and it prints "Child initialized".


