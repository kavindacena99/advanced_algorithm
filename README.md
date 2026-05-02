# Advanced Algorithms Study Notes

Short, exam-focused notes for the MSc Advanced Algorithms module, prepared from Lessons 01-04.

## Contents

1. [Introduction to Algorithms](#1-introduction-to-algorithms)
2. [Algorithm Correctness](#2-algorithm-correctness)
3. [Complexity of Algorithms](#3-complexity-of-algorithms)
4. [Best, Worst, and Average Case](#4-best-worst-and-average-case)
5. [Asymptotic Notation](#5-asymptotic-notation)
6. [Common Growth Rates](#6-common-growth-rates)
7. [Complexity Rules](#7-complexity-rules)
8. [Basic Complexity Examples](#8-basic-complexity-examples)
9. [Sum of 1 to n](#9-sum-of-1-to-n)
10. [Insertion Sort](#10-insertion-sort)
11. [Loop Invariant](#11-loop-invariant)
12. [Merge Sort](#12-merge-sort)
13. [Recurrence Relations](#13-recurrence-relations)
14. [Solving Recurrences](#14-solving-recurrences)
15. [Divide and Conquer](#15-divide-and-conquer)
16. [Master Theorem](#16-master-theorem)
17. [Binary Search](#17-binary-search)
18. [Powering a Number](#18-powering-a-number)
19. [Fibonacci Numbers](#19-fibonacci-numbers)
20. [Matrix Multiplication](#20-matrix-multiplication)
21. [Strassen Improvement Problem](#21-strassen-improvement-problem)
22. [Quicksort](#22-quicksort)
23. [Algorithm Comparison Table](#23-algorithm-comparison-table)
24. [Exam-Style Questions](#24-exam-style-questions)
25. [Final Revision Points](#25-final-revision-points)
26. [Study Plan](#26-study-plan)

---

## 1. Introduction to Algorithms

### 1.1 What Is an Algorithm?

An algorithm is a well-defined, step-by-step computational procedure that takes input, processes it, and produces output in a finite amount of time.

```text
Input -> Algorithm -> Output
```

Example: find the largest number in an array.

```text
Input:  [4, 9, 2, 7]
Output: 9
```

The algorithm checks each number and keeps track of the largest value.

### 1.2 Important Features of an Algorithm

| Feature | Meaning |
| --- | --- |
| Finiteness | Must terminate after a finite number of steps |
| Definiteness | Each step must be clear and unambiguous |
| Input | Can have zero or more inputs |
| Output | Must produce at least one output |
| Effectiveness | Each operation must be simple and executable |

### 1.3 Why Study Algorithms?

Algorithms are important because they:

- Form the core of computer science.
- Help solve real-world problems efficiently.
- Reduce time and memory usage.
- Provide tools for designing better solutions.
- Can make a slower computer outperform a faster one if the algorithm is better.

Example: merge sort on a slower computer can beat insertion sort on a faster computer for large inputs because merge sort has better asymptotic complexity.

---

## 2. Algorithm Correctness

An algorithm is useful only if it is correct.

For every valid input, a correct algorithm must:

- Produce the correct output.
- Terminate.

### 2.1 Partial Correctness

If the algorithm terminates, the answer it gives is correct.

### 2.2 Termination

The algorithm must eventually stop.

### 2.3 GCD by Consecutive Integer Checking

Problem: find `gcd(m, n)`.

Algorithm:

```text
1. Let t = min(m, n)
2. Divide m by t
3. If m is divisible by t, divide n by t
4. If n is also divisible by t, return t
5. Otherwise, decrease t by 1 and repeat
```

Example:

```text
gcd(12, 30)
t = min(12, 30) = 12
```

Check values:

```text
30 mod 12 != 0
t = 11, 10, 9, 8, 7
```

When `t = 6`:

```text
12 mod 6 = 0
30 mod 6 = 0
```

Therefore:

```text
gcd(12, 30) = 6
```

This method terminates because `t` keeps decreasing and eventually reaches `1`, which divides every positive integer.

### 2.4 Euclid's Algorithm

Euclid's algorithm is a faster method for GCD.

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

Euclid's algorithm is a decrease-and-conquer algorithm because each step reduces the problem into a smaller version.

---

## 3. Complexity of Algorithms

Complexity measures how much resource an algorithm uses.

| Complexity Type | Meaning |
| --- | --- |
| Time complexity | How running time grows with input size |
| Space complexity | How memory usage grows with input size |

Actual clock time is not a reliable universal measure because it depends on:

- Computer speed
- Programming language
- Compiler or interpreter
- Operating system
- Other running programs

Therefore, we use asymptotic analysis, which measures running time as a function of input size `n`.

---

## 4. Best, Worst, and Average Case

For the same input size, different inputs may take different amounts of time.

Example: sequential search in an array of size `n`.

```text
A = [5, 8, 10, 15, 20]
```

| Case | Example | Comparisons | Complexity |
| --- | --- | ---: | --- |
| Best case | Search for `5` | 1 | O(1) |
| Worst case | Search for `20` | n | O(n) |
| Average case | Random item | n/2 | O(n) |

Worst-case analysis is commonly used because it gives an upper bound on running time.

---

## 5. Asymptotic Notation

Asymptotic notation describes how an algorithm grows when input size becomes large.

### 5.1 Big-O Notation

Big-O gives an upper bound.

```text
f(n) = O(g(n))
```

Meaning:

```text
f(n) <= c * g(n), for all n >= n0
```

where `c` and `n0` are positive constants.

Example: prove `2n^2 + 10 = O(n^2)`.

We need:

```text
2n^2 + 10 <= c n^2
```

Choose `c = 3`:

```text
2n^2 + 10 <= 3n^2
10 <= n^2
```

This is true when `n >= 4`.

Therefore:

```text
2n^2 + 10 = O(n^2)
```

### 5.2 Omega Notation

Omega gives a lower bound.

```text
f(n) = Omega(g(n))
```

Meaning: `f(n)` grows at least as fast as `g(n)`.

Example:

```text
10n^2 + 4n + 2 = Omega(n^2)
```

### 5.3 Theta Notation

Theta gives a tight bound.

```text
f(n) = Theta(g(n))
```

Meaning: `f(n)` grows at the same rate as `g(n)`.

Example:

```text
10n^2 + 4n + 2 = Theta(n^2)
```

because it is both:

```text
O(n^2)
Omega(n^2)
```

---

## 6. Common Growth Rates

From fastest to slowest:

```text
O(1) < O(log n) < O(n) < O(n log n) < O(n^2) < O(n^3) < O(2^n) < O(n!)
```

| Complexity | Name | Example |
| --- | --- | --- |
| O(1) | Constant | Access array element |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Sequential search |
| O(n log n) | Linearithmic | Merge sort |
| O(n^2) | Quadratic | Insertion sort worst case |
| O(n^3) | Cubic | Standard matrix multiplication |
| O(2^n) | Exponential | Naive Fibonacci |
| O(n!) | Factorial | Brute-force permutations |

---

## 7. Complexity Rules

### Rule 1: Ignore Constants

```text
O(5n) = O(n)
```

### Rule 2: Ignore Lower-Order Terms

```text
O(n^2 + n + 10) = O(n^2)
```

### Rule 3: Keep the Dominant Term

```text
O(3n^3 + 5n^2 + 7n + 4) = O(n^3)
```

---

## 8. Basic Complexity Examples

### 8.1 Constant Time

```text
Algorithm swap(a, b):
    temp = a
    a = b
    b = temp
```

The number of statements is constant.

```text
T(n) = O(1)
```

### 8.2 Linear Time

```text
sum = 0
for i = 1 to n:
    sum = sum + i
```

The loop runs `n` times.

```text
T(n) = O(n)
```

### 8.3 Quadratic Time

```text
for i = 1 to n:
    for j = 1 to n:
        print(i, j)
```

Total operations:

```text
n * n = n^2
```

Therefore:

```text
T(n) = O(n^2)
```

---

## 9. Sum of 1 to n

### Method 1: Loop Method

```text
sum = 0
for i = 1 to n:
    sum = sum + i
return sum
```

The loop runs `n` times.

```text
T(n) = O(n)
```

### Method 2: Formula Method

```text
return n(n + 1) / 2
```

Only one formula is calculated.

```text
T(n) = O(1)
```

Example: find the sum from `1` to `100`.

```text
n(n + 1) / 2
= 100(100 + 1) / 2
= 100 * 101 / 2
= 5050
```

So:

```text
1 + 2 + 3 + ... + 100 = 5050
```

---

## 10. Insertion Sort

Insertion sort builds the sorted array one element at a time.

### 10.1 Idea

At each step:

1. Take one element as the `key`.
2. Compare it with previous elements.
3. Shift larger elements to the right.
4. Insert `key` in the correct position.

### 10.2 Example

Sort:

```text
8 2 4 9 3 6
```

Step-by-step:

```text
Start:  8 2 4 9 3 6
Step 1: 2 8 4 9 3 6
Step 2: 2 4 8 9 3 6
Step 3: 2 4 8 9 3 6
Step 4: 2 3 4 8 9 6
Step 5: 2 3 4 6 8 9
```

Final sorted output:

```text
2 3 4 6 8 9
```

### 10.3 Complexity

| Case | Explanation | Complexity |
| --- | --- | --- |
| Best case | Already sorted array | O(n) |
| Worst case | Reverse sorted array | O(n^2) |
| Average case | Random order | O(n^2) |

### 10.4 Worst-Case Maths

For input size `n`, the number of comparisons or shifts is approximately:

```text
1 + 2 + 3 + ... + (n - 1)
```

Using the arithmetic series formula:

```text
(n - 1)n / 2
= (n^2 - n) / 2
```

The dominant term is `n^2`.

Therefore:

```text
T(n) = Theta(n^2)
```

---

## 11. Loop Invariant

A loop invariant is a condition that remains true before and after every loop iteration.

It is used to prove algorithm correctness.

For insertion sort:

```text
Before each iteration, the left part of the array is already sorted.
```

| Step | Meaning |
| --- | --- |
| Initialization | True before the first loop iteration |
| Maintenance | Remains true after each iteration |
| Termination | Helps prove final correctness |

---

## 12. Merge Sort

Merge sort is a divide-and-conquer sorting algorithm.

### 12.1 Main Idea

1. Divide the array into two halves.
2. Recursively sort both halves.
3. Merge the two sorted halves.

### 12.2 Example

Sort:

```text
8 2 4 9 3 6
```

Divide:

```text
[8 2 4]      [9 3 6]
[8] [2 4]    [9] [3 6]
```

Sort small parts:

```text
[2 4]        [3 6]
```

Merge:

```text
[2 4 8]      [3 6 9]
```

Final merge:

```text
[2 3 4 6 8 9]
```

### 12.3 Recurrence

```text
T(n) = 2T(n/2) + Theta(n)
```

| Part | Meaning |
| --- | --- |
| `2` | Two subproblems |
| `T(n/2)` | Each subproblem has size `n/2` |
| `Theta(n)` | Work needed to merge |

Using Master Theorem:

```text
a = 2
b = 2
f(n) = n
n^(log_b a) = n^(log_2 2) = n
```

Since `f(n) = Theta(n)`, this is Master Theorem Case 2.

Therefore:

```text
T(n) = Theta(n log n)
```

---

## 13. Recurrence Relations

A recurrence expresses the running time of a recursive algorithm in terms of smaller inputs.

Example:

```text
T(n) = 2T(n/2) + n
```

Meaning:

- The problem splits into 2 subproblems.
- Each subproblem has size `n/2`.
- Extra work outside recursion is `n`.

---

## 14. Solving Recurrences

### 14.1 Substitution Method

Steps:

1. Guess the answer.
2. Prove it using induction.
3. Solve constants.

Example:

```text
T(n) = T(n - 1) + 1
```

Expand:

```text
T(n)     = T(n - 1) + 1
T(n - 1) = T(n - 2) + 1
T(n - 2) = T(n - 3) + 1
```

So:

```text
T(n) = T(n - 3) + 3
```

After `n` steps:

```text
T(n) = T(0) + n
```

Therefore:

```text
T(n) = Theta(n)
```

### 14.2 Recursion Tree Method

Example:

```text
T(n) = 2T(n/2) + n
```

Level costs:

```text
Level 0: n
Level 1: n/2 + n/2 = n
Level 2: n/4 + n/4 + n/4 + n/4 = n
```

Number of levels:

```text
log_2 n
```

Total cost:

```text
n * log_2 n
```

Therefore:

```text
T(n) = Theta(n log n)
```

---

## 15. Divide and Conquer

Divide and conquer has three steps:

| Step | Meaning |
| --- | --- |
| Divide | Break problem into smaller subproblems |
| Conquer | Solve subproblems recursively |
| Combine | Combine subproblem answers |

Common examples:

- Merge sort
- Binary search
- Fast exponentiation
- Matrix multiplication
- Quicksort

---

## 16. Master Theorem

Master Theorem is used for recurrences of the form:

```text
T(n) = aT(n/b) + f(n)
```

| Symbol | Meaning |
| --- | --- |
| `a` | Number of subproblems |
| `n/b` | Size of each subproblem |
| `f(n)` | Work done outside recursive calls |

Let:

```text
p = log_b a
```

### Case 1: Recursive Work Dominates

If:

```text
f(n) = O(n^(p - epsilon))
```

Then:

```text
T(n) = Theta(n^p)
```

### Case 2: Work Is Balanced

If:

```text
f(n) = Theta(n^p log^k n)
```

Then:

```text
T(n) = Theta(n^p log^(k + 1)n)
```

### Case 3: Outside Work Dominates

If:

```text
f(n) = Omega(n^(p + epsilon))
```

Then:

```text
T(n) = Theta(f(n))
```

---

## 17. Binary Search

Binary search works only on a sorted array.

### 17.1 Idea

1. Check the middle element.
2. If the target is smaller, search the left half.
3. If the target is larger, search the right half.
4. Repeat.

### 17.2 Example

Array:

```text
3 5 7 8 9 12 15
```

Find:

```text
9
```

Steps:

```text
Middle = 8
9 > 8, so search right half: 9 12 15

Middle = 12
9 < 12, so search left half: 9

Found.
```

### 17.3 Recurrence

```text
T(n) = T(n/2) + Theta(1)
```

Using Master Theorem:

```text
a = 1
b = 2
f(n) = 1
n^(log_2 1) = n^0 = 1
```

Case 2:

```text
T(n) = Theta(log n)
```

---

## 18. Powering a Number

Problem:

```text
Compute a^n
```

### 18.1 Naive Method

```text
a * a * a * ... * a
```

Complexity:

```text
Theta(n)
```

### 18.2 Divide-and-Conquer Method

If `n` is even:

```text
a^n = a^(n/2) * a^(n/2)
```

If `n` is odd:

```text
a^n = a^((n - 1)/2) * a^((n - 1)/2) * a
```

Recurrence:

```text
T(n) = T(n/2) + Theta(1)
```

Therefore:

```text
T(n) = Theta(log n)
```

Example:

```text
2^8 = 2^4 * 2^4
2^4 = 2^2 * 2^2
2^2 = 2 * 2 = 4
2^4 = 4 * 4 = 16
2^8 = 16 * 16 = 256
```

---

## 19. Fibonacci Numbers

Definition:

```text
F0 = 0
F1 = 1
Fn = F(n - 1) + F(n - 2), for n >= 2
```

Sequence:

```text
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
```

### 19.1 Naive Recursive Fibonacci

```text
fib(n):
    if n == 0 return 0
    if n == 1 return 1
    return fib(n - 1) + fib(n - 2)
```

This is slow because it repeats many calculations.

```text
Complexity = exponential
```

### 19.2 Bottom-Up Fibonacci

```text
F0 = 0
F1 = 1

for i = 2 to n:
    Fi = F(i - 1) + F(i - 2)
```

Complexity:

```text
Theta(n)
```

Example: find `F6`.

```text
F0 = 0
F1 = 1
F2 = 1
F3 = 2
F4 = 3
F5 = 5
F6 = 8
```

---

## 20. Matrix Multiplication

Given two `n x n` matrices `A` and `B`, output matrix `C = A x B`.

Each element:

```text
c_ij = sum of a_ik * b_kj
```

### 20.1 Standard Matrix Multiplication

```text
for i = 1 to n:
    for j = 1 to n:
        for k = 1 to n:
            C[i][j] += A[i][k] * B[k][j]
```

Total operations:

```text
n * n * n = n^3
```

Therefore:

```text
T(n) = Theta(n^3)
```

### 20.2 Divide-and-Conquer Matrix Multiplication

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

Since `f(n) = Theta(n^2)` is smaller than `n^3`:

```text
T(n) = Theta(n^3)
```

So normal divide-and-conquer matrix multiplication is not asymptotically better than the standard algorithm.

### 20.3 Strassen's Algorithm

Strassen reduces recursive multiplications from `8` to `7`.

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

This is better than:

```text
Theta(n^3)
```

The difference matters because it is in the exponent.

---

## 21. Strassen Improvement Problem

Problem:

```text
T(n) = aT(n/4) + Theta(n^2)
```

Find the largest integer `a` so the algorithm is faster than Strassen's algorithm.

Strassen:

```text
T(n) = Theta(n^(log_2 7))
```

We need:

```text
log_4 a < log_2 7
```

Since:

```text
log_2 7 approx 2.807
```

Then:

```text
log_4 a < 2.807
a < 4^2.807
a < 49
```

Largest integer:

```text
a = 48
```

Answer:

```text
48
```

---

## 22. Quicksort

Quicksort is a divide-and-conquer sorting algorithm proposed by C. A. R. Hoare.

It is in-place and very practical with good tuning.

### 22.1 Main Idea

1. Choose a pivot.
2. Partition the array:
   - Elements smaller than the pivot go left.
   - Elements greater than the pivot go right.
3. Recursively sort the left and right parts.

### 22.2 Example

Array:

```text
8 2 4 9 3 6
```

Choose pivot:

```text
6
```

Partition:

```text
[2 4 3] 6 [8 9]
```

Sort left:

```text
[2 3 4]
```

Sort right:

```text
[8 9]
```

Final:

```text
2 3 4 6 8 9
```

### 22.3 Complexity

| Case | Complexity |
| --- | --- |
| Best case | Theta(n log n) |
| Average case | Theta(n log n) |
| Worst case | Theta(n^2) |

Worst case happens when the pivot always becomes the minimum or maximum element, such as with already sorted or reverse sorted input.

---

## 23. Algorithm Comparison Table

| Algorithm | Best Case | Average Case | Worst Case | Notes |
| --- | ---: | ---: | ---: | --- |
| Sequential search | O(1) | O(n) | O(n) | Works on unsorted arrays |
| Binary search | O(1) | O(log n) | O(log n) | Requires sorted array |
| Insertion sort | O(n) | O(n^2) | O(n^2) | Good for small or nearly sorted data |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | Stable and predictable |
| Quicksort | O(n log n) | O(n log n) | O(n^2) | Fast in practice |
| Standard matrix multiplication | O(n^3) | O(n^3) | O(n^3) | Three nested loops |
| Strassen | O(n^2.81) | O(n^2.81) | O(n^2.81) | Faster asymptotically |
| Bottom-up Fibonacci | O(n) | O(n) | O(n) | Avoids repeated recursion |
| Naive Fibonacci | Exponential | Exponential | Exponential | Very inefficient |

---

## 24. Exam-Style Questions

### Question 1

Find the Big-O of:

```text
f(n) = 5n^2 + 3n + 20
```

Answer:

```text
Dominant term = 5n^2
Ignore constants = n^2
f(n) = O(n^2)
```

### Question 2

Find the complexity:

```text
for i = 1 to n:
    print(i)
```

Answer:

```text
Loop runs n times.
T(n) = O(n)
```

### Question 3

Find the complexity:

```text
for i = 1 to n:
    for j = 1 to n:
        print(i, j)
```

Answer:

```text
Outer loop = n
Inner loop = n
Total = n * n = n^2
T(n) = O(n^2)
```

### Question 4

Solve:

```text
T(n) = 2T(n/2) + n
```

Answer:

```text
a = 2
b = 2
f(n) = n
n^(log_2 2) = n
Case 2
T(n) = Theta(n log n)
```

### Question 5

Solve:

```text
T(n) = T(n/2) + 1
```

Answer:

```text
a = 1
b = 2
f(n) = 1
n^(log_2 1) = 1
Case 2
T(n) = Theta(log n)
```

### Question 6

Solve:

```text
T(n) = 8T(n/2) + n^2
```

Answer:

```text
a = 8
b = 2
f(n) = n^2
n^(log_2 8) = n^3
n^2 is smaller than n^3
Case 1
T(n) = Theta(n^3)
```

### Question 7

Solve:

```text
T(n) = 7T(n/2) + n^2
```

Answer:

```text
a = 7
b = 2
f(n) = n^2
n^(log_2 7) approx n^2.81
n^2 is smaller than n^2.81
Case 1
T(n) = Theta(n^2.81)
```

### Question 8

Compare insertion sort and merge sort for large input.

Answer:

```text
Insertion sort worst case = Theta(n^2)
Merge sort worst case = Theta(n log n)

Since n log n grows slower than n^2,
merge sort is better for large input.
```

---

## 25. Final Revision Points

Remember:

```text
Algorithm = finite step-by-step solution
Complexity = resource usage growth
Big-O = upper bound
Omega = lower bound
Theta = tight bound
Worst case = most commonly analyzed
Divide and conquer = divide + conquer + combine
Recurrence = running time equation for recursion
Master Theorem = shortcut for divide-and-conquer recurrences
```

Most important formulas:

```text
1 + 2 + ... + n = n(n + 1) / 2

T(n) = aT(n/b) + f(n)

Merge sort:
T(n) = 2T(n/2) + n = Theta(n log n)

Binary search:
T(n) = T(n/2) + 1 = Theta(log n)

Insertion sort worst case:
Theta(n^2)

Standard matrix multiplication:
Theta(n^3)

Strassen:
Theta(n^2.81)
```

---

## 26. Study Plan

Study in this order:

1. Understand what an algorithm is.
2. Learn time complexity and Big-O.
3. Practice loop counting.
4. Learn insertion sort and merge sort.
5. Practice recurrence relations.
6. Learn Master Theorem.
7. Practice binary search, matrix multiplication, Strassen, and quicksort.

For exam preparation, focus heavily on:

```text
Big-O simplification
Loop complexity
Insertion sort analysis
Merge sort recurrence
Binary search recurrence
Master Theorem
Strassen recurrence
Quicksort best/average/worst case
```

