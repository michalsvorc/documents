# PostgreSQL

- [Documentation](https://www.postgresql.org/docs/)
- [Wiki](https://wiki.postgresql.org/wiki/Main_Page)
- [FAQ](https://wiki.postgresql.org/wiki/Frequently_Asked_Questions)

Tools:

- [psql](https://www.postgresql.org/docs/14/app-psql.html)

## Data types

- [Documentation](https://www.postgresql.org/docs/current/datatype.html)

### Numeric types

- [Documentation](https://www.postgresql.org/docs/current/datatype-numeric.html)

In addition to ordinary numeric values, the numeric and floating-point types have several special values:

- 'Infinity'
- '-Infinity'
- 'NaN'

PostgreSQL treats NaN values as equal, and greater than all non-NaN values.

#### Numeric and Decimal

The types decimal and numeric are equivalent.

It is especially recommended for storing monetary amounts and other quantities where exactness is required.

The _precision_ of a numeric is the total count of significant digits in the whole number, that is, the number of digits
to both sides of the decimal point. The _scale_ of a numeric is the count of decimal digits in the fractional part.

The maximum precision that can be explicitly specified in a `NUMERIC` type declaration is 1000.

#### Floating-Point types

The data types real and double precision are inexact, variable-precision numeric types.

When rounding values, the numeric type rounds ties away from zero, while (on most machines) the real and double
precision types round ties to the nearest even number.

#### Serial types

The data types smallserial, serial and bigserial are not true types, but merely a notational convenience for creating
unique identifier columns (similar to the `AUTO_INCREMENT` property supported by some other databases).

Because smallserial, serial and bigserial are implemented using sequences, there may be "holes" or gaps in the sequence
of values which appears in the column.
