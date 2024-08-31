'''LEGB'''
Local, Enclosing, Global, Built in
```
x = 'Global x'
def test():
 y = 'local y'
 print(y)
 print(x)

test() // Global x, local y

print(y) //if we try accessing y here, we get error NameError: name 'y' is not defined 
```
```


x = 'Global x'
def test():
 x = 'local x'
 print(x)

test() // local x

print(x) //global x
```
What if u want to modify the global x's value from within the test function.
To do this , we can tell python that the x variable is the global one and we want to modify it with adding 'Global x'

```
x = 'Global x'
def test():
 global x
 x = 'global x being updated here'
 print(x) //global x being updated here

print(x)// global x being updated here

```
