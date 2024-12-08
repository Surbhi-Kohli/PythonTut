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
#### Reason
When super().__ init__() is used in the Child class, it follows the method resolution order (MRO) for the Child class. The MRO determines the order in which parent class constructors (__ init__ methods) are called. The MRO ensures that:

Each class is called only once.
The order respects the linearization of the hierarchy.
The MRO for Child is:
```
Child → Parent1 → Parent2 → object
```
 #### Step-by-Step Execution
 
    1.Child's __init__ is executed, which calls super().__ init__(). 
      super() looks at the next class in the MRO after Child, which is Parent1. 
      
    2. Parent1's __ init__ is executed. 
      Since Parent1 doesn't explicitly call super().__ init__(), the chain stops here for the __ init__ calls.
      
    3. Control returns to Child's __ init__, and it prints "Child initialized". 

### Example 2: Advanced Use of super() with Multiple Inheritance

In this example, D inherits from both B and C, which themselves inherit from A. The super() function in each class's constructor ensures that the initializers of the parent classes are called in the proper order (A, B, C). This maintains consistency and avoids potential conflicts in method resolution.
```

class A:
    def __init__(self):
        print("Initializing A")

class B(A):
    def __init__(self):
        super().__init__()
        print("Initializing B")

class C(A):
    def __init__(self):
        super().__init__()
        print("Initializing C")

class D(B, C):
    def __init__(self):
        super().__init__()
        print("Initializing D")

d = D()
```
Class Hierarchy
The hierarchy can be represented as:
```
    A
   / \
  B   C
   \ /
    D
```
Class D inherits from B and C, both of which inherit from A.

MRO for Class D
In Python, the MRO is calculated using the C3 linearization algorithm. It ensures:

A consistent order for resolving methods.
Parent classes are initialized before child classes.
Left-to-right ordering is respected when possible.
For D, the MRO is:
```
D → B → C → A
```
What Happens During Initialization
When d = D() is executed:

 1. D.__ init__ calls super().__ init__().
    This looks at the next class in the MRO, which is B.
    ```B.__ init__()``` is called
 2. B.__ init__ calls super().__ init__().
    This looks at the next class in the MRO, which is C.
    super() in B doesn't directly invoke ```A.__ init__()```. Instead, it looks at the MRO after B, which points to C.
    ```C.__ init__()``` is called.
 3. When C.__ init__() is executed:
    C.__ init__ calls ```super().__ init__()```.
    super() in C looks at the MRO after C, which points to A.
    ```A.__ init__()``` is called.
 4. A.__ init__ is executed.
    Since A has no super().__ init__(), it stops here.  
 5.The control returns back up the chain:
    C.__ init__ completes.
    B.__ init__ completes.
    D.__ init__ completes.


The key point is that super() follows the MRO. So, even though B appears before C in the inheritance hierarchy of D, the MRO ensures C is called before B.

Step-by-Step Output
Initializing A: First, A is initialized because it is the common ancestor.
Initializing C: Then, C.__ init__ is executed.
Initializing B: After C, B.__ init__ is executed.
Initializing D: Finally, D.__ init__ completes the process.   
#### In this code, will B's super.__init__ not be a call to A, since A is the parent class ??
Yes, in this code, B's super().__ init__() will indeed call A.__ init__() because A is the parent class of B. However, the behavior of super() in Python considers the method resolution order (MRO). Let's analyze this step by step.

#### Why Doesn't super().__ init__() in B Call A.__ init__() Directly?
super() is not tied to the direct parent in the class hierarchy.
Instead, it follows the MRO, which ensures that A.__ init__() is only called once in the entire hierarchy.

Key Takeaways
super() resolves the next method to call based on the MRO, not just the direct parent.
This ensures that each class in the hierarchy is initialized only once, and the order is consistent with the MRO.
