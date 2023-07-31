# Types

## Overview

- [Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- [Built-in Constants](https://docs.python.org/3/library/constants.html)
- [speedsheet](https://speedsheet.io/s/python?select=T5aC)
- [Mutability](https://realpython.com/python-mutable-vs-immutable-types/)

### Standard Types

- `bool`: Boolean
- `int`: Integer
- `complex`: Complex Number
- `float`: Floating Point
- `str`: String, Immutable sequence of characters
- `bytes`: [Byte](https://speedsheet.io/s/python?select=BF5h), creates a byte array
- `NoneType`: `None`, object representing the [absence of a value](https://speedsheet.io/s/python?select=UHpm)

### Sequence Types

- [Documentation](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)
- [Python tutorial](https://www.pythontutorial.net/advanced-python/python-sequences/)

A sequence is a positionally ordered collection of items. You can refer to any item in the sequence by using its index number.

In Python, the sequence index starts at 0.

A sequence can be homogeneous or heterogeneous. In general, homogeneous sequence types are more efficient than heterogeneous in terms of storage and operations.

- `list`: Mutable Array 
- `tuple`: Immutable Array
- `range`: Immutable sequence of Integers

### Collections

- `dict`: Dictionary of Key Value Pairs
- `set` Mutable Set

## Iterables

- [Glossary](https://docs.python.org/3/glossary.html#term-iterable)
- [Python tutorial](https://www.pythontutorial.net/python-basics/python-iterables/)
- [Real Python](https://realpython.com/python-iterators-iterables/)

An object capable of returning its members one at a time.
Iterables can be used in a `for` loop and in many other places where a sequence is needed.

Any sequence is iterable. For example, a `list` is iterable.
However, an iterable may not be a sequence type. For example, a `set` is iterable but it’s not a sequence (it's a collection).

Generally speaking, iterables are more general than sequence types.

## Iterators

- [Glossary](https://docs.python.org/3/glossary.html#term-iterator)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#iterator-types)

When an iterable object is passed as an argument to the built-in function `iter()`, it returns an iterator for the object.

## Type functions

Type inspection:

- `type()`

Type conversion:

- `int()`
- `float()`
- `str()`

## Comparisons

- [Documentation](https://docs.python.org/3/library/stdtypes.html#comparisons)
- [speedsheet](https://speedsheet.io/s/python?q=compar#KYLe)
- [Comparing Sequences and Other Types](https://docs.python.org/3/tutorial/datastructures.html#comparing-sequences-and-other-types)

Objects of different types, except different numeric types, never compare equal.

The `==` operator is for some object types (for example, class objects) equivalent to `is`.

`in` and `not in`, are supported by types that are iterable or implement the `__contains__()` method.

`string_1.casefold()`: Use this when you need to compare two strings but ignore the case (caseless). 


## Boolean 

- [speedsheet](https://speedsheet.io/s/python?q=boolean#qA4r)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#boolean-values)
- [Truth Value Testing](https://docs.python.org/3/library/stdtypes.html#truth)
- [Boolean Operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)

Functions:

- [bool()](https://docs.python.org/3/library/functions.html#bool): convert any value to a Boolean

## Numeric

- [Documentation](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)
- [Integer Operations | speedsheet](https://speedsheet.io/s/python?q=integer#u0H4)
- [Float Operations | speedsheet](https://speedsheet.io/s/python?q=float#b25U)

- `int`: [Integer](https://speedsheet.io/s/python#f3Sf)
- `float`: [Floating Point](https://speedsheet.io/s/python?select=R2Pv)
- `complex`: [Complex Number](https://speedsheet.io/s/python?select=0C9U)
- `Decimal`
- `Fraction`

Division always returns a floating point number:

```python
8 / 4  # 2.0 
```

## Strings

- [speedsheet](https://speedsheet.io/s/python?select=GQSJ)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
- [Library](https://docs.python.org/3/library/string.html)
- [Formatted string literals](https://docs.python.org/3/reference/lexical_analysis.html#f-strings)
- [Operations | speedsheet](https://speedsheet.io/s/python?q=strings#T7xJ)

Strings can be enclosed in single quotes or double quotes with the same result.

## List

- [speedsheet](https://speedsheet.io/s/python#Cn3A)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#lists)
- [Real Python](https://realpython.com/python-list/)

Lists are `mutable` arrays.


```python
class list([iterable])
l = [...]
```

An ordered list implemented as a fixed-length array of pointers. 

Lists are **mutable** sequences, typically used to store collections of homogeneous items (where the precise degree of similarity will vary by application).

### List Operations

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)
- [Mutable Sequence Operations](https://docs.python.org/3/library/stdtypes.html#typesseq-mutable)
- [Operations | speedsheet](https://speedsheet.io/s/python#hCt6)

All slice operations return a new list containing the requested elements. 

Methods like `insert`, `remove` or `sort` that only modify the list have no return value printed – they return the default `None`. This is a design principle for all mutable data structures in Python.

Not all data can be sorted or compared. For instance, `[None, 'hello', 10]` doesn’t sort because integers can’t be compared to strings and `None` can’t be compared to other types.

### List Comprehension

- [Wikipedia](https://en.wikipedia.org/wiki/List_comprehension)
- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)

A list comprehension consists of brackets containing an expression followed by a `for` clause, then zero or more `for` or `if` clauses.
The result will be a new list resulting from evaluating the expression in the context of the `for` and `if` clauses which follow it.

```python
squares = [x**2 for x in range(10)]
```

List comprehensions provide a concise way to create lists. Common applications are to make new lists where each element is the result 
of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition.

## Tuple

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences)
- [speedsheet](https://speedsheet.io/s/python?q=tuple#fHp3)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#tuple)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)
- [namedtuple](https://docs.python.org/3/library/collections.html#collections.namedtuple)

Tuples are `immutable` arrays.

```python
class tuple([iterable])
t = (...)
```

A special problem is the construction of tuples containing 0 or 1 items: the syntax has some extra quirks to accommodate these:

```python
empty = ()
singleton = 'hello',    # <-- note trailing comma
```

### Tuple compared to list

- [Python tutorial](https://www.pythontutorial.net/advanced-python/python-tuple-vs-list/)

- A tuple is immutable while a list is mutable.
- The storage efficiency of a tuple is greater than a list.
- Copying a tuple is slightly faster than a list.
- Use a tuple if you don’t intend to mutable it.

## Range

- [speedsheet](https://speedsheet.io/s/python?q=range#S6GN)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)

```python
class range(stop)
class range(start, stop[, step])
```

- Range is an immutable sequence of integers.
- Range can be used anywhere a sequence can be used.

## Set

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#sets)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset)
- [speedsheet](https://speedsheet.io/s/python?select=0RXJ)

A set object is an unordered collection of distinct hashable objects. 

```python
class set([iterable])
s = {...}
```

Common uses include membership testing, removing duplicates from a sequence, 
and computing mathematical operations such as intersection, union, difference, and symmetric difference.

Being an unordered collection, sets do not record element position or order of insertion.
Accordingly, sets do not support indexing, slicing, or other sequence-like behavior.

Since it is mutable, it has no hash value and cannot be used as either a dictionary key or as an element of another set. 

To represent sets of sets, the inner sets must be `frozenset` objects.

To create an empty set you have to use `set()`, not `{}`;

Both set and frozenset support set to set comparisons. Two sets are equal if and only if every element of each set is contained in the other (each is a subset of the other). 

### Frozenset

- [Documentation](https://docs.python.org/3/library/stdtypes.html#frozenset)

The frozenset type is immutable and hashable — its contents cannot be altered after it is created; it can therefore be used as a dictionary key or as an element of another set.

```python
class frozenset([iterable])
```

## Dictionary

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#dictionaries)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#typesmapping)
- [speedsheet](https://speedsheet.io/s/python?select=BUXG)

A mapping object maps hashable values to arbitrary objects. Mappings are mutable objects. 

```python
class dict(**kwargs)
class dict(mapping, **kwargs)
class dict(iterable, **kwargs)
d = {'key_1': 'value_1', 'key_2': 'value_2', ...}
```

Dictionaries are indexed by keys, which can be any immutable type

Internally stored as a hash table.

Getting a value if key is not in the map raises a `KeyError`. To check whether a single key is in the dictionary, use the `in` keyword.

Dictionaries compare equal if and only if they have the same (key, value) pairs (regardless of ordering).

- Changed in version 3.7: Dictionary order is guaranteed to be insertion order.
- Changed in version 3.8: Dictionaries are now reversible.

### Dictionary view objects

- [MappingProxyType](https://docs.python.org/3/library/types.html#types.MappingProxyType)

The objects returned by `dict.keys()`, `dict.values()` and `dict.items()` are view objects.
They provide a dynamic view on the dictionary’s entries, which means that when the dictionary changes, the view reflects these changes.

`types.MappingProxyType` can be used to create a read-only view of a dict.

## Abstract data types

### Stack

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#using-lists-as-stacks)

The list methods make it very easy to use a list as a stack, where the last element added is the first element retrieved (“last-in, first-out”).

To add an item to the top of the stack, use `append()`. To retrieve an item from the top of the stack, use `pop()` without an explicit index.

### Queue

- [Tutorial](https://docs.python.org/3/library/collections.html#collections.deque)

It is also possible to use a list as a queue, where the first element added is the first element retrieved (“first-in, first-out”); however, lists are not efficient for this purpose.

## The del statement

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#the-del-statement)
- [Reference](https://docs.python.org/3/reference/simple_stmts.html#del)
- [Real Python](https://realpython.com/python-del-statement/)

Remove an item from a list given its index instead of its value.

## Sequence packing and unpacking

- [Tutorial](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences)

Tuple packing:

`t = 12345, 54321, 'hello!'`

Sequence unpacking

`x, y, z = t`

