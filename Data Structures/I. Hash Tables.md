#Hash #PRNG 

Hash tables are primitive to python as python dictionaries are implemented via hash tables. It is also common to implement dictionaries through tree data structures such as red-black tree, but hash tables provide even better asymptotic performance in most scenarios (lookup and insert in $O(1)$ time).
### Hashing
All keys need to be first hashed so that resulting hashed indices conforms to a uniform distribution. This is important to control the expected steps taken in open addressing and bucket length in separate chaining. 
1. Keys are first transformed to numbers. 
2. The transformed number is passed to a pseudo-random number generator (**hash function**), producing a **hash value**.
3. Mod $m$ of the hash value to obtain **hash index.**
### Implementation
Hash table implementation differs mainly in their ways of dealing with ***key collisions***. 
1. Open Addressing: Linear Probing. Use next free index (modulo $m$). 
2. Open Addressing: Quadratic Probing. Try table index +1, then +4, then +9, etc.
3. Separate Chaining. Use an array of linked lists (called buckets).

|                             | Open Addressing |               Separate Chaining                |
| :-------------------------: | :-------------: | :--------------------------------------------: |
| Sensitive to Hash Function? |       Yes       |                       No                       |
|      Space Efficient?       |       Yes       |                       No                       |
|     Caching Performance     |      Good       | Many Misses <br>(poor locality of linked list) |
|    Application Scenarios    |   Known Size    |                  Unknown Size                  |
|           Others            | May become full |              Resize whenever full              |
### Asymptotic Analysis
Asymptotic performance is the same for both implementation.
- $O(1)$ average cost for **lookup**
- $O(1)$ average and amortized cost for **insert**
However, this result relies on two factors: whether a ***good hash function*** is used and whether the hash table gets automatically ***resized*** when maximum capacity is reached. We will use separate chaining for analysis.
###### Good Hash Function
Recall our motivation for using a hash function is to produce a ***uniformly distributed*** key. For an extreme counter-example, consider a hash function that always returns the ***same*** hash value. All keys will then map to the same table entry, and the linked list associated with the table entry will get extremely long.
###### Automatic Resize
Suppose our dictionary contains $n$ entries, and hash table has capacity $m$ (so $m$ linked list). The length of each linked list (bucket) is $n/m$, called **load factor.** Table is automatically resize whenever a threshold $c$ is reached. That is, $(n+1)/m \geq c$. The new table will have $2m$ entries.

Note that resizing requires inserting all entries into the new table, so time complexity is $n * O(1) = O(n)$. However, the next $n$ insertions all cost $O(1)$, so in total, insertion have amortized $O(1)$ cost.

If resize never happens, we cannot bound time complexity using threshold $c$, as buckets will grow infinitely.
###### Summary

|        Lookup        | Good Hash Function | Bad Hash Function |
| :------------------: | :----------------: | :---------------: |
| **Automatic Resize** |   $O(1)$ Average   |      $O(n)$       |
|    **No Resize**     |      $O(n/m)$      |      $O(n)$       |

|        Insert        |    Good Hash Function    |    Bad Hash Function     |
| :------------------: | :----------------------: | :----------------------: |
| **Automatic Resize** | $O(1)$ Average/Amortized | $O(1)$ Average/Amortized |
|    **No Resize**     |         $O(n/m)$         |          $O(n)$          |
### LeetCode Problems
There are a variety of LeetCode problems that utilize hash tables (dictionaries). All of then want to achieve one or more of the following:
1. Fast membership check without ordering. For example, memo in DP.
2. Records unique elements. 

----
##### References
1. CS122
2. https://stackoverflow.com/questions/2061222/what-is-the-true-difference-between-a-dictionary-and-a-hash-table?rq=3
3. https://stackoverflow.com/questions/114830/is-a-python-dictionary-an-example-of-a-hash-table
4. https://leetcode.com/problem-list/hash-table/
5. https://leetcode.com/explore/learn/card/hash-table/