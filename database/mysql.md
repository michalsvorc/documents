# MySQL

Overview:

- [Documentation](https://dev.mysql.com/doc/)
- [Built-In Function and Operator Reference - Documentation](https://dev.mysql.com/doc/refman/8.0/en/built-in-function-reference.html)
- [SQL Statements - Documentation](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html)
- [Examples - Documentation](https://dev.mysql.com/doc/mysql-tutorial-excerpt/8.0/en/examples.html)

Tutorials:

- [(Video) MySQL - The Basics](https://www.youtube.com/watch?v=Cz3WcZLRaWc)
- [(Video) SQL Tutorial - Full Database Course for Beginners](https://www.youtube.com/watch?v=HXV3zeQKqGY)

Topics:

- [ACID](https://en.wikipedia.org/wiki/ACID)
- [Pattern Matching](https://dev.mysql.com/doc/refman/8.0/en/pattern-matching.html)
- [Triggers](https://www.mysqltutorial.org/mysql-triggers.aspx)
- [Full text search](https://dev.mysql.com/doc/refman/8.0/en/fulltext-search.html)

## Data types

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
- [javatpoint.com](https://www.javatpoint.com/mysql-data-types)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-data-types.aspx)
- [tutorialspoint.com](https://www.tutorialspoint.com/mysql/mysql-data-types.htm)

MySQL does not have the built-in [BOOLEAN](https://www.mysqltutorial.org/mysql-boolean/) or[
BOOL](https://www.mysqltutorial.org/mysql-boolean/) data type. To represent boolean values, MySQL uses the smallest
integer type which is `TINYINT(1)`. In other words, `BOOLEAN` and `BOOL` are synonyms for `TINYINT(1)`.

In MySQL, a [NULL](https://www.mysqltutorial.org/mysql-null/) value means unknown. A `NULL` value is different from zero
(0) or an empty string ''. A `NULL` value is not equal to anything, even itself. If you compare a NULL value with another
`NULL` value or any other value, the result is `NULL` because the value of each `NULL` value is unknown.

### Numeric Data Types

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/numeric-types.html)

MySQL supports all standard SQL numeric data types. These types include the exact numeric data types (`INTEGER`,
`SMALLINT`, `DECIMAL`, and `NUMERIC`), as well as the approximate numeric data types (`FLOAT`, `REAL`, and `DOUBLE PRECISION`). The keyword INT is a synonym for INTEGER, and the keywords DEC and FIXED are synonyms for DECIMAL. MySQL
treats `DOUBLE` as a synonym for `DOUBLE PRECISION` (a nonstandard extension). MySQL also treats `REAL` as a synonym for
`DOUBLE PRECISION` (a nonstandard variation), unless the `REAL_AS_FLOAT` SQL mode is enabled.

In MySQL, numeric data types are categories into two types, either signed or unsigned except for the `BIT` data type.

Decimals have much higher precision and are usually used within financial applications that require a high degree of
accuracy. Decimals are much slower (up to 20X times in some tests) than a double/float.

### Date and Time Data Types

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html)

The date and time data types for representing temporal values are `DATE`, `TIME`, `DATETIME`, `TIMESTAMP`, and `YEAR`.
Each temporal type has a range of valid values, as well as a “zero” value that may be used when you specify an invalid
value that MySQL cannot represent.

MySQL supports the timestamp data type for tracking the changes in a row of a table. The `TIMESTAMP` and `DATETIME` types
have special automatic updating behavior.

### String Data Types

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/string-types.html)

The string data types are `CHAR`, `VARCHAR`, `BINARY`, `VARBINARY`, `BLOB`, `TEXT`, `ENUM`, and `SET`.

The `CHAR` and `VARCHAR` types are declared with a length that indicates the maximum number of characters you want to
store. For example, fixed-length `CHAR(30)` can hold up to 30 characters. Values in `VARCHAR` columns are variable-length
strings.

### Spatial Data Types

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/spatial-types.html)

MySQL spatial extensions enable the generation, storage, and analysis of geographic features:

- Data types for representing spatial values
- Functions for manipulating spatial values
- Spatial indexing for improved access times to spatial columns

### The JSON Data Type

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/json.html)

MySQL supports a native JSON data type defined by RFC 7159 that enables efficient access to data in JSON (JavaScript
Object Notation) documents. The JSON data type provides these advantages over storing JSON-format strings in a string
column:

- Automatic validation of JSON documents stored in JSON columns. Invalid documents produce an error.
- Optimized storage format.

JSON documents stored in JSON columns are converted to an internal format that permits quick read access to document
elements. When the server later must read a JSON value stored in this binary format, the value need not be parsed from a
text representation. The binary format is structured to enable the server to look up subobjects or nested values
directly by key or array index without reading all values before or after them in the document.

## User-defined variables

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/user-variables.html)

You can store a value in a user-defined variable in one statement and refer to it later in another statement. This
enables you to pass values from one statement to another.

User variables are written as `@var_name`.

User-defined variables are session specific. A user variable defined by one client cannot be seen or used by other
clients.

`SET @var_name = expr [, @var_name = expr] ...`

## Operators

- [Comparison Functions and Operators - Documentation](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html)
- [Logical Operators - Documentation](https://dev.mysql.com/doc/refman/8.0/en/logical-operators.html)
- [Assignment Operators - Documentation](https://dev.mysql.com/doc/refman/8.0/en/assignment-operators.html)
- [Aggregate Functions - Documentation](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html)

## Keys

- [Difference between Primary Key and Foreign Key](https://www.javatpoint.com/primary-key-vs-foreign-key)
- [Difference between Primary Key and Unique key](https://www.javatpoint.com/primary-key-vs-unique-key)

`KEY` is normally a synonym for `INDEX`. The key attribute `PRIMARY KEY` can also be specified as just `KEY` when given
in a column definition.

### Unique Key

- [javatpoint.com](https://www.javatpoint.com/mysql-unique-key)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-unique-constraint/)

A unique key in MySQL is a single field or combination of fields that ensure all values going to store into the column
will be unique. It means a column cannot stores duplicate values.

It can accept a null value, but MySQL allowed only one null value per column.

We can create a key in two ways:

- `CREATE TABLE` Statement
- `ALTER TABLE` Statement

If we use a UNIQUE constraint in the table, MySQL automatically creates a UNIQUE index behind the scenes.

See also unique index.

### Primary Key

- [javatpoint.com](https://www.javatpoint.com/mysql-primary-key)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-primary-key/)

MySQL primary key is a single or combination of the field, which is used to identify each record in a table uniquely.

The primary key follows these rules:

- The primary key column value must be unique.
- Each table can contain only one primary key.
- The primary key column cannot be null or empty.
- MySQL does not allow us to insert a new row with the existing primary key.
- Because MySQL works faster with integers, it is recommended to use INT or BIGINT data type for the primary key column.

When you define a primary key for a table, MySQL automatically creates an index called `PRIMARY`.

```sql
CREATE TABLE table_name(
    col1 datatype PRIMARY KEY,
    col2 datatype,
    ...
);
```

### Foreign Key

- [javatpoint.com](https://www.javatpoint.com/mysql-foreign-key)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-foreign-key/)

The foreign key is used to link one or more than one table together. It is also known as the referencing key. A foreign
key matches the primary key field of another table. It means a foreign key field in one table refers to the primary key
field of the other table. It identifies each row of another table uniquely that maintains the referential integrity in
MySQL.

A foreign key makes it possible to create a parent-child relationship with the tables.

```sql
[CONSTRAINT constraint_name]
    FOREIGN KEY [foreign_key_name] (col_name, ...)
    REFERENCES parent_tbl_name (col_name,...)
    ON DELETE referenceOption
    ON UPDATE referenceOption
```

### Composite Key

- [javatpoint](https://www.javatpoint.com/mysql-composite-key)

A composite key in MySQL is a combination of two or more than two columns in a table that allows us to identify each row
of the table uniquely. It is a type of candidate key which is formed by more than one column. MySQL guaranteed the
uniqueness of the column only when they are combined. If they have taken individually, the uniqueness cannot maintain.

`PRIMARY KEY (COL1, COL2);`

## Index

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)
- [javatpoint.com](https://www.javatpoint.com/how-to-create-index-in-mysql)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-index/)

An index is a data structure such as B-Tree that improves the speed of data retrieval on a table at the cost of
additional writes and storage to maintain it.

It enables you to improve the faster retrieval of records on a database table. It creates an entry for each value of the
indexed columns. We use it to quickly find the record without searching each row in a database table whenever the table
is accessed. We can create an index by using one or more columns of the table for efficient access to the records.

When a table is created with a primary key or unique key, it automatically creates a special index named `PRIMARY`. We
called this index as a clustered index. All indexes other than `PRIMARY` indexes are known as a non-clustered index or
secondary index.

### Unique index

- [javatpoint.com](https://www.javatpoint.com/mysql-unique-index)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-unique/)

MySQL allows another constraint called the `UNIQUE INDEX` to enforce the uniqueness of values in one or more columns. We
can create more than one `UNIQUE` index in a single table, which is not possible with the primary key constraint.

```sql
CREATE UNIQUE INDEX index_name
  ON table_name (index_column1, index_column2,...);
```

Another way to enforce the uniqueness of value in one or more columns is to use the `UNIQUE` constraint.

When you create a `UNIQUE` constraint, MySQL creates a `UNIQUE` index behind the scenes.

## Join

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/join.html)
- [javatpoint.com](https://www.javatpoint.com/mysql-join)
- [mysqltutorial.org](https://www.mysqltutorial.org/mysql-join/)
- [(Video) SQL Joins Tutorial for Beginners](https://www.youtube.com/watch?v=2HVMiPPuPIM)

A join is a method of linking data between one (self-join) or more tables based on values of the common column between
the tables.

MySQL JOINS are used with `SELECT` statement.

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- CROSS JOIN
- SELF JOIN

```sql
SELECT columns
  FROM table1
  INNER JOIN table2
  ON table1.column = table2.column;
```

### Using

If the join condition uses the equality operator (=) and the column names in both tables used for matching are the same,
and you can use the `USING` clause instead.

## Union

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/union.html)
- [javatpoint.com](https://www.javatpoint.com/mysql-union)
- [Union vs. Join - javatpoint.com](https://www.javatpoint.com/mysql-union-vs-join)

`UNION` combines the result from multiple `SELECT` statements into a single result set.

It comes with a default feature that removes the duplicate rows from the result set. MySQL always uses the name of the
column in the first `SELECT` statement will be the column names of the result set(output).

```sql
SELECT column_list FROM table1
UNION
SELECT column_list FROM table2;
```

The Union and Join clause are different because a union always combines the result set _vertically_ while the join
appends the output _horizontally_.

## Transactions

- [javatpoint.com](https://www.javatpoint.com/mysql-transaction)

A transaction in MySQL is a _sequential group_ of statements, queries, or operations such as select, insert, update or
delete to perform as a one single work unit that can be committed or rolled back.

## Views

- [Documentation](https://dev.mysql.com/doc/refman/8.0/en/views.html)
- [javatpoint.com](https://www.javatpoint.com/mysql-view)

Views are stored queries that when invoked produce a result set. A view acts as a virtual table.

The View and table have one main difference that the views are definitions built on top of other tables (or views). If
any changes occur in the underlying table, the same changes reflected in the View also.
