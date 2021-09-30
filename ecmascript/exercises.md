# Exercises

---

PEMDAS and coercion to string happens only on addition

```js
console.log(1 + 4 * 2 + 7 - '6' + '4' * 5 + '3' - '12') // 291

console.log(1 + 8 + 7 - '6' + 20 + '3' - '12')
console.log(30 + '3' - '12')
console.log('303' - '12')
```

---

Shortcircuiting

```js
console.log(false && true);
console.log(false && 1 && []);
console.log(" " && true && 5);
console.log(null || 0 || undefined);
console.log(null || 1 || undefined);
```

---

```js
for(var i = 0; i < 3; i++){
  setTimeout(function() {console.log(i)}, 0);

  console.log(i)
}
```

Output: 1,2,3 and then 3 three times since variable declared with `var` keyword does not have block scope. Also, inside
the `for` loop, the variable `i` is incremented first, and then checked.

---

```js
(function(){
  setTimeout(()=> console.log(1),2000);

  console.log(2);

  setTimeout(()=> console.log(3),0);

  console.log(4);
})();
```

Output: 2 4 3 1

Even though the second timeout function has a waiting time of zero seconds, the JavaScript engine always evaluates the
`setTimeout` function using the Web API and therefore, the complete function executes before the `setTimeout` function can
execute. See event loop and asynchronicity.

---

```js
const x = {};
const y = {name: "Alice"}
const z = {name: "Bob"};

x[y] = {name:"Yan"};
x[z] = {name:"Zachary"};

console.log(x[y]);
```

Output: `{name: "Zachary"}`

While setting a property of an object, JavaScript coerces the parameter into a string. Therefore, since `y` is an
object, it will be converted to "object Object". `x[x]`, `x[y]` and `x[z]` will be coerced to the same property name.

---

```js
let hero = {
  powerLevel: 99,
  getPower() {
    return this.powerLevel;
  }
}
  
let getPower = hero.getPower;

var powerLevel = 97;

console.log(getPower()); 
```

Output: 97

When the function is *called*, it is invoked referencing the global object. `var` declaration in global scope is added
to window object.

---

```js
var name = 'Window object'

const a = function fnA() {
  console.log('a', this.name);

  const b = {
    fnB: function() {
      console.log('b', this.name);
    }  
  }

  const c = {
    fnC: () => {
      console.log('c', this.name);
    }
  }
  
  const d = function() {
    console.log('d', this.name);
  }

  b.fnB(); 
  c.fnC(); 
  d(); 
}

a();
```

Output:

"a", "Window object"
"b", undefined
"c", "Window object"
"d", "Window object"

`this` depends on the call site. `this.name` has nothing to do with
[Function.name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name)
property.

`var` declaration is assigned to global object.

---

```js
var name = 'Window object'

const b = {
  name:"Alice",
  func: function() {
    var person = this;

    console.log('a', this.name);

    (function(){
      console.log('b', this.name);
      console.log('c', person.name);
    })();
  }
}

b.func();
```

Output:

"a", "Alice"
"b", "Window object"
"c", "Alice"

"c" prints Alice because `person` is in closure.

---

```js
var a = 1;

(function outer(a){
  return (function inner(){
    console.log(a);

    a = 3;
  })()
})(2);
```

Output: 2

Even though argument `a` of the outer function is passed down from IIFE, due to closure and lexical scope the inner
functions has access to it.

---

Implement even number test function with binary operator:

```js
function isEven(n) {
  return !(n & 1)
}
```

* [Bitwise AND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_AND)

## Hoisting

```js
let a = f();
const b = 2;
function f() { return b; }

console.log(a)
```

Output: "ReferenceError: can't access lexical declaration 'b' before initialization"

---

```js
console.log(y);

y = 1;
```

Output: "ReferenceError: y is not defined"

Missing var, let or const.

---

```js
console.log(y);

var y = 2;
```

Output: undefined

---

```js
y = 3;

console.log(y);

var y;
```

Output: 3

---

```js
var z = 1;
let z;

console.log(z);
```

Output: "SyntaxError: Identifier 'z' has already been declared

---

```js
console.log(z);

let z = 1;
```

Output: "ReferenceError: Cannot access 'z' before initialization

---

```js
function hoistingExample() {  
  console.log(a); 
} 

console.log(a);

var a = 1;

hoistingExample();
```

Output: 

undefined
1

---

```js
let text = 'a';

function logIt(){
  console.log(text);

  var text = 'b';
};

logIt();
```

Output: undefined

---

```js
let text = 'a';

function logIt(){
  console.log(text);

  let text = 'b';
};

logIt();
```

Output: "ReferenceError: can't access lexical declaration 'text' before initialization"

---

```js
function logFunction() {
  console.log(this === window);
}

logFunction(); 
new logFunction();
```


Output: 

true, because logFunction() is executed as property of window
false, refers to an object created with new keyword

---

## Arrays

* [Array intersection, difference, and union in ES6 - medium.com](https://medium.com/@alvaro.saburido/set-theory-for-arrays-in-es6-eb2f20a61848)


```js
const arrA=[1,2,3];
const arrB=[1,2,4];
```

---

Intersection: Elements present in both arrays.

```js
arrA.filter(x => arrB.includes(x));
```

Output: [1,2]

---

Difference: Will output the elements from array A that are not in the array B.

```js
arrA.filter(x => !arrB.includes(x));
```

Output: [3] 

---

Union: Distinct elements from both arrays.

```js
[...(new Set([...arrA, ...arrB]))];
```

Output: [ 1, 2, 3, 4 ]

---

Symmetrical difference: An array containing all the elements of array A that are not in array B and vice-versa.

```js
arrA
  .filter(x => !arrB.includes(x))
  .concat(arrB.filter(x => !arrA.includes(x)));
```

Output: [3, 4]

---
