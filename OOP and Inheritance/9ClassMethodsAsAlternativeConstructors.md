# Class Methods as Alternative Constructors
In object-oriented programming, the term "constructor" refers to a special type of method that is automatically executed when an object is created from a class. The purpose of a constructor is to initialize the object's attributes, allowing the object to be fully functional and ready to use.

However, there are times when you may want to create an object in a different way, or with different initial values, than what is provided by the default constructor. This is where class methods can be used as alternative constructors.

A class method belongs to the class rather than to an instance of the class. One common use case for class methods as alternative constructors is when you want to create an object from data that is stored in a different format, such as a string or a dictionary. For example, consider a class named "MyEmployee" that has two attributes: "name" and "salary". The default constructor for the class might look like this:
```

class MyEmployee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
```
But what if you want to create a MyEmployee object from a string that contains the person's name and salary, separated by a - in case thats how you get your input.
```
class MyEmployee:
    def __init__(self,name,salary):
        self.name = name
        self.salary = salary
        
emp1 = MyEmployee("John",12000)    
print(emp1.name,emp1.salary) # John 12000        

## If data comes in form of string: "Harry-15000", you have to parse that string and get individual data to pass to constructor
str_input ="Harry-15000"
emp2 = MyEmployee(str_input.split("-")[0],(int(str_input.split("-")[1])))
print(emp2.name,emp2.salary) # Harry 15000

```
If we try to optimize this, update the constructor __ init __ to accept a string and that has a logic to do splitting etc, that would hamper our normal initialization
```
class MyEmployee:
    def __init__(self,str):
        self.name = str_input.split("-")[0]
        self.salary = int(str_input.split("-")[1])

str_input ="Harry-15000"
emp1 = MyEmployee("Harry-15000")
print(emp1.name,emp2.salary) # Harry 15000

# But now how can we do:
# emp2 = MyEmployee("John",12000)????
```
So the above is not a good way to go about doing things.So we will use class methods as alternative constructors.

```
class MyEmployee:
    def __init__(self,name,salary):
        self.name = name
        self.salary = salary
    @classmethod
    def alt_constructor_str(cls,str):
        return cls(str.split("-")[0],(int(str.split("-")[1])))
        
emp1 = MyEmployee("John",12000)    
print(emp1.name,emp1.salary) # Output: John 12000    

## If data comes in form of string: "Harry-15000", you have to parse that string and get individual data to pass to constructor
str_input ="Harry-15000"
emp2 = MyEmployee(str_input.split("-")[0],(int(str_input.split("-")[1])))
print(emp2.name,emp2.salary)  # Output: Harry 15000

str_input3 = "Tom-18000"
emp3 = MyEmployee.alt_constructor_str(str_input3)
print(emp3.name,emp3.salary) # Output: Tom 18000


```
