# Types

## Overview

- [Built-in Types](https://docs.python.org/3/library/stdtypes.html)
- [Built-in Constants](https://docs.python.org/3/library/constants.html)
- [From library](https://speedsheet.io/s/python?select=T5aC)
- [Mutability](https://realpython.com/python-mutable-vs-immutable-types/)

### Standard Types

- `bool`: Boolean
- `int`: Integer
- `complex`: Complex Number
- `float`: Floating Point
- `str`: String
- `bytes`: [Byte](https://speedsheet.io/s/python?select=BF5h), creates a byte array
- `NoneType`: `None`, object representing the [absence of a value](https://speedsheet.io/s/python?select=UHpm)

### Sequence Types

- [Documentation](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range)

- `list`: List / Mutable Array
- `tuple`: Immutable Array
- `range` Immutable sequence of Integers

### Collections

- `dict`: Dictionary of Key Value Pairs
- `set` Mutable Set

## Type functions

Type inspection:

- `type()`

Type conversion:

- `int()`
- `float()`
- `str()`

## Comparisons

- [Documentation](https://docs.python.org/3/library/stdtypes.html#comparisons)
- [speedsheet.io](https://speedsheet.io/s/python?q=compar#KYLe)

Objects of different types, except different numeric types, never compare equal.

The `==` operator is for some object types (for example, class objects) equivalent to `is`.

`in` and `not in`, are supported by types that are iterable or implement the `__contains__()` method.

`string_1.casefold()`: Use this when you need to compare two strings but ignore the case (caseless). 

## Boolean 

- [SpeedSheet](https://speedsheet.io/s/python?q=boolean#qA4r)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#boolean-values)
- [Truth Value Testing](https://docs.python.org/3/library/stdtypes.html#truth)
- [Boolean Operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)

Functions:

- [bool()](https://docs.python.org/3/library/functions.html#bool): convert any value to a Boolean

## Numeric

- [Documentation](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)
- [Integer Operations](https://speedsheet.io/s/python?q=integer#u0H4)
- [Float Operations](https://speedsheet.io/s/python?q=float#b25U)

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

- [SpeedSheet](https://speedsheet.io/s/python?select=GQSJ)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)
- [Library](https://docs.python.org/3/library/string.html)
- [Formatted string literals](https://docs.python.org/3/reference/lexical_analysis.html#f-strings)
- [Operations](https://speedsheet.io/s/python?q=strings#T7xJ)

Strings can be enclosed in single quotes or double quotes with the same result.

## List

- [SpeedSheet](https://speedsheet.io/s/python?q=lis#Cn3A)
- [Documentation](https://docs.python.org/3/library/stdtypes.html#lists)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)
- [Operations](https://speedsheet.io/s/python?q=lis#hCt6)

An ordered list implemented as a fixed-length array of pointers. 
Lists are mutable sequences, typically used to store collections of homogeneous items.

All slice operations return a new list containing the requested elements. 

## Tuple

- [SpeedSheet](https://speedsheet.io/s/python?q=tuple#fHp3)
- [Python SpeedSheet](https://speedsheet.io/s/python?select=fHp3)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)

Type: `tuple`

Tuples are immutable arrays.

```python
= (value_1, value_2, ...)
```

## Range

- [SpeedSheet](https://speedsheet.io/s/python?q=range#S6GN)
- [Common Sequence Operations](https://docs.python.org/3/library/stdtypes.html#common-sequence-operations)

Type: `range`

- Range is an immutable sequence of integers.
- Range can be used anywhere a sequence can be used.

```python
= range(min, max_plus_1, step)
```

## Dictionary

- [SpeedSheet](https://speedsheet.io/s/python?select=BUXG)

Type: dict

- A collection of key value pairs.
- Keys can be any immutable type.
- Internally stored as a hash table.

```python
= {'key_1': 'value_1', 'key_2': 'value_2'...}
```

## Set

- [SpeedSheet](https://speedsheet.io/s/python?select=0RXJ)

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
