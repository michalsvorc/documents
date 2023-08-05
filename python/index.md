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

When you don’t need fancy output but just want a quick display of some variables for debugging purposes, you can convert
any value to a string with the [repr()](https://docs.python.org/3/library/functions.html#repr) or
[str()](https://docs.python.org/3/library/stdtypes.html#str) functions.

You can view objects as JSON string representation with
[.dumps()](https://docs.python.org/3/library/json.html#json.dumps).

## Testing

- [Getting Started With Testing in Python | realpython](https://realpython.com/python-testing/)
- [Python's doctest: Document and Test Your Code at Once | realpython](https://realpython.com/python-doctest/)
- [Unit Testing with Pytest and Mocks | realpython](https://realpython.com/python-cli-testing/#unit-testing-with-pytest-and-mocks)

It is convention to ensure each file starts with `test_` so all test runners will assume that Python file contains tests to be executed.

You can import any attributes of the script, such as classes, functions, and variables by using the built-in `__import__()` function.

## Linting

- [Python Code Quality: Tools & Best Practices | realpython](https://realpython.com/python-code-quality/)
