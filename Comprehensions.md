## Comprehensions
A list comprehension is an easier and more readable way to create a list

#### Example 1: Print the list
Example without list comprehension
```
nums = [1,2,3,4,5,6,7,8,9,10]

# I want 'n' for each 'n' in nums
my_list = []
for n in nums:
   my_list.append(n)
print my_list # [1,2,3,4,5,6,7,8,9,10]

```
With list comprehension:

```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list = [n for n in nums]
print(my_list) # [1,2,3,4,5,6,7,8,9,10]

```
#### Example 2 : Get square of each number and return the list with squares
```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list=[]
for n in nums:
  my_list.append(n*n)
print my_list
```
With list comprehension:
```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list=[n*n for n in nums]
print my_list # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

```
With map + lambda

```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list=map(lambda n:n*n,nums)
# better way would be to use list comprehension since that is more readable.
# 99% of times u can convert map+ lambda to list comprehension and its better to do that
print my_list # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

```
#### Example 3 : I want 'n'  for each 'n' in nums if 'n' is even
```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list=[]
for n in nums:
   if n%2==0:
    my_list.append(n)
print(my_list) # [2,4,6,8,10]
```
using list comprehension:
```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list =[n for n in nums if n%2 ==0]
print(my_list) # [2,4,6,8,10]

```

Using filter + lambda

```
nums = [1,2,3,4,5,6,7,8,9,10]
my_list=[]
my_list = filter(lamda n:n%2==0,nums)
print(my_list)
```
