# Modules

- [Modules](https://docs.python.org/3/tutorial/modules.html#packages)
- [Real Python](https://realpython.com/python-modules-packages/)
- [speedsheet](https://speedsheet.io/s/python?q=modules#w9zp)

## Wheel: Application distribution

- [Python wheels](https://realpython.com/python-wheels/)
- [speedsheet](https://speedsheet.io/s/python#Th7c)

Wheel is currently considered the standard for built and binary packaging for Python.

## PIP: Package manager

- [speedsheet](https://speedsheet.io/s/python?select=aTYy)

PIP can create requirements file from installed packages and install all the packages in the requirements file.

## Virtual environments

- [Real Python](https://realpython.com/python-virtual-environments-a-primer)

Python virtual environment is a folder structure that gives you everything you need to run a lightweight yet isolated Python environment.

Use virtual environments for every project to:

- Avoid System Pollution
- Sidestep Dependency Conflicts
- Minimize Reproducibility Issues
- Dodge Installation Privilege Lockouts

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

`from fibo import *` imports all names except those beginning with an underscore (_).
In most cases Python programmers do not use this facility since it introduces an unknown set of names into the interpreter.

You can reload module import in current interpreter with `importlib.reload`, e.g. when testing a modified module.

## Executing modules as scripts

```python
python fibo.py <arguments>
```

The code in the module will be executed, just as if you imported it, but with the `__name__` set to `"__main__"`.

you can make the file usable as a script as well as an importable module, based on the following:

```python
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```

