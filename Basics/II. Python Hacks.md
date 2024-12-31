### Structures
#Struct #LinkedList 
Use classes to declare a C-like struct. 
```python
'''
Description: singly linked list
Parameters: 
	self.data: stores generic data
	self.next: "pointer" to the next node
'''
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None
```
###### Reference
1. https://www.geeksforgeeks.org/singly-linked-list-in-python/
### Lambda Expression
#Lambda #Cpp 
A lambda function is a small anonymous function that can take any number of arguments, but can only have **one expression**. This is different from C++ where we can declare local variables in lambda functions.
```python
'''
Description: prints "Even number" if input is even, else "Odd number"
Parameters: 
	num: an integer
'''
evenOdds = lambda num: "Even number" if num % 2 == 0 else "Odd number"
```
###### Reference
1. https://www.w3schools.com/python/python_lambda.asp
2. https://www.geeksforgeeks.org/python-lambda/
### Higher-order Functions
#Hof #Map #Reduce #Filter #FunctionalProgramming #Zip #Enum
Recall in functional programming, we treat functions as values. That is, functions can be passed as a parameter of another function.
```python
def plus(input): 
    return input + 1
  
def minus(input): 
    return input - 1

# This is our HoF
def calc(func): 
    result = func(0)
    print(result)  
  
calc(plus)  # Outputs 1
calc(minus) # Outputs -1
```
Common higher-order functions are listed below. Most functions learned in 15150/15210 using SML have their equivalency in python.
```python
# %---------------------------------------------- map() 
nums = [1, 2, 3, 4] 
squared = map(lambda x: x**2, nums) 
print(list(squared)) 
# Output: 
#	[1, 4, 9, 16]

# %---------------------------------------------- filter()
nums = [1, 2, 3, 4]
evens = filter(lambda x: x % 2 == 0, nums)
print(list(evens))  
# Output: 
#	[2, 4]

# %---------------------------------------------- reduce()
from functools import reduce
nums = [1, 2, 3, 4] 
product = reduce(lambda x, y: x * y, nums) 
print(product) 
# Output: 24

# %---------------------------------------------- zip()
a = [1, 2, 3] 
b = ['a', 'b', 'c'] 
print(list(zip(a, b))) 
# Output: 
#	[(1, 'a'), (2, 'b'), (3, 'c')]

# %---------------------------------------------- enumerate()
words = ['hello', 'world'] 
for tup in enumerate(words): 
	print(tup)
# Output: 
#	(0, 'hello')
#	(1, 'world')
```
###### Reference
1. https://www.geeksforgeeks.org/higher-order-functions-in-python/
2. https://www.w3schools.com/python/ref_func_zip.asp
3. https://www.geeksforgeeks.org/reduce-in-python/