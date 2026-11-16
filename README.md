# Lab 09: Exploring D&C Algorithms

**Instructions:** Work in small groups to complete the following exercises. Try sketching out your work on the whiteboards or scratch paper. Everyone should submit their own answers to the exercises, but you are encouraged to discuss your reasoning with your group members.

Name(s): Tyler Biss

---

## Exercise 1: Recurrence Extraction

Consider the following divide-and-conquer algorithm, which takes an array $A$ of $n$ numbers as input and returns a single number. 

```text
Procedure Mystery(A, n)
    if n <= 1:
        return A[1]                              // Base case
        
    k = floor(n / 3)                             // Find the one-third point
    
    left = Mystery(A[1..k], k)                   // Recur on the left third
    right = Mystery(A[k+1..n], n - k)            // Recur on the rest
    
    total = 0 
    for i = 1 to n:
        total = total + (A[i] * left * right)    // Combine results
        
    return total
```

### Part A: The Recurrence Relation
Let $T(n)$ be the running time of `Mystery` on an input of size $n$. Write down a recurrence relation for the worst-case running time $T(n)$. You may assume $n$ is a power of 3 for simplicity. *(Note: You do not need to solve the recurrence relation yet, just formulate it).*

$T(n)$ = $T(n/3)$ + $T(2n/3)$ + $\theta(n)$
- First recurrence equates to n/3 since k is n/3 and k is what is ceiling for the recurrence
- Second recurrence equates to n - n/3 which is 2n/3 since k is equal to (n/3)
- The combine results equates to linear time since it goes from 1 to n

### Part B: Visualizing Algorithm Behavior
Without solving the recurrence, look closely at the recursive calls and the combine step. If you were to draw the recursion tree for this algorithm, what would it look like? Is the tree balanced or skewed? 

The recursion tree would be skewed. Since the two recursions shrink by different rates the first being n/3 the other 2n/3 so the tree will look skewed and unbalanced.

---

## Exercise 2: Unrolling the Recursion Tree

Suppose you have developed a new divide-and-conquer algorithm. You analyze your pseudocode and determine that its worst-case running time $T(n)$ satisfies the following recurrence relation:

$$T(n) \leq 3T\left(\frac{n}{2}\right) + cn^2 \quad \text{for } n > 1$$
$$T(1) \leq c$$

where $c$ is a positive constant. 

### Part C: Recursion Tree Analysis

Analyze the running time of the algorithm by unrolling the recursion tree. Specifically, answer the following questions:

1. **Root Work:** Find the amount of work done at the root level (level $0$) of the recursion tree.
The total work done in the root level is $cn^2$
2. **First Levels:** Find the amount of work done at level $1$ and level $2$ of the recursion tree.
The first level would split into three work values of $c(n/2)^2$ which means that the work adds up to $3c(n/2)^2$. This equates to $3/4cn^2$. The second level would then split into nine more work values of $c(n/4)^2$ which means that the work adds up to $9c(n/4)^2$. This equates to $9/16cn^2$
3. **Tree Height:** Find the height of the recursion tree (at what level does the input size reach $1$?).
The input size for T() is n but is divided by 2 for every level. So level 1, the input would be n/2. Level 2, the input would be n/4 and so on. So the input size for a certain number like x would be n/(2^x). When solving for x, we get the height of log2(n).

**Bonus!** Find a general formula for the total work done at level $i$ of the recursion tree.

---

## Exercise 3: Reflection

1. During lecture last week, we looked at two different divide-and-conquer algorithms. What were these algorithms and what problems did they solve?





2. How do the algorithms you analyzed in this lab compare to the ones we discussed in lecture? Specifically, each algorithm differs from the two we discussed in lecture in one important way. For each of the algorithms above, what is that difference?