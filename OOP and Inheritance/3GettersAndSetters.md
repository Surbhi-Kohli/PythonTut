# Getters:

In simpler terms getters help you to access a function's return value as an object's property.
Getter method behaves like a property instead of as a method.

Getters in Python are methods that are used to access the values of an object's properties. They are used to return the value of a specific property, and are typically defined using the @property decorator. Here is an example of a simple class with a getter method:
```
class MyClass:
    def __init__(self, value):
        self._value = value
    def show(self):
      print(f"value is {self._value}")
    @property
    def ten_value(self):
        return 10*self._value
obj = MyClass(10)
obj.show() # value is 10
print(obj.ten_value) # 100

# What if we try setting
obj.ten_value=67 # AttributeError: can't set attribute
```
In this example, the MyClass class has a single property, _value, which is initialized in the init method. The value method is defined as a getter using the @property decorator, and is used to return the value of the _value property.

To use the getter, we can create an instance of the MyClass class, and then access the ten_value property as if it were an attribute.

# Setters
It is important to note that the getters do not take any parameters and we cannot set the value through getter method.For that we need setter method which can be added by decorating method with @property_name.setter

Here is an example of a class with both getter and setter:

```
class MyClass:
    def __init__(self, value):
        self._value = value

    def show(self):
      print(f"value is {self._value}")

    @property
    def ten_value(self):
        return 10*self._value

    @ten_value.setter
    def value(self, new_value):
        self._value = new_value/10
obj = MyClass(10)
obj.show() # value is 10
print(obj.ten_value) # 100
obj.ten_value=67
print(obj.ten_value)#67
obj.show()# value is 6.7

```
In conclusion, getters are a convenient way to access the values of an object's properties, while keeping the internal representation of the property hidden. 
This can be useful for encapsulation and data validation.
