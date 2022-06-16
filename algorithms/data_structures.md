# Data structures

Overview:

- [Data Structure and Algorithms Tutorial](https://www.tutorialspoint.com/data_structures_algorithms/index.htm)
- [Recursion and stack](https://javascript.info/recursion)
- [trekhleb/javascript-algorithms](https://github.com/trekhleb/javascript-algorithms)

## Stack (LIFO)

- [Wikipedia](<https://en.wikipedia.org/wiki/Stack_(abstract_data_type)>)

### Operations

- push() − Pushing (storing) an element on the stack.
- pop() − Removing (accessing) an element from the stack.
- peek() − get the top data element of the stack, without removing it.
- isFull() − check if stack is full.
- isEmpty() − check if stack is empty.

## Queue (FIFO)

- [Wikipedia](<https://en.wikipedia.org/wiki/Queue_(abstract_data_type)>)

### Operations

- enqueue() − add (store) an item to the queue.
- dequeue() − remove (access) an item from the queue.
- peek() − Gets the element at the front of the queue without removing it.
- isfull() − Checks if the queue is full.
- isempty() − Checks if the queue is empty.

### Priority queue

- [Wikipedia](https://en.wikipedia.org/wiki/Priority_queue)

Each element in queue additionally has a "priority" associated with it. In a priority queue, an element with high
priority is served before an element with low priority.

## Linked list

- [Wikipedia](https://en.wikipedia.org/wiki/Linked_list)

### Node

- Element - holds the data of a node
- Next - holds the pointer to the next node

### List of nodes

- head - stores the first node of a list
- size indicates the number of nodes in a list

### Operations

- Insertion − Adds an element at the end of the list.
- Deletion − Deletes an element at the end of the list.
- Display − Displays the complete list.
- Search − Searches an element using the given key.
- Delete − Deletes an element using the given key.

### Traversal in Linked list

```js
// start out by looking at the first node
let current = this.head;

// follow `next` links until you reach the end
while (current.next !== null) {
  current = current.next;
}
```

## Hash table

- [Wikipedia](https://en.wikipedia.org/wiki/Hash_table)
- [Hash function](https://en.wikipedia.org/wiki/Hash_function)
- [hash collisions](<https://en.wikipedia.org/wiki/Collision_(computer_science)>)

A hash table (hash map) is a data structure that implements an associative array abstract data type, a structure that
can map keys to values and supports fast lookups. A hash table uses a hash function to compute an index, also called a
hash code, into an array of buckets or slots, from which the desired value can be found. During lookup, the key is
hashed and the resulting hash indicates where the corresponding value is stored.

Ideally, the hash function will assign each key to a unique bucket, but most hash table designs employ an imperfect hash
function, which might cause hash collisions where the hash function generates the same index for more than one key.

Search, Insert and delete operations:

Average: `O(1)`
Worst: `O(n)`

### Collision resolution

- Chaining with linked lists
- Open addressing with probing for next empty bucket

### Open addressing

Number of buckets n n should be roughly double the number of objects that you are storing and be a prime number

### Universal hashing

- [Wikipedia](https://en.wikipedia.org/wiki/Universal_hashing#:~:text=In mathematics and computing%2C universal,property (see definition below).)

Refers to selecting a hash function at random from a family of hash functions with a certain mathematical property. This
guarantees a low number of collisions in expectation.

## Graphs

- [Wikipedia](<https://en.wikipedia.org/wiki/Graph_(abstract_data_type)>)

Nodes = Vertices (n)
Edges (m)

### Undirected edge graphs

An undirected graph is a graph, i.e., a set of objects (n) that are connected together, where all the edges (m) are
bidirectional.

There are just two verses of edge. The two points say U and V and you don't distinguish one as the first and one as the
second.

### Directed edge graphs

A directed graph is a graph, i.e., a set of objects (n) that are connected together, where all the edges (m) are
directed from one vertex to another. You do have a notion of a first vertex or a first end point and the second vertex
or second end point of an edge.

Directed edges are called arcs.

### Sparse vs Dense graphs

- Sparse: m is close to `O(n)`
- Dense: m is close to `O(n^2)`

### Minimum cut

- [Wikipedia](https://en.wikipedia.org/wiki/Minimum_cut)

In graph theory, a minimum cut or min-cut of a graph is a cut (a partition of the vertices of a graph into two disjoint
subsets) that is minimal in some metric.

Variations of the minimum cut problem consider weighted graphs, directed graphs, terminals, and partitioning the
vertices into more than two sets.

The weighted min-cut problem allowing both positive and negative weights can be trivially transformed into a weighted
maximum cut problem by flipping the sign in all weights.
