# Advanced Algorithms Study Notes

Study-focused short notes for the MSc Advanced Algorithms module, updated from Lessons 01-06.

Source base: Lesson 01-06 PDFs

## Contents

1. [Introduction to Algorithms](#1-introduction-to-algorithms)
2. [Correctness of Algorithms](#2-correctness-of-algorithms)
3. [Complexity of Algorithms](#3-complexity-of-algorithms)
4. [Best, Worst, and Average Case](#4-best-worst-and-average-case)
5. [Asymptotic Notation](#5-asymptotic-notation)
6. [Basic Complexity Patterns](#6-basic-complexity-patterns)
7. [Insertion Sort](#7-insertion-sort)
8. [Divide and Conquer](#8-divide-and-conquer)
9. [Recurrence Relations](#9-recurrence-relations)
10. [Merge Sort](#10-merge-sort)
11. [Binary Search](#11-binary-search)
12. [Master Theorem](#12-master-theorem)
13. [Powering a Number](#13-powering-a-number)
14. [Fibonacci Numbers](#14-fibonacci-numbers)
15. [Matrix Multiplication and Strassen's Algorithm](#15-matrix-multiplication-and-strassens-algorithm)
16. [Quicksort](#16-quicksort)
17. [Dynamic Programming](#17-dynamic-programming)
18. [Coin-Row Problem](#18-coin-row-problem)
19. [Rod Cutting Problem](#19-rod-cutting-problem)
20. [Matrix Chain Multiplication](#20-matrix-chain-multiplication)
21. [Greedy Algorithms](#21-greedy-algorithms)
22. [Activity Selection Problem](#22-activity-selection-problem)
23. [Greedy Scheduling Example](#23-greedy-scheduling-example)
24. [Huffman Encoding](#24-huffman-encoding)
25. [DP vs Greedy](#25-dp-vs-greedy)
26. [Important Algorithm Complexity Summary](#26-important-algorithm-complexity-summary)
27. [Exam-Focused Formulas](#27-exam-focused-formulas)
28. [Very Important Final Revision](#28-very-important-final-revision)

---

## 1. Introduction to Algorithms

### 1.1 What is an Algorithm?

An algorithm is a finite sequence of clear steps used to solve a problem. It takes input, processes it, and gives output.

```text
Input -> Algorithm -> Output
```

Example:

```text
Problem: Find maximum number
Input:  [4, 9, 2, 7]
Output: 9
```

### 1.2 Features of an Algorithm

A proper algorithm should have:

| Feature | Meaning |
| --- | --- |
| Finiteness | Must stop after finite steps |
| Definiteness | Every step must be clear |
| Input | Zero or more inputs |
| Output | At least one output |
| Effectiveness | Each operation must be simple and executable |

These features are directly emphasized in Lesson 01.

### 1.3 Why Study Algorithms?

Algorithms are important because they are the core of computer science and are used in real-world applications such as sorting, internet systems, e-commerce, manufacturing, and large-scale data problems. Lesson 01 also explains that efficient algorithms matter because computer time and memory are limited resources.

A very important idea:

```text
A good algorithm on a slower computer can beat a bad algorithm on a faster computer.
```

---

## 2. Correctness of Algorithms

An algorithm is correct if it gives the correct output for every valid input and terminates.

### 2.1 Partial Correctness

If the algorithm terminates, the answer is correct.

### 2.2 Termination

The algorithm must eventually stop.

### 2.3 Example: GCD by Consecutive Integer Checking

To find `gcd(m, n)`:

```text
1. t = min(m, n)
2. Check whether t divides both m and n
3. If yes, return t
4. Otherwise, t = t - 1
5. Repeat
```

Example:

```text
gcd(12, 30)

t = 12 -> not divisor of both
t = 11 -> no
t = 10 -> no
...
t = 6

12 mod 6 = 0
30 mod 6 = 0

gcd(12, 30) = 6
```

This algorithm terminates because `t` decreases and eventually reaches `1`, which divides every positive integer.

### 2.4 Euclid's Algorithm

Euclid's algorithm is a more efficient GCD algorithm.

```text
while n != 0:
    r = m mod n
    m = n
    n = r

return m
```

Example:

```text
gcd(123, 36)

123 mod 36 = 15
36 mod 15 = 6
15 mod 6 = 3
6 mod 3 = 0

gcd(123, 36) = 3
```

Euclid's algorithm is a decrease-and-conquer algorithm because it replaces the original problem with a smaller one.

---

## 3. Complexity of Algorithms

### 3.1 What is Complexity?

Complexity measures how much resource an algorithm uses.

| Type | Meaning |
| --- | --- |
| Time complexity | How running time grows with input size |
| Space complexity | How memory usage grows with input size |

Lesson 02 explains that actual running time depends on many factors, such as input size, data structure, hardware, software, language, compiler, and other running programs.

### 3.2 Why Asymptotic Analysis?

Clock time is not enough because different machines and languages give different results. Therefore, algorithm analysis expresses running time as a function of input size `n`.

```text
Running time = f(n)
```

---

## 4. Best, Worst, and Average Case

For the same input size, an algorithm may take different time depending on the input.

Example: sequential search in an array of size `n`.

| Case | Meaning | Time |
| --- | --- | --- |
| Best case | Item found first | O(1) |
| Worst case | Item found last or not found | O(n) |
| Average case | Item found around middle | O(n) |

In algorithm analysis, worst-case analysis is commonly used because it gives an upper bound.

---

## 5. Asymptotic Notation

Asymptotic notation describes the growth rate of algorithms for large input sizes.

### 5.1 Big-O Notation

Big-O gives an upper bound.

```text
f(n) = O(g(n))
```

Meaning:

```text
f(n) <= c * g(n), for all n >= n0
```

Example:

```text
f(n) = 2n^2 + 10
```

For large `n`, the dominant term is `n^2`.

```text
2n^2 + 10 = O(n^2)
```

### 5.2 Omega Notation

Omega gives a lower bound.

```text
f(n) = Omega(g(n))
```

Example:

```text
10n^2 + 4n + 2 = Omega(n^2)
```

### 5.3 Theta Notation

Theta gives a tight bound.

```text
f(n) = Theta(g(n))
```

Example:

```text
10n^2 + 4n + 2 = Theta(n^2)
```

Because it is both:

```text
O(n^2) and Omega(n^2)
```

Lesson 03 explains Big-O, Omega, Theta, little-o, and little-omega as tools for comparing growth rates.

### 5.4 Common Growth Rates

From best to worst:

```text
O(1) < O(log n) < O(n) < O(n log n) < O(n^2) < O(n^3) < O(2^n) < O(n!)
```

| Complexity | Name | Example |
| --- | --- | --- |
| O(1) | Constant | Array access |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Sequential search |
| O(n log n) | Linearithmic | Merge sort |
| O(n^2) | Quadratic | Insertion sort worst case |
| O(n^3) | Cubic | Matrix multiplication |
| O(2^n) | Exponential | Naive Fibonacci |
| O(n!) | Factorial | Brute-force permutation problems |

---

## 6. Basic Complexity Patterns

### 6.1 Constant Time

```text
x = x + 1
```

Complexity:

```text
O(1)
```

### 6.2 Single Loop

```text
for i = 1 to n:
    print(i)
```

Loop runs `n` times.

```text
O(n)
```

### 6.3 Nested Loop

```text
for i = 1 to n:
    for j = 1 to n:
        print(i, j)
```

Total:

```text
n x n = n^2
```

Complexity:

```text
O(n^2)
```

### 6.4 Sum of 1 to n

#### Loop method

```text
sum = 0
for i = 1 to n:
    sum = sum + i
```

Complexity:

```text
O(n)
```

#### Formula method

```text
sum = n(n + 1) / 2
```

Complexity:

```text
O(1)
```

Example:

```text
1 + 2 + ... + 100 = 100(101)/2 = 5050
```

Lesson 02 uses this type of comparison to show that different algorithms can solve the same problem with different efficiencies.

---

## 7. Insertion Sort

### 7.1 Idea

Insertion sort builds a sorted part of the array one element at a time.

Steps:

```text
1. Take current element as key
2. Compare it with previous elements
3. Shift larger elements right
4. Insert key in correct position
```

Lesson 02 explains insertion sort with the input `8 2 4 9 3 6`.

### 7.2 Example

```text
Input:  8 2 4 9 3 6

Step 1: 2 8 4 9 3 6
Step 2: 2 4 8 9 3 6
Step 3: 2 4 8 9 3 6
Step 4: 2 3 4 8 9 6
Step 5: 2 3 4 6 8 9

Output: 2 3 4 6 8 9
```

### 7.3 Complexity

| Case | Complexity |
| --- | --- |
| Best case | O(n) |
| Average case | O(n^2) |
| Worst case | O(n^2) |

Worst case occurs when the input is reverse sorted.

Mathematically:

```text
1 + 2 + 3 + ... + (n - 1)
= n(n - 1)/2
= Theta(n^2)
```

### 7.4 Loop Invariant

A loop invariant is a statement that remains true before and after every loop iteration.

For insertion sort:

```text
Before each iteration, the left part of the array is sorted.
```

Three parts:

```text
Initialization -> Maintenance -> Termination
```

This is used to prove insertion sort correctness.

---

## 8. Divide and Conquer

Divide and conquer solves a problem by breaking it into smaller independent subproblems.

### 8.1 Three Steps

| Step | Meaning |
| --- | --- |
| Divide | Split problem |
| Conquer | Solve subproblems recursively |
| Combine | Merge subproblem solutions |

Lesson 04 explains divide and conquer using merge sort, binary search, matrix multiplication, Strassen, and quicksort.

---

## 9. Recurrence Relations

A recurrence expresses running time of a recursive algorithm.

Example:

```text
T(n) = 2T(n/2) + n
```

Meaning:

```text
2 subproblems of size n/2
plus n extra work
```

---

## 10. Merge Sort

### 10.1 Idea

Merge sort uses divide and conquer.

```text
1. Divide array into two halves
2. Recursively sort both halves
3. Merge sorted halves
```

### 10.2 Recurrence

```text
T(n) = 2T(n/2) + Theta(n)
```

Using Master Theorem:

```text
a = 2
b = 2
f(n) = n
n^(log_2 2) = n
```

So:

```text
T(n) = Theta(n log n)
```

---

## 11. Binary Search

Binary search works on a sorted array.

### 11.1 Idea

```text
1. Check middle element
2. If target is smaller, search left half
3. If target is larger, search right half
4. Repeat
```

### 11.2 Recurrence

```text
T(n) = T(n/2) + Theta(1)
```

Using Master Theorem:

```text
a = 1
b = 2
f(n) = 1
n^(log_2 1) = 1
```

Therefore:

```text
T(n) = Theta(log n)
```

---

## 12. Master Theorem

Master Theorem solves recurrences of the form:

```text
T(n) = aT(n/b) + f(n)
```

Where:

| Symbol | Meaning |
| --- | --- |
| a | Number of subproblems |
| b | Factor of input reduction |
| f(n) | Work outside recursive calls |

### 12.1 Case 1

If:

```text
f(n) = O(n^(log_b a - epsilon))
```

Then:

```text
T(n) = Theta(n^(log_b a))
```

Recursive part dominates.

### 12.2 Case 2

If:

```text
f(n) = Theta(n^(log_b a) log^k n)
```

Then:

```text
T(n) = Theta(n^(log_b a) log^(k+1)n)
```

Both recursive and non-recursive work are balanced.

### 12.3 Case 3

If:

```text
f(n) = Omega(n^(log_b a + epsilon))
```

Then:

```text
T(n) = Theta(f(n))
```

Non-recursive work dominates.

---

## 13. Powering a Number

Problem:

```text
Compute a^n
```

Naive method:

```text
a x a x a x ... x a
```

Complexity:

```text
Theta(n)
```

Divide-and-conquer method:

```text
If n is even:
a^n = a^(n/2) x a^(n/2)

If n is odd:
a^n = a^((n-1)/2) x a^((n-1)/2) x a
```

Recurrence:

```text
T(n) = T(n/2) + Theta(1)
```

Therefore:

```text
T(n) = Theta(log n)
```

---

## 14. Fibonacci Numbers

Fibonacci definition:

```text
F0 = 0
F1 = 1
Fn = F(n-1) + F(n-2), for n >= 2
```

Sequence:

```text
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
```

### 14.1 Naive Recursive Fibonacci

```text
fib(n):
    if n == 0 return 0
    if n == 1 return 1
    return fib(n-1) + fib(n-2)
```

Complexity:

```text
Exponential
```

Because the same subproblems are recomputed many times.

### 14.2 Bottom-Up Fibonacci

```text
F0 = 0
F1 = 1

for i = 2 to n:
    Fi = F(i-1) + F(i-2)
```

Complexity:

```text
Theta(n)
```

Lesson 05 uses Fibonacci to show how dynamic programming avoids repeated calculations and computes the answer in linear time.

---

## 15. Matrix Multiplication and Strassen's Algorithm

### 15.1 Standard Matrix Multiplication

For two `n x n` matrices:

```text
for i = 1 to n:
    for j = 1 to n:
        for k = 1 to n:
            C[i][j] += A[i][k] x B[k][j]
```

Complexity:

```text
Theta(n^3)
```

### 15.2 Divide-and-Conquer Matrix Multiplication

Recurrence:

```text
T(n) = 8T(n/2) + Theta(n^2)
```

Using Master Theorem:

```text
a = 8
b = 2
n^(log_2 8) = n^3
```

So:

```text
T(n) = Theta(n^3)
```

This is not better than standard matrix multiplication.

### 15.3 Strassen's Algorithm

Strassen reduces 8 recursive multiplications to 7.

Recurrence:

```text
T(n) = 7T(n/2) + Theta(n^2)
```

Using Master Theorem:

```text
a = 7
b = 2
n^(log_2 7) approx n^2.81
```

Therefore:

```text
T(n) = Theta(n^2.81)
```

This is asymptotically faster than `Theta(n^3)`. Lesson 04 also includes an exercise where the largest integer value to beat Strassen under a recurrence `T(n) = aT(n/4) + Theta(n^2)` is `a = 48`.

---

## 16. Quicksort

Quicksort is a divide-and-conquer sorting algorithm.

### 16.1 Idea

```text
1. Choose a pivot
2. Partition array into elements <= pivot and >= pivot
3. Recursively sort both parts
4. Combine is trivial
```

### 16.2 Complexity

| Case | Complexity |
| --- | --- |
| Best case | Theta(n log n) |
| Average case | Theta(n log n) |
| Worst case | Theta(n^2) |

Worst case happens when the pivot is always the minimum or maximum element, such as with sorted or reverse-sorted input.

---

## 17. Dynamic Programming

### 17.1 What is Dynamic Programming?

Dynamic Programming is an algorithm design technique used for problems with:

```text
Overlapping subproblems
Optimal substructure
```

Dynamic programming improves inefficient divide-and-conquer algorithms by solving each subproblem once and storing the result in a table. Lesson 05 explains that "programming" here refers to a tabular method.

### 17.2 DP vs Divide and Conquer

| Divide and Conquer | Dynamic Programming |
| --- | --- |
| Subproblems are usually independent | Subproblems overlap |
| Does not usually store subproblem results | Stores subproblem results |
| May recompute same subproblem | Avoids recomputation |
| Example: Merge sort | Example: Fibonacci, rod cutting |

### 17.3 Elements of Dynamic Programming

A problem is suitable for DP if it has:

| Element | Meaning |
| --- | --- |
| Simple subproblems | Original problem can be broken into similar smaller problems |
| Optimal substructure | Optimal solution contains optimal solutions to subproblems |
| Overlapping subproblems | Same subproblems occur multiple times |

Lesson 05 identifies these as the main elements of Dynamic Programming.

### 17.4 Steps to Design a DP Algorithm

1. Characterize the structure of an optimal solution.
2. Recursively define the value of an optimal solution.
3. Compute the value, usually bottom-up.
4. Construct the optimal solution from computed information.

These four design steps are given in Lesson 05.

### 17.5 Principle of Optimality

The principle of optimality states:

```text
In an optimal sequence of decisions, every subsequence must also be optimal.
```

This principle is the foundation of dynamic programming.

---

## 18. Coin-Row Problem

### 18.1 Problem

Given a row of coins:

```text
c1, c2, ..., cn
```

Choose coins to maximize total value, but no two adjacent coins can be selected.

Example:

```text
Coins: 5, 1, 6, 10, 5, 2
```

### 18.2 DP Recurrence

Let:

```text
F(n) = maximum amount from first n coins
```

For the nth coin, there are two choices:

```text
Do not pick coin n -> F(n-1)
Pick coin n -> cn + F(n-2)
```

Therefore:

```text
F(n) = max{ cn + F(n-2), F(n-1) }
```

Base cases:

```text
F(0) = 0
F(1) = c1
```

This recurrence and table method are shown in Lesson 05.

### 18.3 Example

Coins:

```text
5, 1, 6, 10, 5, 2
```

Table:

| i | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| coin | - | 5 | 1 | 6 | 10 | 5 | 2 |
| F(i) | 0 | 5 | 5 | 11 | 15 | 16 | 17 |

Maximum amount:

```text
17
```

One optimal choice:

```text
Coin 1 + Coin 4 + Coin 6 = 5 + 10 + 2 = 17
```

Complexity:

```text
Time: O(n)
Space: O(n)
```

With optimization, only previous two values are needed, so space can be reduced to:

```text
O(1)
```

---

## 19. Rod Cutting Problem

### 19.1 Problem

A rod of length `n` can be cut into pieces. Each length has a price. The goal is to maximize total revenue.

Example price table from Lesson 05:

| Length i | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Price p_i | 1 | 5 | 8 | 9 | 10 | 17 | 17 | 20 | 24 | 30 |

Lesson 05 explains that brute force considers `2^(n-1)` possible cutting ways, which is exponential.

### 19.2 Recurrence

Let:

```text
r_n = maximum revenue for rod length n
```

Then:

```text
r_n = max( p_i + r_{n-i} ), for 1 <= i <= n
```

Base case:

```text
r_0 = 0
```

### 19.3 Example

For rod length `4`:

Prices:

```text
p1 = 1, p2 = 5, p3 = 8, p4 = 9
```

Possible revenues:

```text
1 + r3 = 1 + 8 = 9
5 + r2 = 5 + 5 = 10
8 + r1 = 8 + 1 = 9
9 + r0 = 9 + 0 = 9
```

Maximum:

```text
r4 = 10
```

Optimal cutting:

```text
2 + 2
```

Revenue:

```text
5 + 5 = 10
```

### 19.4 Top-Down Memoization

Top-down memoization solves recursively but stores answers in a table.

Idea:

```text
If result is already stored, return it.
Otherwise compute it and store it.
```

This avoids repeated recursive calculations.

### 19.5 Bottom-Up Rod Cutting

Bottom-up DP solves smaller subproblems first.

```text
r[0] = 0

for j = 1 to n:
    q = -infinity
    for i = 1 to j:
        q = max(q, p[i] + r[j-i])
    r[j] = q
```

Total iterations:

```text
1 + 2 + 3 + ... + n = n(n+1)/2
```

Therefore:

```text
Time Complexity = Theta(n^2)
```

Lesson 05 states that bottom-up rod cutting runs in `Theta(n^2)` time.

---

## 20. Matrix Chain Multiplication

### 20.1 Problem

Given matrices:

```text
A1, A2, ..., An
```

Find the best parenthesization to minimize scalar multiplications.

Important point:

```text
Matrix multiplication is associative, but cost depends on parenthesization.
```

Lesson 05 explains this using examples such as:

```text
(A1 x A2) x A3
A1 x (A2 x A3)
```

### 20.2 Matrix Multiplication Cost

If matrix `A` has dimension:

```text
p x q
```

and matrix `B` has dimension:

```text
q x r
```

Then multiplication cost is:

```text
p x q x r
```

Example:

```text
A = 2 x 3
B = 3 x 2
Cost = 2 x 3 x 2 = 12
```

This exact cost calculation is shown in Lesson 05.

### 20.3 Example

Suppose:

```text
A1 = 2 x 3
A2 = 3 x 4
A3 = 4 x 2
```

#### Option 1: `(A1 x A2) x A3`

First:

```text
A1 x A2 cost = 2 x 3 x 4 = 24
```

Result dimension:

```text
2 x 4
```

Then:

```text
(A1 x A2) x A3 cost = 2 x 4 x 2 = 16
```

Total:

```text
24 + 16 = 40
```

#### Option 2: `A1 x (A2 x A3)`

First:

```text
A2 x A3 cost = 3 x 4 x 2 = 24
```

Result dimension:

```text
3 x 2
```

Then:

```text
A1 x (A2 x A3) cost = 2 x 3 x 2 = 12
```

Total:

```text
24 + 12 = 36
```

So the better parenthesization is:

```text
A1 x (A2 x A3)
```

because:

```text
36 < 40
```

---

## 21. Greedy Algorithms

### 21.1 What is a Greedy Algorithm?

A greedy algorithm makes the choice that seems best at the current moment.

```text
Local best choice -> hope for global best solution
```

Lesson 06 defines greedy algorithms as making the locally optimal choice in the hope that it leads to a globally optimal solution.

### 21.2 Characteristics of Greedy Algorithms

A greedy algorithm:

```text
1. Makes a sequence of choices
2. Each choice seems best at that moment
3. Choice depends only on what has been done so far
4. Choice reduces the problem size
```

### 21.3 Important Warning

Greedy algorithms do not always produce an optimal solution.

They work only when the problem has:

```text
Greedy-choice property
Optimal substructure
```

Lesson 06 explicitly lists these two ingredients for problems suitable for greedy strategy.

### 21.4 Greedy-Choice Property

A problem has the greedy-choice property if a globally optimal solution can be reached by making a locally optimal choice.

Meaning:

```text
Choose the best current option,
then solve the remaining subproblem.
```

But we must prove that this greedy choice leads to an optimal solution.

### 21.5 Optimal Substructure

A problem has optimal substructure if an optimal solution contains optimal solutions to its subproblems.

This is also important in Dynamic Programming, but the difference is:

```text
DP usually solves many overlapping subproblems.
Greedy chooses one direction and does not reconsider previous choices.
```

---

## 22. Activity Selection Problem

### 22.1 Problem

Input:

```text
Set of activities S = {a1, a2, ..., an}
```

Each activity has:

```text
start time s_i
finish time f_i
```

Goal:

```text
Select the maximum-size subset of mutually compatible activities.
```

Two activities are compatible if their time intervals do not overlap.

### 22.2 Greedy Strategy

The greedy rule is:

```text
Always select the activity that finishes earliest.
```

Steps:

```text
1. Sort activities by finish time
2. Select the first activity
3. For each next activity:
      select it if start time >= finish time of last selected activity
```

Lesson 06 describes this as the "early finish greedy" strategy.

### 22.3 Pseudocode

```text
GREEDY-ACTIVITY-SELECTOR(s, f)

A = {a1}
i = 1

for m = 2 to n:
    if s[m] >= f[i]:
        A = A union {am}
        i = m

return A
```

### 22.4 Why Earliest Finish Works

It leaves as much remaining time as possible for other activities. Therefore, it maximizes the opportunity to schedule more activities. Lesson 06 explains that the greedy choice maximizes the amount of unscheduled time remaining.

### 22.5 Complexity

If activities are already sorted by finish time:

```text
O(n)
```

If sorting is required:

```text
O(n log n)
```

---

## 23. Greedy Scheduling Example

Lesson 06 gives a scheduling example with 9 jobs:

```text
3, 5, 6, 10, 11, 14, 15, 18, 20 minutes
```

and 3 processors.

One greedy approach:

```text
Run longest jobs first on available processors
```

The lecture states this gives completion time:

```text
18 + 11 + 6 = 35 minutes
```

Another approach:

```text
Run shortest jobs first
```

This gives completion time:

```text
6 + 14 + 20 = 40 minutes
```

This shows that greedy algorithms are fast, but a greedy choice may not always be globally best.

---

## 24. Huffman Encoding

Lesson 06 also mentions Huffman encoding as a greedy algorithm.

Main idea:

```text
Always combine the two smallest frequencies first.
```

This greedy strategy builds an efficient prefix code.

---

## 25. DP vs Greedy

| Feature | Dynamic Programming | Greedy |
| --- | --- | --- |
| Strategy | Solves many subproblems and stores answers | Makes best current choice |
| Subproblems | Overlapping | Usually one remaining subproblem |
| Reconsider decisions? | Yes, through table comparison | No |
| Guarantees optimal? | Yes, if recurrence is correct | Only if greedy-choice property holds |
| Examples | Fibonacci, coin-row, rod cutting, matrix chain | Activity selection, Huffman coding |

---

## 26. Important Algorithm Complexity Summary

| Algorithm / Problem | Complexity |
| --- | ---: |
| Sequential search | O(n) |
| Binary search | O(log n) |
| Sum using loop | O(n) |
| Sum using formula | O(1) |
| Insertion sort best case | O(n) |
| Insertion sort worst case | O(n^2) |
| Merge sort | Theta(n log n) |
| Quicksort average case | Theta(n log n) |
| Quicksort worst case | Theta(n^2) |
| Standard matrix multiplication | Theta(n^3) |
| Strassen matrix multiplication | Theta(n^2.81) |
| Naive Fibonacci | Exponential |
| Bottom-up Fibonacci | Theta(n) |
| Coin-row DP | O(n) |
| Rod cutting DP | Theta(n^2) |
| Activity selection greedy | O(n) if already sorted |
| Activity selection with sorting | O(n log n) |

---

## 27. Exam-Focused Formulas

### Arithmetic Series

```text
1 + 2 + 3 + ... + n = n(n + 1)/2
```

Used in:

```text
Insertion sort worst case
Rod cutting bottom-up analysis
Nested cumulative loop analysis
```

### Merge Sort

```text
T(n) = 2T(n/2) + n = Theta(n log n)
```

### Binary Search

```text
T(n) = T(n/2) + 1 = Theta(log n)
```

### Standard Matrix Multiplication

```text
T(n) = Theta(n^3)
```

### Strassen

```text
T(n) = 7T(n/2) + n^2 = Theta(n^(log_2 7)) approx Theta(n^2.81)
```

### Coin-Row

```text
F(n) = max{ cn + F(n-2), F(n-1) }
F(0) = 0
F(1) = c1
```

### Rod Cutting

```text
r_n = max( p_i + r_{n-i} ), 1 <= i <= n
r_0 = 0
```

### Matrix Chain Multiplication Cost

```text
Cost of multiplying (p x q) and (q x r) matrices = pqr
```

---

## 28. Very Important Final Revision

For your exam or assignment, remember these points strongly:

```text
Algorithm = finite step-by-step solution
Correctness = correct output + termination
Complexity = time/space growth with input size
Big-O = upper bound
Omega = lower bound
Theta = tight bound
Worst case = most common analysis
Divide and conquer = divide + conquer + combine
Recurrence = time equation for recursion
Master theorem = shortcut for divide-and-conquer recurrences
Dynamic programming = overlapping subproblems + optimal substructure
Greedy = local best choice, works only when greedy-choice property holds
```

Most important topics to practice:

```text
1. Big-O simplification
2. Loop complexity
3. Recurrence solving
4. Master theorem
5. Merge sort and binary search recurrence
6. Insertion sort analysis
7. Strassen recurrence
8. Coin-row DP table
9. Rod cutting recurrence
10. Matrix chain multiplication cost
11. Activity selection greedy algorithm
12. Difference between DP and Greedy
```
