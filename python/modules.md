# Modules

- [Modules](https://docs.python.org/3/tutorial/modules.html#packages)
- [Real Python](https://realpython.com/python-modules-packages/)
- [speedsheet](https://speedsheet.io/s/python?q=modules#w9zp)
- [site](https://docs.python.org/3/library/site.html#module-site)

## Wheel: Application distribution

- [Python wheels](https://realpython.com/python-wheels/)
- [speedsheet](https://speedsheet.io/s/python#Th7c)

Wheel is currently considered the standard for built and binary packaging for Python.

## PIP: Package manager

- [speedsheet](https://speedsheet.io/s/python?select=aTYy)

PIP can create requirements file from installed packages and install all the packages in the requirements file.

Any time you’re working on a Python project that uses external dependencies that you’re installing with pip, it’s best to first create a virtual environment.

## Namespaces

- [Python Scopes and Namespaces](https://docs.python.org/3/tutorial/classes.html#tut-scopes)

Within a module, the module’s name (as a string) is available as the value of the global variable `__name__`.

Each module has its own private namespace, which is used as the global namespace by all functions defined in the module.

A module can use global variables in the module without worrying about accidental clashes with a user’s global variables.

## Imports

- [importlib](https://docs.python.org/3/library/importlib.html#importlib.reload)
- [Python Imports](https://docs.python.org/3/reference/import.html)

Import statement that imports names from a module directly into the importing module’s namespace.

```python
from fibo import fib, fib2
fib(100)

# with as
import fibo as fib
fib.fib(100)

from fibo import fib as fibonacci
fibonacci(100)
```

`from fibo import *` imports all names except those beginning with an underscore (\_).
In most cases Python programmers do not use this facility since it introduces an unknown set of names into the interpreter.

You can reload module import in current interpreter with `importlib.reload`, e.g. when testing a modified module.

## Executing modules as scripts

```python
python fibo.py <arguments>
```

The code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`.

### Scripts

- [Python Scripts](https://docs.python.org/3/tutorial/modules.html#executing-modules-as-scripts)

You can make the file usable as a script as well as an importable module.

This is often used either to provide a convenient user interface to a module, or for testing purposes (running the module as a script executes a test suite).

When you run a Python module with

```python
python <filename>.py <arguments>
```

the `__name__` is set to `"__main__"`:

```python
if __name__ == "__main__":
    import sys
    print(sys.argv[1:])
```

This part of the code will be executed when the module is run as a script.
