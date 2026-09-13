# 1. Algorithm Design Paradigms

 **1.1 What is an algorithm?**
An **algorithm** is a finite sequence of well-defined steps used to solve a problem.

 **1.2 What is an Algorithm Design Paradigm?**
A **design paradigm** is a general strategy for designing algorithms.

Instead of inventing every algorithm from scratch, we recognize a particular type of problem and apply a known strategy.

Think of paradigms as **problem-solving templates**.

 **Major paradigms**

| Paradigm             | Main idea                     | Examples            |
| -------------------- | ----------------------------- | ------------------- |
| Brute Force          | Try all possibilities         | Linear Search       |
| Divide and Conquer   | Divide → solve → combine      | Merge Sort          |
| Decrease and Conquer | Reduce problem size           | Binary Search       |
| Greedy               | Make best local choice        | Kruskal, Prim       |
| Dynamic Programming  | Store overlapping subproblems | Knapsack, Fibonacci |
| Backtracking         | Try → reject → undo           | N-Queens            |
| Branch and Bound     | Search with bounds            | TSP                 |
# 2. Motivation for Algorithm Analysis

There are several reasons.

- **Algorithm Comparison:** Enables objective performance comparison (e.g., selecting an $\mathcal{O}(n)$ algorithm over an $\mathcal{O}(n^2)$ alternative for superior large-scale execution).
    
- **Performance Prediction:** Forecasts execution behavior as input size $n$ increases (e.g., from $10^2$ to $10^6$), preventing failure in high-volume environments.
    
- **Scalability Assessment:** Identifies how gracefully an algorithm handles growth by ordering complexity classes:
    $$\mathcal{O}(n) \text{ scales better than } \mathcal{O}(n^2) \text{ scales better than } \mathcal{O}(2^n)$$
- **Resource Optimization:** Directs optimization efforts across hardware and system limits, including CPU computation time, memory footprint, operation counts, I/O operations, and stack depth.

# 3. Concept of Algorithmic Efficiency

Algorithmic efficiency measures the resource usage of an algorithm as the input size $n$ grows. The two primary resources evaluated are:

- **Time Complexity:** The total number of basic operations (e.g., comparisons, assignments, arithmetic operations) executed relative to input size $n$.
    
- **Space Complexity:** The extra memory space required beyond the input storage (e.g., auxiliary arrays, recursion stacks).

## Calculating time for basic operations

1. **Counting Basic Operations**
Consider:

```
int sum = 0;

for(int i = 0; i < n; i++)
{
    sum += i;
}
```

The important operation is:

```
sum += i;
```

It executes `n` times.

Therefore:

```
T(n) = cn
```

where `c` is the cost of one iteration.

So:

```
T(n)=Θ(n)
```

2. **Sequential Statements**

Consider:

```
statement1;
statement2;
statement3;
```

Suppose:

```
statement1 → O(1)
statement2 → O(n)
statement3 → O(n²)
```

Total:

```
O(1)+O(n)+O(n^2)
```

The dominant term is:

O(n^2)

Therefore:

O(n^2)

 **Rule**

For sequential operations:

> **Add their complexities, then keep the dominant term.**

 **3. Nested Loops**

Consider:

```
for(int i = 0; i < n; i++)
{
    for(int j = 0; j < n; j++)
    {
        cout << "Hello";
    }
}
```

Outer loop: n

Inner loop: n

Total:

```
n×n=n^2
```

Therefore:

Θ(n^2)

4.  **Different Loop Sizes**

```
for(int i = 0; i < n; i++)
{
    for(int j = 0; j < 100; j++)
    {
        cout << "Hello";
    }
}
```

Total: 100n

Since constants are ignored:

Θ(n)

5. **Logarithmic Loops**

Consider:

```
for(int i = 1; i < n; i *= 2)
{
    cout << i;
}
```

Values of `i`:

```
1
2
4
8
16
32
...
```

After `k` iterations:

i=2^k

The loop stops when:

2^k ≥ n

Taking log:

k ≥ log<sub>⁡2</sub> n

Therefore:

Θ(log⁡ n)

This is the basic reason **binary search is O(log n)**.

# Asymptotic Analysis
## Best, average and worst case

- **Worst-Case Analysis ($T_{worst}(n)$):** The maximum number of operations required for any input of size $n$. This provides a guaranteed upper bound on execution time.
    
