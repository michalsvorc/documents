# Asymptotic analysis

Overview:

- [Analysis of Algorithms](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/)
- [Understanding Logarithms and Roots | by Brett Berry | Math Hacks](https://medium.com/i-math/understanding-logarithms-and-roots-2fee92c3317f)
- [Polynom](https://cs.wikipedia.org/wiki/Polynom)
- [(Video) Asymptotic Bounding 101](https://www.youtube.com/watch?v=0oDAlMwTrLo)
- [Algorithm Complexity](https://www.bigocheatsheet.com/)

## Notations

- Big Omega - lower bound
- Theta - tight (exact) bound
- Big O - upper bound

### Big O notation

- [(Video) Big O notation in 5 minutes](https://www.youtube.com/watch?v=__vX2sjlpXU)
- [(Video) Beginner's Guide to Big O Notation](https://www.youtube.com/watch?v=kS_gr2_-ws8)

In Asymptotic Analysis, we evaluate the performance of an algorithm in terms of input size (we don't measure the actual
running time). We calculate how the time (or space) taken by an algorithm increases with the input size.

Suppress both leading constant factors (too system/language dependent) and lower order terms (irrelevant for large
inputs). We're interested in "tail behaviour" lines, not their exact positions relative to x and y axis.

`log2n` is a factor in O notation whenever we're _halving_ (dividing by 2) the input (e.g. merge sort).

## Linear time algorithm

An algorithm whose number of instructions grows proportional to the input size.

`O(n)`

Always simplify to worst case scenario.

`O(logn) + O(n) = O(n)`
`O(n) + O(n) = O(n)`
`O(n) + O(n^2) = O(n2)`

## Divide and conquer paradigm

1. Divide into smaller sub-problems
2. Conquer via recursive calls
3. Combine the solutions to the subproblem into one problem

### Merge sort example

`O(n*log n)`

- we divide a number into half in every step = `log n`
- to merge the subarrays, made by dividing the original array of `n` elements, a running time of `O(n)` will be required.
- Hence the total time for mergeSort function will become `O(n*log n)`.

## Master theorem

- [Wikipedia](<https://en.wikipedia.org/wiki/Master_theorem_(analysis_of_algorithms)>)

In the analysis of algorithms, the master theorem for divide-and-conquer recurrences provides an asymptotic analysis
(using Big O notation) for recurrence relations of types that occur in the analysis of many divide and conquer
algorithms.
