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
precision types round ties to the nearest even number. Floating point numbers should not be used to handle money due to the potential for rounding errors.

**Serial types**:

The data types smallserial, serial and bigserial are not true types, but merely a notational convenience for creating
unique identifier columns (similar to the `AUTO_INCREMENT` property supported by some other databases).

Because smallserial, serial and bigserial are implemented using sequences, there may be "holes" or gaps in the sequence of values which appears in the column, even if no rows are ever deleted. A value allocated from the sequence is still "used up" even if a row containing that value is never successfully inserted into the table column. This may happen, for example, if the inserting transaction rolls back.

### Monetary types

- [Documentation](https://www.postgresql.org/docs/15/datatype-money.html)

The money type stores a currency amount with a fixed fractional precision. The fractional precision is determined by the database's `lc_monetary` setting. 
Since the output of this data type is locale-sensitive, it might not work to load money data into a database that has a different setting of `lc_monetary`.

A `money` value can be cast to `numeric` without loss of precision. 

### Character types

- [Documentation](https://www.postgresql.org/docs/15/datatype-character.html)

SQL defines two primary character types: `character varying(n)` and `character(n)`, where `n` is a positive integer. Both of these types can store strings up to `n` *characters* (not bytes) in length.

The characters that can be stored in any of these data types are determined by the database *character set*, which is selected when the database is created. 

When the excess characters are all spaces, the string will be truncated to the maximum length. (This somewhat bizarre exception is required by the SQL standard.)

If one explicitly casts a value to `character varying(n)` or `character(n)`, then an over-length value will be truncated to n characters without raising an error. (This too is required by the SQL standard.)

Character without length specifier is equivalent to `character(1)`. If character varying is used without length specifier, the type accepts strings of *any size*. 

In addition, PostgreSQL provides the `text` type, which stores strings of any length. (Not in the SQL standard.)

**Performance**:

There is no performance difference among these three types, apart from increased storage space when using the blank-padded type, and a few extra CPU cycles to check the length when storing into a length-constrained column. 

While `character(n)` has performance advantages in some other database systems, there is no such advantage in PostgreSQL; in fact `character(n)` is usually *the slowest of the three* because of its additional storage costs. In most situations `text` or `character varying` should be used instead.

**Trailing spaces**:

Values of type `character` are physically padded with spaces to the specified width `n`, and are stored and displayed that way. However, trailing spaces are treated as semantically insignificant and disregarded when comparing two values of type `character`. 

Note that trailing spaces are semantically significant in character varying and text values, and when using pattern matching, that is `LIKE` and regular expressions.

Trailing spaces are removed when converting a `character` value to one of the other string types.

### Date/Time

- [Documentation](https://www.postgresql.org/docs/current/datatype-datetime.html)

- timestamp (with and without timezone)
- time (with and without timezone)
- date
- interval

The SQL standard requires that writing just `timestamp` be equivalent to `timestamp` *without time zone*, and PostgreSQL honors that behavior. `timestamptz` is accepted as an abbreviation for `timestamp` *with time zone*; this is a PostgreSQL extension.

`time`, `timestamp`, and `interval` accept an optional precision value `p` which specifies the number of fractional digits retained in the seconds field. By default, there is no explicit bound on precision.

The allowed range of `p` is *from 0 to 6*. If no precision is specified in a constant specification, it defaults to the precision of the literal value (but not more than 6 digits).

Valid ISO 8601 examples:

- `date`: '1999-01-08' (recommended format)
- `time`: '04:05:06'
- `timestamp`: '1999-01-08 04:05:06'

The following SQL-compatible functions can also be used to obtain the current time value for the corresponding data type: `CURRENT_DATE`, `CURRENT_TIME`, `CURRENT_TIMESTAMP`, `LOCALTIME`, `LOCALTIMESTAMP`.

We mainly use `interval` values for date and time arithmetic: `'2020-01-01' + INTERVAL 1 DAY`

### Boolean

- [Documentation](https://www.postgresql.org/docs/current/datatype-boolean.html)

The boolean type can have several states: "true", "false", and a third state, "unknown", which is represented by the SQL `null` value.

True state:
- true
- yes
- on
- 1

False state: 
- false
- no
- off
- 0

The key words `TRUE` and `FALSE` are the preferred (SQL-compliant) method for writing Boolean constants in SQL queries.

### Enumerated types

- [Documentation](https://www.postgresql.org/docs/current/datatype-enum.html)

The ordering of the values in an enum type is the order in which the values were listed when the type was created.
Each enumerated data type is separate and cannot be compared with other enumerated types.
Enum labels are case sensitive, white space in the labels is significant too.

### Geometric types

- [Documentation](https://www.postgresql.org/docs/current/datatype-geometric.html)

Geometric data types represent two-dimensional spatial objects.

- Points
- Lines
- Line Segments
- Boxes
- Paths
- Polygons
- Circles

### Network address types

- [Documentation](https://www.postgresql.org/docs/current/datatype-net-types.html)
- [Functions and operators](https://www.postgresql.org/docs/current/functions-net.html)

It is better to use these types instead of plain text types to store network addresses, because these types offer
input error checking and specialized operators and functions.

- inet
- cidr
- inet vs. cidr
- macaddr
- macaddr8

### JSON types

- [Documentation](https://www.postgresql.org/docs/current/datatype-json.html)
- [Functions and operators](https://www.postgresql.org/docs/current/functions-json.html)
- [Type mapping table](https://www.postgresql.org/docs/current/datatype-json.html#JSON-TYPE-MAPPING-TABLE)

The JSON data types have the advantage of enforcing that each stored value is valid according to the JSON rules.

- json
- jsonb
- jsonpath

The `json` and `jsonb` data types accept almost identical sets of values as input. The major practical difference is one of efficiency.
In general, most applications should prefer to store JSON data as `jsonb`, unless there are quite specialized needs, such as legacy assumptions about ordering of object keys.
`jsonb` will reject numbers that are outside the range of the PostgreSQL `numeric` data type, while `json` will not.
In `jsonb`, numbers will be printed according to the behavior of the underlying `numeric` type.

#### json

The `json` data type stores an exact copy of the input text, which processing functions must reparse on each execution.
It will preserve semantically-insignificant white space between tokens, as well as the order of keys within JSON objects. 
If a JSON object within the value contains the same key more than once, all the key/value pairs are kept.

#### jsonb

- [jsonb Containment and Existence](https://www.postgresql.org/docs/current/datatype-json.html#JSON-CONTAINMENT)

`jsonb` data is stored in a decomposed binary format that makes it slightly slower to input due to added conversion overhead, but significantly faster to process.
`jsonb` also supports indexing.
`jsonb` does not preserve white space, does not preserve the order of object keys, and does not keep duplicate object keys. If duplicate keys are specified in the input, only the last value is kept.

Testing *containment* is an important capability of `jsonb`. Containment tests whether one `jsonb` document has contained within it another one. JSON *containment* is nested.

`jsonb` also has an *existence* operator, which is a variation on the theme of containment: it tests whether a string (given as a text value) 
appears as an *object key* or *array element* at the top level of the `jsonb` value.
The JSON *existence* operator is not nested: it will only look for the specified key or array element at top level of the JSON value.

JSON objects are better suited than arrays for testing containment or existence when there are many keys or elements involved,
because unlike arrays they are internally optimized for searching, and do not need to be searched linearly.

##### jsonb Indexing

- [jsonb Indexing](https://www.postgresql.org/docs/current/datatype-json.html#JSON-INDEXING)
- [jsonb Operators](https://www.postgresql.org/docs/current/functions-json.html#FUNCTIONS-JSONB-OP-TABLE)
- [GIN Indexes](https://www.postgresql.org/docs/current/gin-intro.html)

GIN indexes can be used to efficiently search for keys or key/value pairs occurring within a large number of `jsonb` documents.

##### jsonb Subscripting

- [jsonb Subscripting](https://www.postgresql.org/docs/current/datatype-json.html#JSONB-SUBSCRIPTING)

The `jsonb` data type supports array-style subscripting expressions to extract and modify elements.
`UPDATE` statements may use subscripting in the `SET` clause to modify `jsonb` values.

#### jsonpath Type

- [jsonpath Type](https://www.postgresql.org/docs/current/datatype-json.html#DATATYPE-JSONPATH)

The `jsonpath` type implements support for the SQL/JSON path language in PostgreSQL to efficiently query JSON data.
To provide a natural way of working with JSON data, SQL/JSON path syntax uses some JavaScript conventions:
  - Dot `.` is used for member access.
  - Square brackets `[]` are used for array access.

### Other data types

- [Bit String](https://www.postgresql.org/docs/current/datatype-bit.html): Bit strings are strings of 1's and 0's. They can be used to store or visualize bit masks.
- [Text Search](https://www.postgresql.org/docs/current/datatype-textsearch.html): PostgreSQL provides two data types that are designed to support full text search.
- [UUID](https://www.postgresql.org/docs/current/datatype-uuid.html): 128-bit Universally Unique Identifiers. 
- [XML](https://www.postgresql.org/docs/current/datatype-xml.html): Checks the input values for well-formedness, supports functions to perform type-safe operations.

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

```sql
SELECT depname, empno, salary, avg(salary) OVER (PARTITION BY depname) FROM empsalary;
```

A window function call always contains an `OVER` clause directly following the window function's name and argument(s).
This is what syntactically distinguishes it from a normal function or non-window aggregate.

The `OVER` clause determines exactly how the rows of the query are split up for processing by the window function.
The `PARTITION BY` clause within `OVER` divides the rows into groups, or partitions, that share the same values of the `PARTITION BY` expression(s).
For each row, the window function is computed across the rows that fall into the same partition as the current row.

When a query involves multiple window functions, it is possible to write out each one with a separate `OVER` clause, but this is duplicative and error-prone
if the same windowing behavior is wanted for several functions. Instead, each windowing behavior can be named in a `WINDOW` clause and then referenced in `OVER`. 

## Inheritance

- [Tutorial](https://www.postgresql.org/docs/current/tutorial-inheritance.html)

Inheritance is a concept from object-oriented databases. In PostgreSQL, a table can inherit from zero or more other tables.

Although inheritance is frequently useful, it has not been integrated with unique constraints or foreign keys, which limits its usefulness.

```sql
CREATE TABLE cities(
  name       text,
  population real,
  elevation  int
)


CREATE TABLE capitals (
  state      char(2) UNIQUE NOT NULL
) INHERITS (cities);
```

In this case, a row of `capitals` *inherits* all columns (name, population, and elevation) from its *parent*, `cities`.

### ONLY notation

The `ONLY` indicates that the query should be run over only the parent table, and not tables below parent in the inheritance hierarchy.

Many of the commands like `SELECT`, `UPDATE`, and `DELETE` support this `ONLY` notation.

## Aggregations

- [Tutorial](https://www.postgresql.org/docs/current/tutorial-agg.html)

### HAVING

The fundamental difference between `WHERE` and `HAVING` is this: `WHERE` selects input rows before groups and aggregates are
computed (thus, it controls which rows go into the aggregate computation), whereas `HAVING` selects group rows after
groups and aggregates are computed. Thus, the `WHERE` clause must not contain aggregate functions.

```sql
SELECT city, count(*), max(temp_lo)
    FROM weather
    GROUP BY city
    HAVING max(temp_lo) < 40;
```

### FILTER

Another way to select the rows that go into an aggregate computation is to use `FILTER`, which is a per-aggregate option.

`FILTER` is much like `WHERE`, except that it removes rows only from the input of the particular aggregate function that it is attached to. 

Here, the count aggregate counts only rows with `temp_lo` below *45*; but the `max` aggregate is still applied to all rows, so it still finds the reading higher than *45*.

```sql
SELECT city, count(*) FILTER (WHERE temp_lo < 45), max(temp_lo)
    FROM weather
    GROUP BY city;
```