- **Best-Case Analysis ($T_{best}(n)$):** The minimum number of operations required for an optimal input of size $n$ (e.g., searching for an element already in the first array slot).
    
- **Average-Case Analysis ($T_{avg}(n)$):** The expected number of operations over all possible inputs of size $n$, weighted by their probability distribution.

## What is this asymptotic analysis

Now we reach one of the most important concepts.

Suppose:

T(n)=5n^2+3n+100

For small `n`, every term matters.

But as `n` becomes extremely large:

5n^2

dominates:

3n

and

```
100
```

Therefore:

T(n)=Θ(n^2)

This study of algorithm behavior as `n → ∞` is called **asymptotic analysis**.

## Asymptotic notations

Asymptotic notations classify algorithms based on how their execution time grows relative to input size, focusing on the dominant term while ignoring constant factors:

|**Notation**|**Type of Bound**|**Informal Definition**|**Example (T(n)=3n2+5n+10)**|
|---|---|---|---|
|**Big-O ($\mathcal{O}$)**|**Upper Bound**|Algorithm grows **no faster than** this rate.|$\mathcal{O}(n^2)$|
|**Big-Omega ($\Omega$)**|**Lower Bound**|Algorithm requires **at least** this rate.|$\Omega(n^2)$|
|**Big-Theta ($\Theta$)**|**Tight Bound**|Algorithm grows at **the exact same** rate (combines $\mathcal{O}$ and $\Omega$).|$\Theta(n^2)$|

## Common Complexity Growth Rates

From generally better to worse:

```
O(1)<O(log⁡n)<O(n)<O(nlog⁡n)<O(n^2)<O(n^3)<O(2^n)<O(n!)
```

For large inputs:

```
Constant
   ↓
Logarithmic
   ↓
Linear
   ↓
Linearithmic
   ↓
Quadratic
   ↓
Cubic
   ↓
Exponential
   ↓
Factorial
```

The gap between these can become enormous.

# 5. Recurrences

Recurrence describes the running time of a recursive algorithm in terms of the running time on a smaller input.

## How to read a recurrence relation

Take:

```
T(n)=3T(n/4)+n^2
```

Don't immediately start calculating.

Read it as:

> "I have 3 subproblems, each of size n/4n/4, and I spend n2n^2 additional work."



```
T(n)=T(n-1)+1
```

means:

> One subproblem, size reduced by 1, plus constant work.


```
T(n)=2T(n/2)+n
```

means:

> Two half-sized problems plus linear work.

## Why do we need recurrences?

Consider Merge Sort.

At every level:

```
                 n
              /     \
            n/2     n/2
           /  \     /  \
         n/4 n/4 n/4 n/4
```

Merge sort does:

- 2 recursive calls
- each on size `n/2`
- plus `O(n)` work for merging

So:

```
T(n)=2T(n/2)+cn
```

This equation itself doesn't immediately tell us the answer.

We need to solve it.

The answer is:

```
T(n)=Θ(nlog⁡n)
```

The three methods you're learning are different ways of getting that answer:

1. Recursive tree
2. Master method
3. Substitution method

## 1. Recursive tree

Do this first:

| **Rule Name**            | **Formula / Identity**                                   |
| ------------------------ | -------------------------------------------------------- |
| **Product Rule**         | $\log_b(xy) = \log_b(x) + \log_b(y)$                     |
| **Quotient Rule**        | $\log_b\left(\frac{x}{y}\right) = \log_b(x) - \log_b(y)$ |
| **Power Rule**           | $\log_b(x^k) = k \cdot \log_b(x)$                        |
| **Root Rule**            | $\log_b(\sqrt[k]{x}) = \frac{1}{k} \log_b(x)$            |
| **Change of Base**       | $\log_b(x) = \frac{\log_a(x)}{\log_a(b)}$                |
| **Inverse Property (1)** | $\log_b(b^x) = x$                                        |
| **Inverse Property (2)** | $b^{\log_b(x)} = x$                                      |
| **Reciprocal Rule**      | $\log_b(x) = \frac{1}{\log_x(b)}$                        |
| **Base Power Rule**      | $\log_{b^k}(x) = \frac{1}{k} \log_b(x)$                  |

Secret sauce: 

```
            BUILD TREE
                  ↓
        Calculate work/node
                  ↓
       Calculate work/LEVEL
                  ↓
       Look at work level progression
          /        |        \
         /         |         \
    DECREASE     SAME      INCREASE
       ↓           ↓           ↓
     ROOT(first
     level)      HEIGHT ×      LEAVES(last level)
   dominates   level work    dominate
```

