# Go language

- [Documentation](https://go.dev/doc/)
- [Standard library](https://pkg.go.dev/std)
- [Packages](https://pkg.go.dev/)
- [Release notes](https://go.dev/doc/devel/release)

Tutorials:

- [Learn Go with Tests](https://quii.gitbook.io/learn-go-with-tests/)
- [Go by Example](https://gobyexample.com/)
- [Go Tutorial](https://www.tutorialspoint.com/go/index.htm)
- [Matt KODVB Go class (Video)](https://www.youtube.com/playlist?list=PLoILbKo9rG3skRCj37Kn5Zj803hhiuRK6)

Resources:

- [The Go Playground](https://play.golang.com/)
- [Books](https://github.com/dariubs/GoBooks)

Guides:

- [Effective Go](https://go.dev/doc/effective_go)
- [Project layout](https://github.com/golang-standards/project-layout)
- [Package names](https://go.dev/blog/package-names)
- [100 Go Mistakes and How to Avoid Them](https://github.com/teivah/100-go-mistakes)

Blogs:

- [The Go Blog](https://go.dev/blog/)
- [r/golang](https://www.reddit.com/r/golang/)

## Keywords and Identifiers

- [go101.org](https://go101.org/article/keywords-and-identifiers.html)

Identifier `_` is a special identifier, it is called blank identifier.

An identifier starting with an Unicode upper case letter is called an exported identifier. The word exported can be
interpreted as public in many other languages.

The identifiers which don't start with an Unicode upper case letter are called non-exported identifiers. The word
non-exported can be interpreted as private in many other languages.

## Basic types

### Boolean

- [golang-book.com](https://www.golang-book.com/books/intro/3#section3)

`bool`

### Strings

- [go101.org](https://go101.org/article/string.html)

`string`

Go supports two styles of string literals, the double-quote style (or interpreted literals) and the back-quote style (or
raw string literals).

Double quoted strings cannot contain newlines and they allow special escape sequences.

### Numbers

- [go101.org](https://go101.org/article/basic-types-and-value-literals.html)

#### Integers

- uint8, uint16, uint32, uint64, int8, int16, int32 and int64

Aliases:

- byte - alias for uint8
- rune - alias for int32, represents a Unicode code point

Machine dependendent integers:

- uint
- int
- uintptr

Generally if you are working with integers you should just use the `int` type.

### Floating Point Numbers

Floating point numbers are inexact.

Go has two floating point types:

- float32
- float64

(also often referred to as single precision and double precision respectively) as well as two additional types for
representing complex numbers (numbers with imaginary parts):

- complex64
- complex128

Generally we should stick with `float64` when working with floating point numbers.

## Constants and Variables

- [go101.org](https://go101.org/article/constants-and-variables.html)

Go supports type deduction (inference). Go compilers will deduce the types for these values by context.

For most untyped values, each of them has one default type. The predeclared nil is the only untyped value which has no
default type.

### Constants

Constant specification:

```golang
const Pi = 3.1416

// Declare multiple constants in a group.
const (
	Yes = true
	No  = !Yes
)
```

The `=` symbol means "bind" instead of "assign". We should interpret each constant specification as a declared identifier
is bound to a corresponding basic value literal.

#### Scope

The variables declared out of any function body are called package-level constants. We also often call package-level
constants as global constants.

The declaration orders of two package-level constants are not important.

#### Explicit Conversions of Untyped Constants

Value conversions: We can use the form T(v) to convert a value v to the type denoted by T (or simply speaking, type T).

```golang
string(65)          // "A"
string('A')         // "A"
```

#### Autocomplete in constant declarations

At compile time, compilers will automatically complete the following code

```golang
const(
  X float32 = 3.14
	Y           // here must be one identifier
	Z           // here must be one identifier

	A, B = "Go", "language"
	C, _
	// In the above line, the blank identifier is required to be present.
)
```

as

```golang
const (
	X float32 = 3.14
	Y float32 = 3.14
	Z float32 = 3.14

	A, B = "Go", "language"
	C, _ = "Go", "language"
)
```

#### iota

- [golangbyexample.com](https://golangbyexample.com/iota-in-golang/)

Iota is a predeclared constant which can only be used in other constant declarations.

It is declared as `const iota = 0`.

The nth constant specification of a constant declaration, the value of iota is n (starting from zero). So iota is only
useful in group-style constant declarations.

Iota is an identifier which is used with constant and which can simplify constant definitions that use auto increment
numbers. The Iota keyword represent integer constant starting from zero. So essentially it can be used to create
effective constant in Go .

Iota provides an automated way to create a enum,

### Variables

