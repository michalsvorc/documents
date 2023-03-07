# PostgreSQL

- [Documentation](https://www.postgresql.org/docs/)
- [Wiki](https://wiki.postgresql.org/wiki/Main_Page)
- [FAQ](https://wiki.postgresql.org/wiki/Frequently_Asked_Questions)

Tools:

- [psql](https://www.postgresql.org/docs/14/app-psql.html)

## Concepts

Whereas columns have a fixed order in each row, it is important to remember that SQL does not guarantee the order of the
rows within the table in any way (although they can be explicitly sorted for display).

Tables are grouped into databases, and a collection of databases managed by a single PostgreSQL server instance
constitutes a database cluster.

The result of a value expression is sometimes called a scalar, to distinguish it from the result of a table expression (which is a table).
Value expressions are therefore also called scalar expressions (or even simply expressions).

## Data types

- [Documentation](https://www.postgresql.org/docs/current/datatype.html)

PostgreSQL can be customized with an arbitrary number of user-defined data types.

### Numeric types

- [Documentation](https://www.postgresql.org/docs/current/datatype-numeric.html)

In addition to ordinary numeric values, the numeric and floating-point types have several special values:

- 'Infinity'
- '-Infinity'
- 'NaN'

PostgreSQL treats NaN values as equal, and greater than all non-NaN values.

**Numeric and Decimal**:

The types decimal and numeric are equivalent.

It is especially recommended for storing monetary amounts and other quantities where exactness is required.

**Floating-Point**:

The data types real and double precision are inexact, variable-precision numeric types.

When rounding values, the numeric type rounds ties away from zero, while (on most machines) the real and double
precision types round ties to the nearest even number.

**Serial types**:

The data types smallserial, serial and bigserial are not true types, but merely a notational convenience for creating
unique identifier columns (similar to the `AUTO_INCREMENT` property supported by some other databases).

Because smallserial, serial and bigserial are implemented using sequences, there may be "holes" or gaps in the sequence of values which appears in the column, even if no rows are ever deleted. A value allocated from the sequence is still "used up" even if a row containing that value is never successfully inserted into the table column. This may happen, for example, if the inserting transaction rolls back.

## Views

You do not want to type the query each time you need it. You can create a view over the query, which gives a name to the
query that you can refer to like an ordinary table.

Views allow you to encapsulate the details of the structure of your tables, which might change as your application
evolves, behind consistent interfaces. Views can be used in almost any place a real table can be used. Building views
upon other views is not uncommon.

## Transactions

- [Tutorial](https://www.postgresql.org/docs/current/tutorial-transactions.html)

PostgreSQL actually treats every SQL statement as being executed within a transaction.

If you do not issue a `BEGIN` command, then each individual statement has an implicit `BEGIN` and (if successful)
`COMMIT` wrapped around it.

A group of statements surrounded by `BEGIN` and `COMMIT` is sometimes called a transaction block.

### Save points in transaction

It's possible to control the statements in a transaction in a more granular fashion through the use of savepoints.

Savepoints allow you to selectively discard parts of the transaction, while committing the rest. After defining a
savepoint with `SAVEPOINT`, you can if needed roll back to the savepoint with `ROLLBACK TO`.

All the transaction's database changes between defining the savepoint and rolling back to it are discarded, but changes
earlier than the savepoint are kept.

## Window Functions

- [Tutorial](https://www.postgresql.org/docs/current/tutorial-window.html)

A window function performs a calculation across a set of table rows that are somehow related to the current row. This is
comparable to the type of calculation that can be done with an aggregate function.

However, window functions do not cause rows to become grouped into a single output row like non-window aggregate calls
would. Instead, the rows retain their separate identities.

Behind the scenes, the window function is able to access more than just the current row of the query result.

## Inheritance

- [Tutorial](https://www.postgresql.org/docs/current/tutorial-inheritance.html)

Inheritance is a concept from object-oriented databases. In PostgreSQL, a table can inherit from zero or more other tables.

## WHERE and HAVING clauses

The fundamental difference between `WHERE` and `HAVING` is this: `WHERE` selects input rows before groups and aggregates are
computed (thus, it controls which rows go into the aggregate computation), whereas `HAVING` selects group rows after
groups and aggregates are computed. Thus, the `WHERE` clause must not contain aggregate functions.
