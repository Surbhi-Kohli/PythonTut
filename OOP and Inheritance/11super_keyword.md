## Super keyword in Python

The super() keyword in Python is used to refer to the parent class. It is especially useful when a class inherits from multiple parent classes and you want to call a method from one of the parent classes.

When a class inherits from a parent class, it can override or extend the methods defined in the parent class. However, sometimes you might want to use the parent class method in the child class. This is where the super() keyword comes in handy.

Here's an example of how to use the super() keyword in a simple inheritance scenario:

```
class ParentClass:
    def parent_method(self):
        print("This is the parent method.")
class ChildClass(ParentClass):
    def child_method(self):
        print("This is the child method.")
        super().parent_method()
child_object = ChildClass()
child_object.child_method()
```
Output:
```
This is the child method.
This is the parent method.
```
In this example, we have a ParentClass with a parent_method and a ChildClass that inherits from ParentClass and overrides the child_method. When the child_method is called, it first prints "This is the child method." and then calls the parent_method using the super() keyword.

The super() keyword is also useful when a class inherits from multiple parent classes. In this case, you can specify the parent class from which you want to call the method.

Here's an example:
