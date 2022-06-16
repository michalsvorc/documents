# Searching

## Breadth-first search (BFS)

- [Wikipedia](https://en.wikipedia.org/wiki/Breadth-first_search)

It starts at the tree root (or some arbitrary node of a graph, sometimes referred to as a 'search key'), and explores
all of the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.

Can compute shortest path distances.

## Depth-first search (DFS)

- [Wikipedia](https://en.wikipedia.org/wiki/Depth-first_search)

The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and
explores as far as possible along each branch before backtracking.

## Binary search

- [Wikipedia](https://en.wikipedia.org/wiki/Binary_search_algorithm)

`O(log n)`

Binary search works on _sorted arrays_. Binary search begins by comparing an element in the middle of the array with the
target value. If the target value matches the element, its position in the array is returned. If the target value is
less than the element, the search continues in the lower half of the array.

If the target value is greater than the element, the search continues in the upper half of the array. By doing this, the
algorithm eliminates the half in which the target value cannot lie in each iteration.
