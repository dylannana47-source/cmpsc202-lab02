# Lab 02: Asymptotic Analysis and Algorithm Running Times

Work with your Project 1 team to complete the exercises found in `exercises.pdf`. Put your solutions and explanations below. When you are finished, commit and push your repo.

I worked through each proof and algorithm carefully, focusing on the dominant growth term in each case.

# Part 1:

## Problem 1.1
We want to prove that

T(n) = 3n^2 + 15n + 100

is O(n^2).

For all n >= 1, we know that n <= n^2 and 1 <= n^2. Therefore:

15n <= 15n^2
100 <= 100n^2

So:

T(n) = 3n^2 + 15n + 100
     <= 3n^2 + 15n^2 + 100n^2
     = 118n^2

Thus, for c = 118 and n0 = 1,

T(n) <= c n^2 for all n >= n0.

So T(n) is O(n^2).

This works because the quadratic term dominates the linear and constant terms once n is large enough.

Rules used:
- Polynomial growth: n <= n^2 for n >= 1
- Constant terms are dominated by polynomial terms
- Dropping multiplicative constants

## Problem 1.2
We want to prove that

T(n) = 4 * 2^n + 8n^5

is O(2^n).

The exponential function grows faster than any polynomial, so for sufficiently large n,

n^5 <= 2^n.

For example, this is true for all n >= 32. So for n >= 32:

T(n) = 4 * 2^n + 8n^5
     <= 4 * 2^n + 8 * 2^n
     = 12 * 2^n

Thus, for c = 12 and n0 = 32,

T(n) <= c * 2^n for all n >= n0.

Therefore T(n) is O(2^n).

Rules used:
- Exponential is faster than polynomial
- Dropping multiplicative constants
- Summation is a max

# Part 2:

## Algorithm A
We count the exact number of operations in the worst case.

function algoA(n):
count = 0
for i = 1 to n:
    print(i)
    for j = 1 to n:
        for k = 1 to n:
            count = count + 1
return count

The outer loop runs n times. Inside it, the print statement runs n times total. The two nested loops together run n * n * n = n^3 times. So the exact total is:

T(n) = 1 + n + n^3 + 1
    = n^3 + n + 2

The tightest Big-O bound is:

T(n) = O(n^3)

## Algorithm B
function algoB(n):
val = n
steps = 0
while val >= 1:
    val = val / 2
    steps = steps + 1
print("Processing steps: ", steps)

Each iteration divides val by 2. If the loop runs m times, then the value is roughly n / 2^m. The loop stops when val < 1, which happens after about log2(n) iterations. So the number of loop iterations is proportional to log2(n).

Examples:
- n = 8: 8 -> 4 -> 2 -> 1 -> 0.5, so 4 iterations
- n = 16: 16 -> 8 -> 4 -> 2 -> 1 -> 0.5, so 5 iterations
- n = 32: 32 -> 16 -> 8 -> 4 -> 2 -> 1 -> 0.5, so 6 iterations

This matches log2(n) behavior. The exact count is approximately:

T(n) = O(log n)

The reason is that each pass halves the value, so the number of passes needed to reach 1 grows only with the base-2 logarithm of n.

# Part 3:

## Reflection
The rule that feels least intuitive to me is the rule that exponential growth is faster than polynomial growth. It is hard to believe at first, but once n becomes large enough, 2^n grows much faster than n^5.

I found the while-loop analysis in Algorithm B the most challenging because the exact number of iterations depends on repeated division by 2, which is closely related to logarithms.

I think the exercises were helpful because they made the concepts more concrete. The examples in the problem statement were especially useful for understanding how repeated halving connects to log2(n), and they helped connect the theory to how algorithms actually behave as n grows.