# Arrays

Overview:

* [Indexed collections - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections)
* [Array - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
* [Arrays - exploringjs.com](https://exploringjs.com/impatient-js/ch_arrays.html)

Topics:

* [Array intersection, difference and union in ES6](https://medium.com/@alvaro.saburido/set-theory-for-arrays-in-es6-eb2f20a61848)
* [Adding and removing elements](https://exploringjs.com/impatient-js/ch_arrays.html#adding-and-removing-elements-destructively-and-non-destructively)

## Empty slots

```js
let cats = []
cats[5] = ['Dusty']

console.log(cats.length)  // 6
console.log(cats)         // [ <5 empty slots>, "'Dusty'" ]
```

Empty slots are empty, not slots with actual `undefined` values.

## Indices

* [tc39.github.io](https://tc39.github.io/ecma262/#integer-index)

Property keys that are used for Array elements are called *indices*. The square brackets operator `[ ]` for accessing
indices is the same operator that is used for accessing properties.

It coerces any value (that is not a symbol) to a *string*. Therefore, `[0]` retrieves the value of the property whose
key is `0`.

```js
arr[0] === arr['0']
```

Setting or accessing via non-integers using bracket notation (or dot notation) will not set or retrieve an element from
the array list itself, but will set or access a variable associated with that array's [object property
collection](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#properties). 

```js
let arr = []
arr[3.4] = 'Oranges'

console.log(arr.length)               // 0
console.log(arr.[3.4])                // 'Oranges'
console.log(arr.hasOwnProperty(3.4))  // true

arr.stringProperty = "value"

console.log(arr.stringProperty)             // 'value'
```

## Length property

You can also assign directly to the length property. Writing a value that is shorter than the number of stored items
truncates the array. Writing 0 empties it entirely.

## Listing properties

Array Iterator methods return a new Array Iterator object.

* [Array.prototype.entries()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)
* [Array.prototype.values()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/values)
* [Array.prototype.keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)

Listing the indices (integers):

```js
const indexes = Array.from(arr.keys())
```

Listing all properties (integers + non-integers):

```js
array['property'] = 'prop A'
const properties = Object.keys(arr)
```

Access key value pair in iteration:

```js
for (const [key, value] of arr.entries())
```

When listing property `keys()`, indices are treated specially – they always come first and are sorted like numbers.

## Creation

### Array() constructor

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Array)

Arrays can be created using an Array constructor with a single number parameter. An array with its length property set
to that number and the array elements are empty slots.

If more than one argument is passed to the constructor, a new Array with the given elements is created.

```js
new Array(7);        // array of 7 empty slots
new Array(1, 2, 3);  // [1, 2, 3]
```

### Array.from()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

`Array.from()` lets you create Arrays from:

* array-like objects (objects with a length property and indexed elements)
* iterable objects

`Array.from()` has an optional parameter, which allows you to execute a `map()` function on each element of the array being created.

Example for creating an array with range of integers:

```js
function createRange(start, end) {
  return Array.from({length: end - start}, (_, i) => i + start);
}
```

### Array.of()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/of)

The difference between `Array.of()` and the Array constructor is in the handling of integer arguments: `Array.of(7)`
creates an array with a single element 7, whereas `Array(7)` creates an empty array with a length property of 7. 

## Copy an Array

Note that these methods only make shallow copies. That means the nested items will still be a reference type array.

* [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

```js
const originalArray = [1,2,3,4,5]
const clone = originalArray.slice()
```

* [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

```js
const originalArray = [2,4,6,8,10]
const clone = [...originalArray]
```


* [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

```js
const originalArray = [1,2,3,4,5]
const clone = [].concat(originalArray)
```

## Array.prototype.reduce()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

Your reducer function's returned value is assigned to the accumulator, whose value is remembered across each iteration
throughout the array, and ultimately becomes the final, single resulting value.

`reduce((previousValue, currentValue, currentIndex, array) => { ... }, initialValue)`

*initialValue*: A value to use as the first argument to the first call of the callback function. If no `initialValue`
is supplied, the first element in the array will be used as the initial accumulator value and skipped as
`currentValue`.

## Methods

### Single element operations, destructive

* [Array.prototype.shift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift):
  removes the first element, removed element || undefined
* [Array.prototype.unshift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift):
  adds one or more elements to the beginning of an array: new length property
* [Array.prototype.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop):
  removes the last element, removed element || undefined
* [Array.prototype.push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push):
  adds one or more elements to the end of an array, new length property

### Mappings, non-destructive

* [Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce):
  the single value result
* [Array.prototype.reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight):
  the single value result
* [Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map):
  new array
* [Array.prototype.flatMap()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap):
  new array
* [Array.prototype.flat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat):
  new array

### Tests

* [Array.prototype.every()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every):
  boolean
* [Array.prototype.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes):
  boolean
* [Array.prototype.some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some):
  boolean
* [Array.isArray()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray):
  boolean

### Search

* [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find):
  first value || undefined
* [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter):
  new results array || empty array
* [Array.prototype.findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex):
  index of the first element || -1
* [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf):
  index of the first element || -1
* [Array.prototype.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf):
  last index of the element || -1

### Non-destructive manipulation

* [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat):
  new array, shallow copy
* [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice):
  new array containing the extracted elements, shallow copy

### In place manipulation, destructive

* [Array.prototype.reverse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse):
  reversed modified array
* [Array.prototype.copyWithin()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin):
  modified array
* [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort):
  sorted modified array
* [Array.prototype.splice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice):
  array containing the deleted elements || empty array

### Conversion

* [Array.prototype.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join):
  a string with all array elements joined || empty string
* [Array.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString):
  a string representation
* [ref:
  Array.prototype.toLocaleString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString):
  a string representation

### Iteration

* [Array.prototype.forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach),
  undefined

## Typed Arrays

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays)
* [exploringjs.com](https://exploringjs.com/impatient-js/ch_typed-arrays.html)

JavaScript typed arrays are array-like objects and provide a mechanism for accessing raw binary data.

Typed Arrays are used much like normal Arrays with a few notable differences:

* Typed Arrays store their data in ArrayBuffers.
* All elements are initialized with zeros.
* All elements have the same type. Writing values to a Typed Array coerces them to that type. Reading values produces normal numbers or bigints.
* The length of a Typed Array is immutable; it can’t be changed.
* Typed Arrays can’t have holes.

If you are dealing with Arrays of integers or floats, consider Typed Arrays, which were created for this purpose. 

The main uses cases for Typed Arrays, are:

* Processing binary data
* Interacting with native APIs (WebGL, etc.)

### ArrayBuffer, Typed Arrays, DataView

* [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)
* [DataView](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView)

Binary data should be stored in instances of *ArrayBuffer*. If you want to access ArrayBuffer data, you must wrap it in another object - a view object.

View objects:

* Typed Arrays: let you access the data as an indexed sequence of elements that all have the same type.
* DataViews: let you interpret the data as various types that you can read and write at any byte offset.

## Array-like objects

* [exploringjs.com](https://exploringjs.com/impatient-js/ch_arrays.html#array-like-objects)

Array-like object:

* Holds the `.length` of the Array-like object.
* Holds the element at index `[0]`.

Array-like objects are relatively rare in modern JavaScript. Array-like objects used to be common before ES6; now you
don’t see them very often.

Converting iterable and Array-like values to Arrays can be done with Array spreading or with `Array.from()`.
