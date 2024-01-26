# Exceptions

Exceptions should be used to handle irregular behavior related to an unexpected error.

## Try/except

Minimize the amount of code in a `try/except` block. The larger the body of the try,
the more likely that an exception will be raised by a line of code that you didn’t expect to raise an exception.
In those cases, the try/except block hides a real error.

The integration of error processing within `try/catch` blocks can intertwine with regular processing.
A more effective approach involves isolating the content of `try/catch` blocks into distinct functions.

Functions are ideally focused on a singular task, and error handling constitutes one such task.
If the `try` keyword is present in a function, it should be the very first keyword, with nothing following the `catch/finally` blocks.

## Refactoring

- [Replace Exception with Test](https://refactoring.guru/replace-exception-with-test)

A simple conditional can sometimes be more obvious than exception handling code. If an exception can be avoided by simply verifying a condition before running, then do so.
Exceptions should be reserved for real errors.
