# Remember

* [JS Is Weird](https://jsisweird.com/)

## typeof

Common gotchas

```js
typeof NaN === 'number'; // true, despite being "Not-A-Number"

typeof null === 'object' // true

typeof []                // "object"

typeof new Boolean(true) === 'object';  // true 

typeof new Number(1) === 'object';      // true

typeof new String('abc') === 'object';  // true
```

## null vs undefined

Douglas Crockford thinks [null is a bad idea](https://www.youtube.com/watch?v=PSGEjv3Tqo0&feature=youtu.be&t=9m21s) and
we should all just use `undefined`.


## array.length is settable

```js
const arr = [1,2,3]

arr.length = 2

console.log(arr) // [1,2]
```

## Modulus % and negative numbers

```js
console.log(-5 % 2) // -1
console.log(-5 % -2) // -1
```

## + operator

According to [MDN
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Unary_plus) the `+`
is the fastest way of converting a string to a number because it does not perform any operations on the value if it is
already a number.

## parseFloat() vs parseInt()

[parseFloat() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)

Parses an argument (converting it to a string first if needed) and returns a floating point number. Doesn't take a radix parameter.

[parseInt() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

The parseInt function converts its first argument to a string, parses that string, then returns an integer or NaN. If not NaN, the return value will be the integer that is the first argument taken as a number in the specified radix (second argument).

## Creating closures in loops: A common mistake

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures#creating_closures_in_loops_a_common_mistake)

```js
const obj = {}

for (var i = 0; i <= 2; i++) {
  obj[`log_${i}`] = function() {console.log(i)}
}

obj.log_0() // 3
obj.log_1() // 3
obj.log_2() // 3
```

The reason for this is that the functions assigned to `log_${i}` methods are closures; they consist of the function
definition and they captured environment from the outside (`i++`). This is because the variable `i` is declared with
`var`.

You can fix this with creating more closures, or you can use `let  i = 0;`.

## Function.name

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name)

Function object's read-only `name` property indicates the function's name as specified when it was created, or it may be
either anonymous or '' (an empty string) for functions created anonymously.

This property might help with debugging.

## Comparisons and checks

* [Equality comparisons and sameness - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

### Check if number is NaN

* [Number.isNaN() - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN) 
* [NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)

Problem:

```js
typeof NaN === ‘number’ // true
NaN === NaN             // false
```

Solution: Use `Number.isNaN()`. This method returns true if the given value is `NaN`; otherwise, `false`.

### Check if value is a valid number (integer/float), not NaN or Infinity

* [Number.isFinite() - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isFinite)

### Strict comparison

* [Object.is() - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)

Problem:

```js
console.log(+0 === -0) // true
console.log(NaN === NaN) //false
```

Solution: The `Object.is()` method determines whether two values are the same value. 

This is also not the same as being equal according to the `===` operator. The only difference between `Object.is()` and
`===` is in their treatment of signed zeroes and NaNs.

```js
console.log(Object.is(+0, -0)) // false
console.log(Object.is(NaN, NaN)) //true
```

### null and undefined

* [How can I check for "undefined" in JavaScript?](https://stackoverflow.com/questions/3390396/how-can-i-check-for-undefined-in-javascript) \
* [Is there a standard function to check for null, undefined, or blank variables in JavaScript?](https://stackoverflow.com/questions/5515310/is-there-a-standard-function-to-check-for-null-undefined-or-blank-variables-in)

`x == null` checks for both `null` or `undefined`.

undefined:

`x === undefined`

null:

`x === null`

