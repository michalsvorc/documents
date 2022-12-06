# Go language

- [Documentation](https://go.dev/doc/)
- [Standard library](https://pkg.go.dev/std)
- [Packages](https://pkg.go.dev/)
- [Release notes](https://go.dev/doc/devel/release)
- [The Go Playground](https://play.golang.com/)

Tutorials:

- [Learn Go with Tests](https://quii.gitbook.io/learn-go-with-tests/)
- [Go by Example](https://gobyexample.com/)
- [Go Tutorial](https://www.tutorialspoint.com/go/index.htm)
- [Matt KODVB Go class (Video)](https://www.youtube.com/playlist?list=PLoILbKo9rG3skRCj37Kn5Zj803hhiuRK6)

Resources:

- [dariubs/GoBooks](https://github.com/dariubs/GoBooks)
- [The Go Blog](https://go.dev/blog/)
- [r/golang](https://www.reddit.com/r/golang/)

Guides:

- [Google style guide](https://google.github.io/styleguide/go/)
- [Code review commets](https://github.com/golang/go/wiki/CodeReviewComments)
- [Effective Go](https://go.dev/doc/effective_go)
- [Project layout](https://github.com/golang-standards/project-layout)
- [Package names](https://go.dev/blog/package-names)
- [100 Go Mistakes and How to Avoid Them](https://github.com/teivah/100-go-mistakes)
- [Five suggestions for setting up a Go project](https://dave.cheney.net/2014/12/01/five-suggestions-for-setting-up-a-go-project)

Libraries:

- [golangci-lint](https://golangci-lint.run/): An improvement over the default linter.

## Keywords and Identifiers

- [go101.org](https://go101.org/article/keywords-and-identifiers.html)

- Identifier `_` is a blank identifier.
- An identifier starting with an Unicode upper case letter is called an exported identifier. The word exported can be
  interpreded as public, and non-exported as private in many other languages.

## Basic types

- [bool](https://www.golang-book.com/books/intro/3#section3)
- [string](https://go101.org/article/string.html)
- [numbers](https://go101.org/article/basic-types-and-value-literals.html):
  int  int8  int16  int32  int64
  uint uint8 uint16 uint32 uint64 uintptr
  float32 float64
  complex64 complex128

Aliases:

- byte - alias for uint8
- rune - alias for int32, represents a Unicode code point

Boolean values are not convertible to/from integers.

Numbers, strings and booleans are completely separate, there is no truthy/falsy coercion between them.

Strings are passed by reference, they are not copied.

When you need an integer value you should use `int` unless you have a specific reason to use a sized or unsigned integer
type.

## Arrays

- [Go by Example](https://gobyexample.com/arrays)

Arrays are typed by size fixed at compile time. They are passed by value, meaning elements are copied.

## Slices

- [Go by Example](https://gobyexample.com/slices)

Slices have variable length and are passed by reference, no copying, updating is ok.

## Maps

- [Go by Example](https://gobyexample.com/maps)

Maps have special 2 result lookup function. The second result, conventionally assigned to variable name "ok" tells if
the key was there.

## Functions

- [Go by Example](https://gobyexample.com/functions)
- [Named return values](https://go.dev/tour/basics/7)
- [Multiple Return Values](https://gobyexample.com/multiple-return-values)
- [Variadic Functions](https://gobyexample.com/variadic-functions)

Function are first class objects.

The `signature` of a function is the order & type of its parameters and return values. It does not depend on the names
of those parameters or returns.

A function can return any number of results.

You can add documentation to functions with comments, and these will appear in Go Doc just like when you look at the
standard library's documentation.

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

### Defer

- [Go by Example](https://gobyexample.com/defer)
- [Defer, Panic, and Recover](https://go.dev/blog/defer-panic-and-recover)

Defer is used to ensure that a function call is performed later in a program’s execution, usually for purposes of
cleanup. `defer` is often used where e.g. ensure and finally would be used in other languages.

The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order.

## Typing system

- [go101.org](https://go101.org/article/constants-and-variables.html)
- [Type conversions](https://go.dev/tour/basics/13)

Go supports type deduction (inference). Go compilers will deduce the types for these values by context. Go uses
structural typing in most cases.

For most untyped values, each of them has one default type. The predeclared nil is the only untyped value which has no
default type.

## Variables

- [Declaration syntax](https://go.dev/blog/declaration-syntax)
- [Go by Example](https://gobyexample.com/variables)

`=` is the assignment operator. `:=` is for declaration and assignment, called short variable declaration clause.

Inside a function, the `:=` short assignment statement can be used in place of a var declaration with implicit type.

Outside a function, every statement begins with a keyword (var, func, and so on) and so the `:=` construct is not
available.

If an initializer is present, the type can be omitted; the variable will take the type of the initializer.

The variables declared out of any function body are called package-level constants. We also often call package-level
constants as global constants.

The declaration orders of two package-level constants are not important.

Go initializes all variables to "zero" value of their type, there are no "unitialized" variables. The zero value is:
- 0 for numeric types,
- false for the boolean type, and
- "" (the empty string) for strings.

## Constants

Go supports constants of character, string, boolean, and numeric values. Constants must be initialized with a value.

Constants cannot be declared using the `:=` syntax.

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

## Loops

- [Go by Example](https://gobyexample.com/for)

Go has only one looping construct, the `for` loop.

The basic `for` loop has three components separated by semicolons:
- the init statement: executed before the first iteration
- the condition expression: evaluated before every iteration
- the post statement: executed at the end of every iteration

`for` without a condition will loop repeatedly until you `break` out of the loop or return from the enclosing function.
You can also `continue` to the next iteration of the loop.

## If else

- [Go by Example](https://gobyexample.com/if-else)

The `if` statement can start with a short statement to execute before the condition.

Variables declared by the statement are only in scope until the end of the `if`. Variables declared inside an if short
statement are also available inside any of the `else` blocks.

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

## Packages

By convention, the package name is the same as the last element of the import path. For instance, the "math/rand"
package: `rand.Intn(10)`

## Testing

- [Examples](https://go.dev/blog/examples)
- [Benchmarks](https://pkg.go.dev/testing#hdr-Benchmarks)

Writing a test is just like writing a function, with a few rules:

- It needs to be in a file with a name like `xxx_test.go`
- The test function must start with the word `Test`
- The test function takes one argument only `t *testing.T`
- In order to use the `*testing.T` type, you need to `import "testing"`