After calculating the work at each level, **write the sum**.

Then inspect it.

- If you get: $n+n+n+n+⋯n+n+n+n+\cdots$ (Work remains same at all levels)
	you need the **number of levels**: O(nlog⁡n)

- If you get: 1+2+4+8...... (Work keeps on increasing level by level)
	the **last level dominates**: Θ(n)

- If you get: $n^2+\frac{n^2}{2}+\frac{n^2}{4}+\cdots$(Work keeps on decreasing level by level)
	the **first level dominates**: Θ(n^2)

These rules are valid in most cases but there are cases when these fail. So always write the sum of work and then decide.

 **Step 1 — Draw the tree**

```
             T(n)
            /    \
        T(...)  T(...)
        /  \     /  \
       ...
```

**Step 2 — Write work at each node**

Use the f(n) part.

**Step 3 — Calculate total work of each level**

$\boxed{\text{nodes at level}\times\text{work per node}}$

**Step 4 — Find the height**

Keep expanding until the subproblem reaches the base case.

**Step 5 — Write the actual sum**

For example:

n+n+n+⋯n+n+n+

or

$1+2+4+⋯+n1+2+4+\cdots+n$

or

$n^2+{n^2}^2+{n^2}^4 +⋯n^2+\frac{n^2}{2}+\frac{n^2}{4}+\cdots$

**Step 6 — Evaluate the sum**
**This is where you determine the answer.**

## 2. Master Theorem 

The Master Theorem applies to recurrences of the form:

```
T(n)=aT(n/b)+f(n)
```

where:

- a = number of subproblems
- b = factor by which input size shrinks
- f(n) = work done **outside** the recursive calls

The key comparison is:

f(n) vs n<sup>log⁡<sub>b</sub>a</sup>


Think of f(n) vs n<sup>log⁡<sub>b</sub>a</sup> as the **recursive-tree benchmark**.

### Master Method Workflow

Whenever you see a recurrence, do **exactly these steps**.

 **Step 1 — Check the form**

Ask:

> Can I write this as

```
T(n)=aT(n/b)+f(n)
```

If **yes**, Master Theorem may apply. If **no**, don't force it.


**Step 2 — Identify a,b,f(n)**

Example:

```
T(n)=3T(n/2)+n^2
```
Therefore a=3 b=2 f(n)=n^2

**Step 3 — Calculate the benchmark**

Calculate: n<sup>log⁡<sub>b</sub>a</sup>
Here: n<sup>log<sub>⁡2</sub>3</sup> ≈1.585
benchmark: n^{1.585}

**Step 4 — Compare f(n) with the benchmark**

Now compare: f(n) against n<sup>log⁡<sub>b</sub>a</sup>

There are **three major cases**.

**Case 1 — f(n) is smaller**

If $f(n)=O\left(n^{\log_ba-\epsilon}\right)$ for some constant ϵ>0

then $\boxed{T(n)=O(n^{\log_ba})}$


**Case 2 — Same size**

If $f(n)=\Theta(n^{\log_ba}.\log^{k}_2 n)$

then $\boxed{T(n)=\Theta(n^{\log_ba}.\log^{(k+1)}_2 n)}$
assume K such that it matches the condition and k >= 1

**Case 3 — f(n) is larger**

If $f(n)=\Omega(n^{\log_ba+\epsilon})$ & af(n/b) < cf(n)

for some ϵ>0, c < 1
then:

$\boxed{T(n)=\Theta(f(n))}$

# 3. Substitution Method
## 1. What is the Substitution Method?

The **substitution method** is a way to solve a recurrence by:

1. **Guessing** the answer.
2. **Substituting** the guessed bound into the recurrence.
3. **Proving** that the guess is correct using mathematical induction.

The main idea:

> **Expand the recurrence → see the pattern → guess the complexity → prove the guess.**


Suppose:

T(n) = 2T(n/2)+n

We want to find its asymptotic complexity.

Instead of drawing the entire recursion tree, substitution asks:

> **Can I guess a bound for T(n), then prove it?**

We already suspect:

T(n)=O(nlog⁡n)

Now we prove it.


# 4. Example: T(n)=2T(n/2)+n

Let's solve it completely.

We guess:

T(n)=O(nlog⁡n)

So assume:

