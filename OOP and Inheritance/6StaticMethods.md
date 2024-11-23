## Static methods
Static methods in Python are methods that belong to a class rather than an instance of the class. They are defined using the @staticmethod decorator and do not have access to the instance of the class (i.e. self). They are called on the class itself, not on an instance of the class. Static methods are often used to create utility functions that don't need access to instance data.

```
class Math:
    def __init__(self):
        pass
    @staticmethod
    def addUtility(a, b):
        sum=a+b
        return "Good morning, here take your sum: " + str(sum)

    def mathAdd(self,a,b):# this method internally calls the utility 
        return Math.addUtility(a,b)
        
result = Math.addUtility(1, 2)
mathOb= Math()

print(result) # Good morning, here take your sum: 3
print(mathOb.mathAdd(4,6)) # Good morning, here take your sum: 10
print(mathOb.addUtility(7,8)) # Good morning, here take your sum: 15

```
Q: When u define a method inside a class, is it necessary to provide self?  
A: No, self would not be required in case of a static method
