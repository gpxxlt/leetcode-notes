#Asymptotic #Recurrence 
### 1. Asymptotic Basics

#### Big-O
Let the time complexity of an algorithm be $f(n)$. We say $f(n) = O(g(n))$ if there exists constants $C, n_0$  such that for all $n \geq n_0, f(n) \leq Cg(n)$. That is, the expression inside big-O, which is $g(n)$, is the **upper bound** of our algorithm with time complexity $f(n)$.
#### Big-Omega
The exact reverse of big-O. For some $h: \mathbb{R}^+ \rightarrow \mathbb{R}^+, \Omega(h(n))$ represents the **lower bound** of the time complexity of our algorithm.  
#### Big-Theta
When we have both $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$, we say $f(n) = \Theta(g(n))$ holds.
### 2. Work and Span



### 3. Recurrence
We utilize the [brick method](https://www.diderot.one/courses/160/books/704/chapter/9988) to analyze time complexity of recursive algorithms. 
> [!note] 5 Steps of Brick Method
>  1. Write out recurrence expression. For example, $W(n) = 2W(n/2)+n$.
>  2. Calculate work/span of parent level. For this example, cost of parent is $n$.
>  3. Calculate work/span of child level. For this example, cost of children is $2 * n/2 = n$.
>  4. Calculate parent-to-child cost ratio. Here, we have $\text{parent} / \text{children} =n/n = 1$.
>  5. Based on the ratio, determine type of recurrence.

#### Balanced
- Condition: parent equals to children. Ratio ***equals*** to 1. 
- Total cost: number of levels * cost of each level.
##### Common Cases
1. $W(n) = 2W(n/2)+n$
2. $W(n) = W(n-1)+c$
3. $S(n) = 2S(\sqrt{n})+1$
4. $S(n) = 2S(n/2)+\log n$
#### Leaf-Dominated
- Condition: children's cost dominates that of parent's. Ratio ***less*** than 1.
- Total cost: number of leaves of the recurrence tree.
##### Common Cases
1. $W(n) = 2W(n/2)+\sqrt{n}$
2. $W(n) = 2W(n-1)+c$
#### Root-Dominated
- Condition: parents's cost dominates that of children's. Ratio ***greater*** than 1.
- Total cost: cost of the root level.
##### Common Cases
1. $W(n) = 2W(n/2)+n^2$
2. $W(n) = W(n/2)+n$
### 4. Space Complexity


###### References
[CS251](https://www.pandanotes.org/servers/cs251f23/chapters/Time_Complexity/), [CS210](https://www.diderot.one/courses/160/books/704/chapter/9986)