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

- Identifier `_` is a blank identifier.
- An identifier starting with an Unicode upper case letter is called an exported identifier. The word exported can be
  interpreded as public, and non-exported as private in many other languages.

## Basic types

- [bool](https://www.golang-book.com/books/intro/3#section3)
- [string](https://go101.org/article/string.html)
- [numbers](https://go101.org/article/basic-types-and-value-literals.html)

Aliases:

- byte - alias for uint8
- rune - alias for int32, represents a Unicode code point

Boolean values are not convertible to/from integers.

Numbers, strings and booleans are completely separate, there is no truthy/falsy coercion between them.

Strings are passed by reference, they are not copied.


## Arrays and slices

Arrays are typed by size fixed at compile time. They are passed by value, meaning elements are copied.

Slices have variable length and are passed by reference, no copying, updating is ok.

## Maps

Maps have special 2 result lookup function. The second result, conventionally assigned to variable name "ok" tells if
the key was there.

## Functions

Function are first class objects, you can:
- define them, even inside another function
- create anonymous function literals
- pass them as function parameters or return values
- store them in variables, slices and maps (but not as keys)
- store them as fields of a structure type
- send and receive them in channels
- write methods against a function type
- compare a function var against `nil`

The `signature` of a function is the order & type of its parameters and return values. It does not depend on the names
of those parameters or returns.

### Parameter passing

By value:
- numbers
- bool
- arrays
- structs

By reference:
- anything passed by pointer (`&x`)
- strings (they are immutable)
- slices
- maps
- channels

## Typing system

- [go101.org](https://go101.org/article/constants-and-variables.html)

Go supports type deduction (inference). Go compilers will deduce the types for these values by context. Go uses
structural typing in most cases.

For most untyped values, each of them has one default type. The predeclared nil is the only untyped value which has no
default type.

## Variables

`=` is the assignment operator. `:=` is for declaration and assignment, called short variable declaration clause.

 Inside a function, the `:=` short assignment statement can be used in place of a var declaration with implicit type.

Outside a function, every statement begins with a keyword (var, func, and so on) and so the `:=` construct is not
available. 

Go initializes all variables to "zero" value of their type, there are no "unitialized" variables.

Only basic types like strings, numbers and booleans can be immutable constants.

The variables declared out of any function body are called package-level constants. We also often call package-level
constants as global constants.

The declaration orders of two package-level constants are not important.

Declaration:

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

Value conversions: We can use the form `T(v)` to convert a value `v` to the type denoted by `T`.

```golang
string(65)          // "A"
string('A')         // "A"
```

### Autocomplete in constant declarations

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

## iota

- [golangbyexample.com](https://golangbyexample.com/iota-in-golang/)

Iota is a predeclared constant which can only be used in other constant declarations.

It is declared as `const iota = 0`.

The nth constant specification of a constant declaration, the value of iota is n (starting from zero). So iota is only
useful in group-style constant declarations.

Iota is an identifier which is used with constant and which can simplify constant definitions that use auto increment
numbers. The Iota keyword represent integer constant starting from zero. So essentially it can be used to create
effective constant in Go .

Iota provides an automated way to create a enum,

