#PythonLib #Collections #Deque #Counter
### 1. Doubly Ended Queue (Deque)
Allows **append** and **pop** operations from **both** ends of the container with $O(1)$ time complexity. 
##### Queuing Items
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
##### Accessing Items
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
##### Global Operations
```python
# Adds a container (iterable) of elements to the right --- O(len(L))
deq.extend(L)
# Adds a container (iterable) of elements to the left ---- O(len(L))
deq.extendleft(L)
# Rotates to the right if k > 0, else to left; k can be arbitrarily large
deq.rotate(k) # O(k)
deq.reverse() # O(n)
```
##### Reference
1. Examples and Time Complexity: https://www.geeksforgeeks.org/deque-in-python/
2. Official Documentation: https://docs.python.org/3/library/collections.html#collections.deque
### 2. Counter
Returns an object that records the frequency of each unique element in the list. Equivalent to a **histogram**. Output is ***sorted by frequency***: most frequent element goes to front. A `Counter` object can be accessed with `[]` operator like `list` and `dict` instances. 
##### Limitation
Requires elements in the list to be [hashable](https://docs.python.org/3/glossary.html#term-hashable). ***Mutable objects are not hashable.***
##### Class Methods
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
##### Summary
1. Equivalence. Two `OrderedDict` objects are ***equal*** if they have 1) same key-val pairs; 2) same ordering. Note that for 2 python vanilla dictionaries to be equal 2) is not necessary.
2. Reversal. Reversing an `OrderedDict` object requires $O(n)$ of both time and space complexity. 
3. `popitem()`: By passing different args to `popitem()`, `OrderedDict` can behave similar (LIFO or FIFO) to either **stack** or **queue.** See [[III. List-like Structures]] for details.
4. `move_to_end`: Items in an `OrderedDict` can be ***moved*** to the end or beginning due to order preservation.
##### Note
1. In python 3.7 and later versions, insertion order of vanilla dictionary (aka, `dict` instances) is preserved. 
2. `OrderedDict` is a **subclass** of `dict` so it inherits all `dict` methods.
##### Class Methods
```python
from collections import OrderedDict

# 1. Equivalency 
dic1 = { 'a' : 1, 'b' : 2, 'c' : 3 }
dic2 = { 'c' : 3, 'b' : 2, 'a' : 1 }
print(dic1 == dic2) # Output: True

od1 = OrderedDict(dic1)
od2 = OrderedDict(dic2)
print(dic1 == dic2) # Output: False

# 2. Reversal 
my_dict = OrderedDict([('a', 1), ('b', 2), ('c', 3)])
reversed_dict = OrderedDict(reversed(list(my_dict.items())))

# 3. Item removal & insertion (same as ordinary dict)
item = my_dict.popitem()            # Removes and returns the last item - LIFO  
item = my_dict.popitem(last=False)  # Removes and returns the first item - FIFO
my_dict['d'] = 4                    # Inserts key-val pair at the end

# 4. Moving items (new feature)
my_dict.move_to_end('one')              # Move 'one' to the end
my_dict.move_to_end('two', last=False)  # Move 'two' to the beginning
```
##### Reference
1. Example and comparison with python vanilla dicts: https://www.geeksforgeeks.org/ordereddict-in-python/
2. Official Documentation: https://docs.python.org/3/library/collections.html#collections.OrderedDict
### 4. DefaultDict
Create a dictionary with **default values** for keys. **Type** of default values need be specified before a `DefaultDict` instance is materialized. `Defaultdict` has same operations as `dict` with same time complexity because it is a **subclass** of dict.
##### Reference
1. Examples: https://www.geeksforgeeks.org/defaultdict-in-python/
2. Official Documentation: https://docs.python.org/3/library/collections.html#defaultdict-objects
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
Allows creation of `tuple` with named fields, similar but less redundant than creating a new class. This is more like `struct` in C++ instead of class. See [official documentation](https://docs.python.org/3/library/collections.html#namedtuple-factory-function-for-tuples-with-named-fields) for full description.
-- -
##### References
1. Intro: https://docs.python.org/3/library/collections.html
2. Official Documentation: https://www.geeksforgeeks.org/python-collections-module/
3. Time Complexity: https://www.geeksforgeeks.org/complexity-cheat-sheet-for-python-operations/