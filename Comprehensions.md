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
#### Example 4: I want a (letter,num) pair for each letter in 'abcd'  and each number in '0123'

```
my_list = []
for letter in 'abcd':
  for num in range(4):
    my_list.append((letter,num))
print(my_list)
# Output:
# [('a', 0), ('a', 1), ('a', 2), ('a', 3), ('b', 0), ('b', 1), ('b', 2), ('b', 3), ('c', 0), ('c', 1), ('c', 2), ('c', 3), ('d', 0), ('d', 1), ('d', 2), ('d', 3)]

```

With list comprehension:
```

my_list = [(letter,n) for letter in 'abcd' for num  in range(4) ]
print(my_list)
```
### Dictionary Comprehensions:

#### Example 5: I want a dict {'name':'hero'} for each name, hero in zip(names,heros)
```
names = ['Bruce','Clark','Peter','Logan','Wade']
heros = ['Batman', 'Superman','Spiderman','Wolverine','Deadpool']
print(zip(names,heros)) # <zip object at 0x7fdbe11fd580>
my_dict = {}
for name,hero in zip(names,heros):
 my_dict[name] = hero
print(my_dict) # {'Bruce': 'Batman', 'Clark': 'Superman', 'Peter': 'Spiderman', 'Logan': 'Wolverine', 'Wade': 'Deadpool'}
```
With dict comprehension:

```
names = ['Bruce','Clark','Peter','Logan','Wade']
heros = ['Batman', 'Superman','Spiderman','Wolverine','Deadpool']


my_dict = {name:hero for name,hero in zip(names,heros)}
print(my_dict) # {'Bruce': 'Batman', 'Clark': 'Superman', 'Peter': 'Spiderman', 'Logan': 'Wolverine', 'Wade': 'Deadpool'}

```
 #### Example 6 : I want a dict {'name':'hero'} for each name, if name not equal to Peter, hero in zip(names,heros)

```
names = ['Bruce','Clark','Peter','Logan','Wade']
heros = ['Batman', 'Superman','Spiderman','Wolverine','Deadpool']


my_dict = {name:hero for name,hero in zip(names,heros) if name != 'Peter'}
print(my_dict)  # {'Bruce': 'Batman', 'Clark': 'Superman', 'Logan': 'Wolverine', 'Wade': 'Deadpool'}

```
### Set Comprehensions:

```
nums =[1,1,2,1,3,4,3,4,5,5,6,7,8,7,9,9]
my_set = set()
for n in nums:
   my_set.add(n)
print(my_set) # {1, 2, 3, 4, 5, 6, 7, 8, 9}

```
With set comprehension:

```
nums =[1,1,2,1,3,4,3,4,5,5,6,7,8,7,9,9]
my_set = {n for n in nums}
print(my_set) # {1, 2, 3, 4, 5, 6, 7, 8, 9}

```

### Generator expressions:


