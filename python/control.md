# Control structures

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html)
- [speedsheet](https://speedsheet.io/s/python?select=45aB)
- [break and continue](https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops)

- `if, elif, else`
- `for`
- `while`
- `match`

## if, elif, else

- [Documentation](https://docs.python.org/3/reference/compound_stmts.html#the-if-statement)
- [speedsheet](https://speedsheet.io/s/python?q=if#pnWX)

## for

- [Documentation](https://docs.python.org/3/reference/compound_stmts.html#for)
- [speedsheet](forhttps://speedsheet.io/s/python?q=if#pnWX)

Python’s for statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.

When the iterator is exhausted, the suite in the `else` clause, if present, is executed, and the loop terminates.

A `break` statement executed in the first suite terminates the loop without executing the else clause’s suite.
A `continue` statement executed in the first suite skips the rest of the suite and continues with the next item, or with the else clause if there is no next item.

If you do need to iterate over a sequence of numbers, the built-in function `range()` can be used.
The built-in type `range()` represents immutable arithmetic sequences of integers

## while

- [Documentation](https://docs.python.org/3/reference/compound_stmts.html#while)
- [speedsheet](https://speedsheet.io/s/python?q=while#v8Fy)

A `break` statement executed in the first suite terminates the loop without executing the else clause’s suite.
A `continue` statement executed in the first suite skips the rest of the suite and goes back to testing the expression.

## match

New in version 3.10.

- [Tutorial](https://docs.python.org/3/tutorial/controlflow.html#match-statements)
- [Documentation](https://docs.python.org/3/reference/compound_stmts.html#the-match-statement)
- [speedsheet](https://speedsheet.io/s/python?q=match#1Bmp)

Similar to a switch statement in C, Java or JavaScript (and many other languages), but it’s more similar to pattern matching in languages like Rust or Haskell. 
