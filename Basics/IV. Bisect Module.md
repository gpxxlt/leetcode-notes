In this note we will introduce Python `bisect` module. This module will be useful in settings where you need to perform a modified sorting or binary search. Specifically, it helps pinpoint the location that would otherwise nasty to find when we want a specific relation to be satisfied, for example, greater or equal to.

```python
import bisect

lst = [1, 3, 4, 4, 5, 7]
position = bisect.bisect_left(lst, 4)
print(position)  
# Output: 2

bisect.insort_left(lst, 4)
print(lst)  
# Output: [1, 3, 4, 4, 4, 5, 7]

```
Similarly there are `right` versions of the above algorithms. 

##### Time Complexity
Same as common search $O(\log n)$ and sort $O(n\log n)$.
##### References
1. https://docs.python.org/3/library/bisect.html

##### LeetCode Problems
1. https://leetcode.com/problems/successful-pairs-of-spells-and-potions/description/?envType=study-plan-v2&envId=leetcode-75 