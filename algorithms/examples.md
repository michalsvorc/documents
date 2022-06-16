# Examples

## Binary search

```javascript
const binarySearch = function (array, searchValue, startIndex = 0, endIndex = array.length - 1) {
  if (startIndex > endIndex) return false;

  const middleIndex = Math.floor((startIndex + endIndex) / 2);

  if (array[middleIndex] === searchValue) {
    return true;
  } else if (array[middleIndex] > searchValue) return binarySearch(array, searchValue, startIndex, middleIndex - 1);
  else return binarySearch(array, searchValue, middleIndex + 1, endIndex);
};

let array = [1, 3, 5, 7, 8, 9];

console.log(binarySearch(array, 6));
```

## Arithmetic progression

- [Wikipedia](https://en.wikipedia.org/wiki/Arithmetic_progression)

Write a function sumTo(n) that calculates the sum of numbers 1 + 2 + 3 + n.

Arithmetic progression formula:

```javascript
function sumTo(n) {
  return (n * (1 + n)) / 2;
}

console.log(sumTo(5)); // 15
```

## Fibonacci number

- [Wikipedia](https://en.wikipedia.org/wiki/Fibonacci_number)

The sequence of Fibonacci numbers has the formula `F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub>`.

The next number is a sum of the two preceding ones.

Fibonacci sequence: 1,1,2,3,5,8,13,21

Return n-th numer in the sequence.

Under some older definitions, the value `F0 = 0` is omitted, so that the sequence starts with `F1 = F2 = 1`.

### Recursion solution

Recursive solution by itself has too big Big O notation for high n-th number.

```javascript
function fib(n) {
  if (Math.sign(n) === -1) throw new Error("Negative number");

  if (n < 2) return n;

  return fib(n - 1) + fib(n - 2);
}

console.log(fib(8)); // 21
```

Recursion visualition:

```javascript
(fib(3) + fib(2))(fib(2) + 1) + (1 + 0)(1 + 0 + 1) + (1 + 0);
```

### Recursion solution + memo

```javascript
function fib(n, memo = new Map()) {
  if (n < 2) return n;

  if (memo.has(n)) return memo.get(n);

  const result = fib(n - 1, memo) + fib(n - 2, memo);

  memo.set(n, result);

  return result;
}

console.log(fibMemo(8)); // 21
```

### Tail recursion

```javascript
function fibTail(n, a = 0, b = 1) {
  if (n === 0) return a;
  if (n === 1) return b;

  return fibTail(n - 1, b, a + b);
}

console.log(fibTail(6)); // 8
```

Recursion visualition:

```javascript
console.log(fibTail(6))(
  // 8

  6,
  0,
  1
)(5, 1, 0 + 1)(4, 1, 1 + 1)(3, 2, 1 + 2)(2, 3, 2 + 3)(1, 5, 3 + 5); // n === 1, b is returned (3+5)
```

## Test for prime number

Prime number sequence: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97

### Loop

```javascript
function isPrime(n) {
  if (num === 1) return false;

  for (let i = 2; i < num; i++) {
    if (num % i === 0) return false;
  }

  return true;
}

console.log(isPrime(3)); // true
```

### Recursion

```javascript
function isPrime(n) {
  if (n === 2 || n === 3) return true;
  if (n % 2 === 0) return false;

  // https://en.wikipedia.org/wiki/Prime_number#Trial_division
  const dividerLimit = Math.floor(Math.sqrt(n));

  function isPrimeRecursion(n, i) {
    if (n % i === 0) return false;
    if (i >= dividerLimit) return true; // exhausted all other options, this is prime

    return isPrimeRecursion(n, i + 2); // try to divide with odd numbers only
  }

  return isPrimeRecursion(n, 3);
}

console.log(isPrime(3)); // true
```
