# Types

## Overview

- [Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- [Built-in Constants](https://docs.python.org/3/library/constants.html)
- [From library](https://speedsheet.io/s/python?select=T5aC)

### Standard Types

- `bool`: [Boolean](https://speedsheet.io/s/python?q=boolean#qA4r) constant objects `False` and `True`, used to represent truth values
- `int`: [Integer](https://speedsheet.io/s/python?select=CPVx)
- `complex`: [Complex Number](https://speedsheet.io/s/python?select=0C9U)
- `float`: [Floating Point](https://speedsheet.io/s/python?select=R2Pv)
- `str`: [String](https://speedsheet.io/s/python?select=GQSJ)
- `bytes`: [Byte](https://speedsheet.io/s/python?select=BF5h), creates a byte array
- `NoneType`: `None`, object representing the [absence of a value](https://speedsheet.io/s/python?select=UHpm)

Sequence Types:

- `list` (List / Mutable Array)
- `tuple` (Immutable Array)
- `range` (Immutable Integers)

Collections:

- `dict` (Dictionary of Key Value Pairs)
- `set` (Mutable Set)
- `frozenset` (Immutable Set)

## Mutability

### Mutable Types

- bytearray
- classes
- class instances
- dict
- list
- set

### Immutable Types

- boolean
- byte
- float
- frozenset
- int
- complex
- str
- tuple

## Type functions

Type inspection:

- type()

Type conversion:

- int()
- float()
- str()

## Boolean 

- [Documentation](https://docs.python.org/3/library/stdtypes.html#boolean-values)
- [Truth Value Testing](https://docs.python.org/3/library/stdtypes.html#truth)
- [Boolean Operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)

Functions:

- [bool()](https://docs.python.org/3/library/functions.html#bool): convert any value to a Boolean

## List

- [Python SpeedSheet](https://speedsheet.io/s/python?select=Cn3A)

An ordered list implemented as a fixed-length array of pointers.

```python
= [value_1, value_2, ...]
```

Return elements in range, including element at index postion `n`:

```python
list_1[n:m]
list_1[n:]
list_1[:n]
```

## Tuple

- [Python SpeedSheet](https://speedsheet.io/s/python?select=fHp3)

Type: `tuple`

Tuples are immutable arrays.

```python
= (value_1, value_2, ...)
```

## Range

- [Python SpeedSheet](https://speedsheet.io/s/python?select=S6GN)

Type: `range`

- Range is an immutable sequence of integers.
- Range can be used anywhere a sequence can be used.

```python
= range(min, max_plus_1, step)
```

## Dictionary

- [Python SpeedSheet](https://speedsheet.io/s/python?select=BUXG)

Type: dict

- A collection of key value pairs.
- Keys can be any immutable type.
- Internally stored as a hash table.

```python
= {'key_1': 'value_1', 'key_2': 'value_2'...}
```

## Set

- [Python SpeedSheet](https://speedsheet.io/s/python?select=0RXJ)

- Unordered group of unique items.
- Contains no duplicates.

```python
= {value_1, value_2, ...}
```

### Frozenset

- [Documentation](https://docs.python.org/3/library/stdtypes.html#frozenset)

The Python `frozenset()` method returns a new frozenset object whose elements are taken from the passed iterable.

If iterable is not specified, a new empty set is returned.

Note: The elements must be hashable.
