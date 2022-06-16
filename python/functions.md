# Functions

- [Built-in Functions](https://docs.python.org/3/library/functions.html)
- [Functions](https://speedsheet.io/s/python?select=EE7Q)
- [Closure](https://speedsheet.io/s/python?select=FFTh)
- [Decorators](https://speedsheet.io/s/python?select=YaLr)

- We define a function using the `def` keyword.
- Functions are stored as global attributes.
- Functions are first class objects and can be passed as values.
- `__name__` property holds function name.

```python
def function_1(arg_1, arg_2 ...):
    """Function docstring."""
    ...
    return response
```

## Default arguments

- The arguments with default values are optional.
- Optional arguments must come after standard non-optional arguments.

```python
def function_1(optional_arg_1 = default_value, ...):
    ...
```

## Named arguments

- Pass arguments by name to by using the form name = value.
- Order is not important.

```python
def greet(greeting, name):
	print(greeting, name)

# Call:

greet(name = 'John', greeting = 'Hi')
```

## Arguments as Key Word Dictionary

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

Call:

```python
def say(greeting, name):
	print(greeting, name)

dict_1 = {'greeting' : 'Hi', 'name' : 'John'}

say(**dict_1)
```

## Arguments as Sequence

Definition:

`args Type: tuple`

```python
def say(*args):
	print(args[0], args[1])

say("Hi", "John")
```

Call:

```python
def say(greeting, name):
	print(greeting, name)

list_1 = ['Hi', 'John']

say(*list_1)
```

## Return multiple values as Tuple

```python
def function_1():
	return value_1, value_2, ...
```

## Inner Functions (Closure)

- An inner function has read access to it's parent's variables.
- There are in scope due to the function 'closing' over the parent's environment.

## Lambda expressions

- [Lambda](https://docs.python.org/3.8/reference/expressions.html#lambda)
- [Lambda expressions](https://docs.python.org/3.8/tutorial/controlflow.html#lambda-expressions)
- [Python SpeedSheet](https://speedsheet.io/s/python?select=x8x6)

- Lambda expressions (sometimes called lambda forms) are used to create anonymous functions.
- All lambdas return a value. Returns are implied.

Definition:

```python
lambda arg_1, arg_2, ... : expression
```

Definition using the standard function form to return a 'lambda':

```python
def lambda_name(args_1, args_2, ...): return expression
```

Example:

```python
multiply = lambda x, y : x * y

result = multiply(2, 3)
```