T(n/2)≤cn2log⁡n2T(n/2)\leq c\frac n2\log\frac n2

Substitute this into the recurrence:

T(n)=2T(n/2)+nT(n) = 2T(n/2)+n

Therefore:

T(n)≤2(cn2log⁡n2)+nT(n) \leq 2\left(c\frac n2\log\frac n2\right)+n

Simplify:

T(n)≤cnlog⁡n2+nT(n) \leq cn\log\frac n2+n

Using:

log⁡n2=log⁡n−1\log\frac n2=\log n-1

we get:

T(n)≤cn(log⁡n−1)+nT(n)\leq cn(\log n-1)+n T(n)≤cnlog⁡n−cn+nT(n)\leq cn\log n-cn+n T(n)≤cnlog⁡n−(c−1)nT(n)\leq cn\log n-(c-1)n

If:

c≥1c\geq1

then:

−(c−1)n≤0-(c-1)n\leq0

so:

T(n)≤cnlog⁡nT(n)\leq cn\log n

Therefore:

T(n)=O(nlog⁡n)\boxed{T(n)=O(n\log n)}

---

# 5. Why Do We Use a Constant cc?

This is extremely important.

When we say:

T(n)=O(nlog⁡n)T(n)=O(n\log n)

we don't directly substitute:

T(n/2)=n2log⁡n2T(n/2)=\frac n2\log\frac n2

Instead, we assume:

T(n/2)≤c(n2log⁡n2)\boxed{T(n/2)\leq c\left(\frac n2\log\frac n2\right)}

because Big-O means:

T(n)≤c g(n)T(n)\leq c\,g(n)

for some constant c>0c>0.

So **cc gives us room to make the inequality work.**

---

# 6. The Induction Structure

Substitution method is essentially **mathematical induction on nn**.

You have:

### Induction hypothesis

Assume:

T(k)≤cg(k)T(k)\leq cg(k)

for smaller values k<nk<n.

Since:

n2<n\frac n2<n

we can apply the hypothesis to T(n/2)T(n/2).

Then substitute it into the recurrence.

---

# 7. The Base Case

You must also verify the recurrence for small nn.

For example:

T(n)=2T(n/2)+nT(n)=2T(n/2)+n

Suppose the base case is:

T(1)=c0T(1)=c_0

We need to choose cc large enough so that:

T(1)≤c(1log⁡1)T(1)\leq c(1\log1)

But log⁡1=0\log1=0, so this particular guessed form isn't convenient at the base case.

A common fix is to use:

T(n)≤cnlog⁡n+dnT(n)\leq cn\log n+dn

or start from a sufficiently large constant n0n_0.

For learning, don't get stuck on the base case—the **substitution step is the main idea**.

---

# 8. How Do We Make the Guess?

This is usually the hardest part.

You don't randomly guess.

Use:

### Method A — Expand a few times

For:

T(n)=2T(n/2)+nT(n)=2T(n/2)+n

Expand:

T(n)=2[2T(n/4)+n/2]+nT(n)=2[2T(n/4)+n/2]+n =4T(n/4)+2n=4T(n/4)+2n

Again:

=8T(n/8)+3n=8T(n/8)+3n

Pattern:

T(n)=2kT(n/2k)+knT(n)=2^kT(n/2^k)+kn

At:

k=log⁡2nk=\log_2n

we get:

T(n)=nT(1)+nlog⁡nT(n)=nT(1)+n\log n

Therefore:

T(n)=Θ(nlog⁡n)\boxed{T(n)=\Theta(n\log n)}

Now you have your **guess**.

---

# 9. Substitution Method vs Recursion Tree

They are solving the same recurrence, but differently.

### Recursion Tree

You ask:

> How much work is happening at every level?

### Substitution

You ask:

> Can I prove that T(n)T(n) is bounded by my guessed function?

So:

Recursion Tree → discover the answer\boxed{\text{Recursion Tree → discover the answer}} Substitution → prove the answer\boxed{\text{Substitution → prove the answer}}

This is a very useful way to remember the difference.

---

# 10. Example Where the Guess Is O(n)O(n)

Consider:

T(n)=2T(n/2)+1T(n)=2T(n/2)+1

From recursion-tree intuition:

T(n)=Θ(n)T(n)=\Theta(n)

Guess:

T(n)≤cnT(n)\leq cn

Substitute:

T(n)=2T(n/2)+1T(n) = 2T(n/2)+1

