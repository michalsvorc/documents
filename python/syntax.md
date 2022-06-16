# Python syntax

- [Reserved words](https://docs.python.org/3/reference/lexical_analysis.html?highlight=reserved#keywords)
- [Language fundamentals](https://speedsheet.io/s/python?select=4pcY)
- [Operators](https://speedsheet.io/s/python?select=VbdZ)

Built-in:

- [Functions](https://docs.python.org/3/library/functions.html)
- [Types](https://docs.python.org/3/library/stdtypes.html)

## Overview

- Case sensitive.
- 4 spaces indent convention.
- Weakly typed.
- End-of-Line terminates a statement.
- Use a semicolon ';' to separate statements in one line.
- `self` is `this`.

## Comments

`#`: single line comment

There are no multiline comments in Python.

`"""Python Docstring."""`

## Operators

- [Python SpeedSheet](https://speedsheet.io/s/python?select=VbdZ)

Comparison operators:

```python
a is b
a is not b
```

Logical Operators:

```python
a and b
a or b
not b # Is Empty?
```

Is Between:

```python
= min < value < max
```

## Scope Levels

- Module
- Class
- Function
- Closure
- Generator Expression
- Comprehension

There is no block level scope.

## Global variables

```python
global name
```

Updates an existing global variable from inside a function. Without the keyword global, Python will create a local
variable.

## pass

Use as a placeholder in places where a code block should exist but you don't have any code yet.
