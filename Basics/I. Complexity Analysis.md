#Asymptotic #Recurrence #Parallelism #Scheduling
### 1. Asymptotic Basics
#### Big-O
Let the time complexity of an algorithm be $f(n)$. We say $f(n) = O(g(n))$ if there exists constants $C, n_0$  such that for all $n \geq n_0, f(n) \leq Cg(n)$. That is, the expression inside big-O, which is $g(n)$, is the **upper bound** of our algorithm with time complexity $f(n)$.
#### Big-Omega
The exact reverse of big-O. For some $h: \mathbb{R}^+ \rightarrow \mathbb{R}^+, \Omega(h(n))$ represents the **lower bound** of the time complexity of our algorithm.  
#### Big-Theta
When we have both $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$, we say $f(n) = \Theta(g(n))$ holds.
### 2. Work and Span
#### Basic Concepts
>[!quote] Rough Definition (CS210)
> Roughly speaking, the **work** of a computation corresponds to the total number of operations it performs, and the **span** corresponds to the longest chain of dependencies in the computation. 

In other words, work is defined under sequential computation, or single-core computation, whereas span is considered in multi-core scenarios. We can derive a efficiency metric (for any algorithm) by comparing single-core versus multi-core efficiency as follows.
>[!note] Parallelism (**Average Parallelism**)
>Parallelism ($\bar{P}$) is defined as the work over the span ($W/S$).  It informs us approximately how many processors we can use efficiently. 
#### Scheduling
Due to scheduling, computation efficiency does not grow linearly with the number of processors. In multi-core settings, it is impossible to perfectly distribute tasks among all available processors. 
>[!note] Definition (Greedy Scheduler)
>A scheduler is **greedy** if whenever there is a processor available and a task ready to execute, it assigns the task to the processor and starts running it immediately. 

>[!note] Definition (Greedy Scheduling Principle)
>If a computation is run on $P$ processors using a **greedy scheduler**, then the total time $T_P$ (clock cycles) for running the computation is bounded by $T_P < W/P + S$, where $W$ is work, $S$ is span. When we have high parallelism $W/P + S \rightarrow W/P$.

 A greedy scheduler does reasonably close to best possible. Note that $T_P>\max({W/P, S})$:
 1. $T_P>W/P$ because we only have $P$ processors and even distribution of work is ***absolute*** lower bound;
 2. $T_P>S$ because $S$ represents the ***longest*** chain of ***sequential*** dependencies; we surely have other chains.
 
 However, greedy schedule is unachievable in practice. For example, distributing work also requires a certain amount of computation power. This is why we need some other metric to evaluate parallel execution.

>[!note] Definition (Speedup)
>The **speedup** $S_P$ of a $P$-processor parallel execution over a sequential one is defined as $S_P = T_S/T_P$ where $T_S$ is sequential time, $T_P$ is parallel time. **Perfect speedup** is reached when $S_P = P$.
### 3. Recurrence
We utilize the [brick method](https://www.diderot.one/courses/160/books/704/chapter/9988) to analyze time complexity of recursive algorithms. 
> [!summary] 5 Steps of Brick Method
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
----
##### References
1. [CS251](https://www.pandanotes.org/servers/cs251f23/chapters/Time_Complexity/)
2. [CS210](https://www.diderot.one/courses/160/books/704/chapter/9986)