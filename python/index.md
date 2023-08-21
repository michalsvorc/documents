# Python

Overview:

- [Tutorial](https://docs.python.org/3/tutorial/index.html)
- [Standard Library](https://docs.python.org/3/library/index.html)
- [Glossary](https://docs.python.org/3/glossary.html)

Resources:

- [Awesome Python](https://github.com/vinta/awesome-python)
- [Legally Free Python Books List](https://www.pythonkitchen.com/legally-free-python-books-list/)
- [speedsheet](https://speedsheet.io/s/python)
- [Real Python](https://realpython.com/)

Tools:

- [Jupyter Docker Stacks](https://github.com/jupyter/docker-stacks)

## Style conventions

- [Coding Style](https://docs.python.org/3/tutorial/controlflow.html#intermezzo-coding-style)
- [Documentation Strings](https://docs.python.org/3/tutorial/controlflow.html#documentation-strings)
- [Function Anntotations](https://docs.python.org/3/tutorial/controlflow.html#function-annotations)
- [speedsheet](https://speedsheet.io/s/python?select=qhNs)

- Class `TitleCase`
- Function `function_name_1`
- Constant `UPPER_SNAKE_CASE`
- Magic Method `__snake_case__`
- Module `snake_case`
- Private Name `_name`
- Variable `snake_case`

## Terms

- [hashable](https://docs.python.org/3/glossary.html#term-hashable)

## Input and Output

- [Tutorial](https://docs.python.org/3/tutorial/inputoutput.html)
- [Python print | realpython](https://realpython.com/python-print/)
- [Python 3's F-Strings | realpython](https://realpython.com/python-f-strings/)

You can convert any value to a string with the:
- [repr()](https://docs.python.org/3/library/functions.html#repr)
- [str()](https://docs.python.org/3/library/stdtypes.html#str)

You can view objects as JSON string representation with [.dumps()](https://docs.python.org/3/library/json.html#json.dumps).

Python comes with the `pprint` module in its standard library,
which will help you in pretty-printing large data structures that don’t fit on a single line.

Python comes with a built-in function for accepting input from the user, predictably called `input()`.

## Debugging

- [Python print - debugging | realpython](https://realpython.com/python-print/#debugging)
- [Python Debugging With Pdb](https://realpython.com/python-debugging-pdb/)

A debugger that runs in the terminal, named `pdb` for “The Python Debugger,” is distributed as part of the standard library.

## Testing

- [Getting Started With Testing in Python | realpython](https://realpython.com/python-testing/)
- [Unit Testing with Pytest and Mocks | realpython](https://realpython.com/python-cli-testing/#unit-testing-with-pytest-and-mocks)
- [Python's doctest: Document and Test Your Code at Once | realpython](https://realpython.com/python-doctest/)
- [Understanding the Python Mock Object Library](https://realpython.com/python-mock-library/)

It is convention to ensure each file starts with `test_` so all test runners will assume that Python file contains tests to be executed.

You can import any attributes of the script, such as classes, functions, and variables by using the built-in `__import__()` function.

## Linting

- [Python Code Quality: Tools & Best Practices | realpython](https://realpython.com/python-code-quality/)

## Logging

- [Logging in Python | realpython](https://realpython.com/courses/logging-python/)
- [Python print - logging](https://realpython.com/python-print/#logging)

Logging module is bundled with the standard library:

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

There’s a somewhat related `warnings` module in Python, which can also log messages to the standard error stream.
However, it has a narrower spectrum of applications, mostly in library code, whereas client applications should use the logging module.

That said, you can make them work together by calling `logging.captureWarnings(True)`.