Using the hypothesis:

T(n/2)≤cn2T(n/2)\leq c\frac n2

Therefore:

T(n)≤2(cn2)+1T(n)\leq2\left(c\frac n2\right)+1 T(n)≤cn+1T(n)\leq cn+1

We need:

cn+1≤cncn+1\leq cn

which is impossible.

### What's happening?

Our guess:

T(n)≤cnT(n)\leq cn

is **too tight** for the induction to work.

This doesn't mean T(n)T(n) isn't O(n)O(n).

It means we need a **stronger induction hypothesis**.

---

# 11. The Trick: Add a Lower-Order Term

Instead, guess:

T(n)≤cn−d\boxed{T(n)\leq cn-d}

Substitute:

T(n)≤2(cn2−d)+1T(n)\leq2\left(c\frac n2-d\right)+1 =cn−2d+1=cn-2d+1

We want:

cn−2d+1≤cn−dcn-2d+1\leq cn-d

which means:

−d+1≤0-d+1\leq0

Therefore:

d≥1d\geq1

So the induction works.

This is one of the **most important tricks** in substitution method:

> If your guess is correct but substitution leaves an annoying extra term, **strengthen the guess**.

---

# 12. Common Strengthening Tricks

If your first guess doesn't work, try:

### Guess 1

T(n)≤cnT(n)\leq cn

If it fails, try:

T(n)≤cn−dT(n)\leq cn-d

---

### Guess 2

T(n)≤cnlog⁡nT(n)\leq cn\log n

If it fails, try:

T(n)≤cnlog⁡n−dnT(n)\leq cn\log n-dn

---

### Guess 3

T(n)≤cn2T(n)\leq cn^2

If it fails, try:

T(n)≤cn2−dnT(n)\leq cn^2-dn

The extra term gives the induction inequality some **slack**.

---

# 13. Big-O vs Big-Ω vs Θ

Substitution can prove different types of bounds.

### To prove Big-O

Assume:

T(n)≤cg(n)T(n)\leq cg(n)

and prove it.

T(n)=O(g(n))\boxed{T(n)=O(g(n))}

---

### To prove Big-Ω

Assume:

T(n)≥cg(n)T(n)\geq cg(n)

and prove it.

T(n)=Ω(g(n))\boxed{T(n)=\Omega(g(n))}

---

### To prove Θ

Prove both:

T(n)=O(g(n))T(n)=O(g(n))

and

T(n)=Ω(g(n))T(n)=\Omega(g(n))

Therefore:

T(n)=Θ(g(n))\boxed{T(n)=\Theta(g(n))}

---

# 14. The Complete Workflow

For an exam/problem, use this:

1. Expand\boxed{\textbf{1. Expand}}

Expand the recurrence a few times to discover a pattern.

2. Guess\boxed{\textbf{2. Guess}}

Guess O(g(n))O(g(n)), Ω(g(n))\Omega(g(n)), or Θ(g(n))\Theta(g(n)).

3. Write the Induction Hypothesis\boxed{\textbf{3. Write the Induction Hypothesis}}

For example:

T(n/2)≤c g(n/2)T(n/2)\leq c\,g(n/2) 4. Substitute\boxed{\textbf{4. Substitute}}

Put the hypothesis into the recurrence.

5. Simplify\boxed{\textbf{5. Simplify}}

Use logarithm/exponent rules.

6. Make the Inequality Work\boxed{\textbf{6. Make the Inequality Work}}

Choose suitable constants such as cc or dd.

7. Check Base Case\boxed{\textbf{7. Check Base Case}}

Verify the bound for the smallest relevant nn.

8. State the Result\boxed{\textbf{8. State the Result}} T(n)=O(g(n))\boxed{T(n)=O(g(n))}

or

T(n)=Θ(g(n))\boxed{T(n)=\Theta(g(n))}

---

# 15. The One-Line Mental Model

When you see **Substitution Method**, think:

Expand → Guess → Assume → Substitute → Simplify → Prove\boxed{ \text{Expand → Guess → Assume → Substitute → Simplify → Prove} }

And remember:

> **The difficult part is usually finding the right guess. Once the guess is right, substitution is mostly algebra.**

Next, the best way to learn this is **3–4 carefully chosen problems**, starting with an easy one like T(n)=2T(n/2)+1T(n)=2T(n/2)+1, then moving to one where you need the **cn−dcn-d** strengthening trick.
