# Sorting

## Merge sort

- [Wikipedia](https://en.wikipedia.org/wiki/Merge_sort)

`O(n log n)`

1. Divide the unsorted list into `n` sublists, each containing one element (a list of one element is considered sorted).
2. Repeatedly [merge](https://en.wikipedia.org/wiki/Merge_algorithm) sublists to produce new sorted sublists until there
   is only one sublist remaining. This will be the sorted list.

## Quick sort

- [Wikipedia](https://en.wikipedia.org/wiki/Quicksort)

`O(n)`, average `O(logn)`

It works by selecting a _pivot_ element from the array and partitioning the other elements into two sub-arrays,
according to whether they are less than or greater than the pivot.

The best case is when the algorithm always picks the median as a pivot, in the worst case the min or the max is always
chosen as the pivot, resulting in linear depth.

## Selection sort

- [Wikipedia](https://en.wikipedia.org/wiki/Selection_sort)

`O(n2)`

The algorithm divides the input list into two parts: a sorted sublist of items which is built up from left to right at
the front (left) of the list and a sublist of the remaining unsorted items that occupy the rest of the list.

Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. The algorithm proceeds by
finding the smallest (or largest, depending on sorting order) element in the unsorted sublist, exchanging (swapping) it
with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the
right.

## Insertion sort

- [Wikipedia](https://en.wikipedia.org/wiki/Insertion_sort)

`O(n2)`

Insertion sort iterates, consuming one input element each repetition, and grows a sorted output list. At each iteration,
insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and
inserts it there. It repeats until no input elements remain.

Sorting is typically done in-place, by iterating up the array, growing the sorted list behind it. At each
array-position, it checks the value there against the largest value in the sorted list (which happens to be next to it,
in the previous array-position checked). If larger, it leaves the element in place and moves to the next. If smaller, it
finds the correct position within the sorted list, shifts all the larger values up to make a space, and inserts into
that correct position.

## Bubble sort

- [Wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)

`O(n2)`

Bubble sort, sometimes referred to as sinking sort, is a simple sorting algorithm that repeatedly steps through the
list, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated
until the list is sorted. The algorithm, which is a comparison sort, is named for the way smaller or larger elements
"bubble" to the top of the list.

This simple algorithm performs poorly in real world use and is used primarily as an educational tool.
