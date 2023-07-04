# Functions

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [Built-in Functions](https://docs.python.org/3/library/functions.html)
- [Functions | speedsheet](https://speedsheet.io/s/python#Vuqm)
- [Closure | speedsheet](https://speedsheet.io/s/python#vbfK)
- [Decorators | speedsheet](https://speedsheet.io/s/python?select=YaLr)

## Overview

- We define a function using the `def` keyword.
- Functions are stored as global attributes.
- Functions are first class objects and can be passed as values.
- `__name__` property holds function name.
- Functions without a return statement return `None` value.

## Default arguments

- The arguments with default values are optional.
- Optional arguments must come after standard non-optional arguments.
- The default value is evaluated only once. This makes a difference when the default 
  is a mutable object such as a list, dictionary, or instances of most classes.

## Named arguments

- Pass arguments by name to by using the form name = value.
- Order is not important.

```python
def greet(greeting, name):
	print(greeting, name)

greet(name = 'John', greeting = 'Hi')
```

## Keyword arguments

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#keyword-arguments)
- [Documentation](https://docs.python.org/3/glossary.html#term-argument)

- Arguments as Key Word Dictionary.
- The caller arguments are placed in a dictionary.
- The caller must use named arguments.
- kwargs (key word arguments) is the name by convention for this argument.

Definition:

`kwargs Type: dict`

```python
def say(**kwargs):
	print(kwargs['greeting'], kwargs['name'])

say(greeting = "Hi", name = "John")
```

Unpacking keyword arguments:

```python
def say(greeting, name):
	print(greeting, name)

dict_1 = {'greeting' : 'Hi', 'name' : 'John'}

say(**dict_1)
```

## Positional arguments

- [Documentation](https://docs.python.org/3/glossary.html#term-argument)

- Arguments as Sequence.

Definition:

`args Type: tuple`

```python
def say(*args):
	print(args[0], args[1])

say("Hi", "John")
```

Unpacking positional arguments:

```python
def say(greeting, name):
	print(greeting, name)

list_1 = ['Hi', 'John']

say(*list_1)
```

### Variadic arguments

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#arbitrary-argument-lists)

- Specify that a function can be called with an arbitrary number of arguments.

```python
def write_multiple_items(file, separator, *args):
    file.write(separator.join(args))
```

## Order of the arguments

```python
def f(arg, *args, **kwargs):
```

### Special parameters

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#special-parameters)

```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):

# Positional only / Positional or keyword * Keyword only
```

`/` and `*` are optional. If used, these symbols indicate the kind of parameter by how the arguments may be passed to the function.
If `/` and `*` are not present in the function definition, arguments may be passed to a function by position or by keyword.

## Return multiple values as Tuple

```python
def function_1():
	return value_1, value_2, ...
```

## Lambda expressions

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions)
- [Documentation](https://docs.python.org/3/reference/expressions.html#lambda)
- [speedsheet](https://speedsheet.io/s/python#x8x6)

- Small anonymous functions can be created with the `lambda` keyword. 
- All lambdas return a value. Returns are implied.

Definition:

```python
lambda arg_1, arg_2, ... : expression
```

Definition using the standard function form to return a 'lambda':

```python
def make_incrementor(n):
    return lambda x: x + n`

f = make_incrementor(42)
f(1) # 43
```
