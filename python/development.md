# Development

1. Set up virtual environment

```shell
python3 -m venv .venv
source .venv/bin/activate
```

2. Install dependencies
   2.1. Install testing framework (pytest)

   ```shell
   python3 -m pip install pytest pytest-testmon pytest-watch
   ```

   2.2. Run tests in watch mode

   ```shell
   ptw -- --testmon
   ```

3. Add `.gitignore`

```shell
__pycache__
.pytest_cache
.testmondata
.venv
```

## Virtual environment

- [Creating Virtual Environments](https://docs.python.org/3/tutorial/venv.html)
- [Real Python](https://realpython.com/python-virtual-environments-a-primer)
- [venv module](https://docs.python.org/3/library/venv.html)

`cd` to project directory.

A common directory location for a virtual environment is `.venv`.

To make your virtual environment reproducible, execute while `venv` is active:

```shell
python3 -m pip freeze > requirements.txt
```

## Testing

- [Getting Started With Testing in Python](https://realpython.com/python-testing/)
- [Effective Python Testing With Pytest](https://realpython.com/pytest-python-testing/)
- [Unit Testing with Pytest and Mocks](https://realpython.com/python-cli-testing/#unit-testing-with-pytest-and-mocks)
- [Understanding the Python Mock Object Library](https://realpython.com/python-mock-library/)
- [Python's doctest: Document and Test Your Code at Once](https://realpython.com/python-doctest/)
- [Assert statements](https://realpython.com/python-assert-statement/)

Test runners:

- unittest: built in, verbose, simple scenarios, discovers files starting with `test_`
- nose2: compatible with unittest, better output, more flexible
- pytest: simple syntax, discovers functions starting with `test_`

It is convention to ensure each file starts with `test_` so all test runners will assume that Python file contains tests to be executed.

### Pytest

- [Fixtures](https://docs.pytest.org/en/latest/explanation/fixtures.html)

## Linting

- [Python Code Quality: Tools & Best Practices](https://realpython.com/python-code-quality/)

## Debugging

- [Python print: debugging](https://realpython.com/python-print/#debugging)
- [Python Debugging With Pdb](https://realpython.com/python-debugging-pdb/)

A debugger that runs in the terminal, named `pdb` for “The Python Debugger,” is distributed as part of the standard library.

Since Python 3.7, you can also call the built-in `breakpoint()` function from the code.

## Logging

- [Python print: logging](https://realpython.com/python-print/#logging)
- [Logging in Python](https://realpython.com/courses/logging-python/)

Logging module is bundled with the standard library:

```python
import logging
logging.basicConfig(level=logging.DEBUG)
logging.debug("debug")
```

There’s a somewhat related `warnings` module in Python, which can also log messages to the standard error stream.
