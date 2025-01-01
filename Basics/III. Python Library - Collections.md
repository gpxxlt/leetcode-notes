#PythonLib #Collections #Deque #Counter
### 1. Doubly Ended Queue (Deque)
Allows append and pop operations from **both** ends of the container with $O(1)$ time complexity. 
Time complexity reference sheet: https://www.geeksforgeeks.org/deque-in-python/
#### Queuing Items
All four operations in this snippet are all in $O(1)$ time complexity.
```python
# Declaration
from collections import deque 
deq = deque([1, 2, 3])

# Insertion and deletion --- all O(1) complexity
deq.append(elem)
deq.appendleft(elem)
deq.pop()
deq.popleft()
```
#### Accessing Items
All four operations in this snippet are all in $O(n)$ time complexity.
```python
# Insert elem at the specified index
deq.insert(idx,elem)
# Remove first occurence of elem
deq.remove(elem)
# Count occurence of elem
deq.count(elem)
# Returns the first index of n in range [begin, end)
deq.index(elem, begin, end)
```
Similar to list, deque can be accessed with `[]` operator, and `len()` returns deque's length. These operations are constant cost $O(1)$.
#### Global Operations
```python
# Adds a container (iterable) of elements to the right --- O(len(L))
deq.extend(L)
# Adds a container (iterable) of elements to the left ---- O(len(L))
deq.extendleft(L)
# Rotates to the right if k > 0, else to left; k can be arbitrarily large
deq.rotate(k) # O(k)
deq.reverse() # O(n)
```
### 2. Counter
Returns an object that records the frequency of each unique element in the list. Equivalent to a **histogram**. Output is ***sorted by frequency***: most frequent element goes to front. A `Counter` object can be accessed with `[]` operator like `list` and `dict` instances. 
#### Limitations
Requires elements in the list to be [hashable](https://docs.python.org/3/glossary.html#term-hashable). ***Mutable objects are not hashable.***
#### Methods
For details see [specs](https://www.geeksforgeeks.org/counters-in-python-set-1/).
```python
ctr.update(L : list)
ctr.subtract(L : list)   # Can go negative
ctr.most_common(n : int) # Optional argument, return all elements if no args
list(ctr.elements())     # Must be used with list
```
###### References
1. https://www.geeksforgeeks.org/counters-in-python-set-1/
2. https://www.geeksforgeeks.org/counters-in-python-set-2-accessing-counters/
3. https://www.geeksforgeeks.org/python-collections-module/


### 3. OrderDict
Elements in an `OrderedDict` instance are ***sorted by the order they are inserted.*** Elements inserted first have smaller indices than those inserted later.


### 4. DefaultDict
Create a dictionary with `int` as keys and provides default values for keys. Type of default values need be specified before a `DefaultDict` instance is materialized.

### 5. ChainMap
Aggregates multiple dictionaries to the same scope. Does not create a new dictionary. Changes to `ChainMap` will also apply to the original `dict` and vice versa (so a `ChainMap` is just an ***aggregation of aliases***). 
```python
# Reference: https://www.geeksforgeeks.org/chainmap-in-python/
import collections
dic1 = { 'a' : 1, 'b' : 2 }
dic2 = { 'b' : 3, 'c' : 4 }
chain = collections.ChainMap(dic1, dic2)

chain['b'] = 1000 # Modify the first key in ChainMap
print(chain)
# Output: ChainMap({'a': 1, 'b': 1000}, {'b': 3, 'c': 4})

dic2['b'] = 1001
print(chain)
# Output: ChainMap({'a': 1, 'b': 1000}, {'b': 1001, 'c': 4})

chain['k'] = -1   # Create a new key automatically
print(chain)
# Output: ChainMap({'a': 1, 'b': 1000, 'k': -1}, {'b': 1001, 'c': 4})

# Adds a new dict to aggregation
new_chain = chain.new_child({'python' : 0})
print(new_chain)
# Output: ChainMap({'python': 0}, {'a': 1, 'b': 1000, 'k': -1}, {'b': 1001, 'c': 4})

# Reverse the map
new_chain.maps = reversed(new_chain.maps)
print(new_chain)
# Output : ChainMap({'b': 1001, 'c': 4}, {'a': 1, 'b': 1000, 'k': -1}, {'python': 0})
```

### 6. NamedTuple
