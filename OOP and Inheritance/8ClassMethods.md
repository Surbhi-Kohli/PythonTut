## What are Python Class Methods?
A class method is a type of method that is bound to the class and not the instance of the class. In other words, it operates on the class as a whole, rather than on a specific instance of the class. Class methods are defined using the "@classmethod" decorator, followed by a function definition. The first argument of the function is always "cls," which represents the class itself(and not the instance).

###vWhy Use Python Class Methods?
Class methods are useful in several situations. For example, you might want to create a factory method that creates instances of your class in a specific way. You could define a class method that creates the instance and returns it to the caller. Another common use case is to provide alternative constructors for your class. This can be useful if you want to create instances of your class in multiple ways, but still have a consistent interface for doing so.


### How to Use Python Class Methods
To define a class method, you simply use the "@classmethod" decorator before the method definition. The first argument of the method should always be "cls," which represents the class itself. Here is an example of how to define a class method:
```
class ExampleClass:
    @classmethod
    def factory_method(cls, argument1, argument2):
        return cls(argument1, argument2)
```
In this example, the "factory_method" is a class method that takes two arguments, "argument1" and "argument2." It creates a new instance of the class "ExampleClass" using the "cls" keyword, and returns the new instance to the caller.

It's important to note that class methods cannot modify the class in any way. If you need to modify the class, you should use a class level variable instead.

```
class MyEmployee:
    company="Apple"
    def show_employee(self):
        print(f"The name is {self.name} and company is {self.company}")
        
    def change_company(cls,new_company_name):
        cls.company = new_company_name
        
        
        
emp1 = MyEmployee()
emp1.name = "Harry"
emp1.show_employee()
emp1.change_company("Tesla") # This did not change the class variable's value
# Rather cls = self = instance of class which is emp1, which gets a variable of  company set to Tesla
emp1.show_employee()
print(MyEmployee.company)
# If we want to update the compnay of class , we will use Class Method

```
### Using class method
```
class MyEmployee:
    company="Apple"
    def show_employee(self):
        print(f"The name is {self.name} and company is {self.company}")
    @classmethod   
    def change_company(cls,new_company_name):# The cls here is the class itself and not its instance/object
        cls.company = new_company_name
        
        
        
emp1 = MyEmployee()
emp1.name = "Harry"
emp1.show_employee() # Output:The name is Harry and company is Apple
emp1.change_company("Tesla")
emp1.show_employee() # Output: The name is Harry and company is Tesla
print(MyEmployee.company) # Tesla


```

# Class Method vs Static Method
### Class Method
A class method is bound to the class, not the instance. It is defined using the @classmethod decorator and takes the class (cls) as its first parameter.

#### Key Characteristics:
* Access to Class-Level Data: It can access and modify the class state via cls.
* Shared Across All Instances: It works with the class as a whole rather than individual instances.
  
Use Case: Useful for factory methods or when you want to operate on class variables.

### Static Method
A static method does not depend on the instance or the class. It is defined using the @staticmethod decorator and does not take self or cls as its first parameter.

#### Key Characteristics:
* No Access to Class or Instance: It cannot modify the class or instance state. It behaves like a plain function but is logically grouped within a class.
  
Use Case: Useful for utility functions that perform a task relevant to the class but don't need to interact with class-level or instance-level data.

### Comparison Table

Feature	| Class Method	| Static Method
------- |  --------  | ----------
Decorator |	@classmethod |	@staticmethod
First Parameter	| cls (class itself) |	None
Access Class Variables	|Yes |	No
Access Instance Variables	|No|	No
Use Case	|Factory methods, class-level operations|	Utility functions, independent of class/instance

