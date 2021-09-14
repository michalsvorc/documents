# Functional programming utilities

## unary

* [Ramda](https://ramdajs.com/docs/#unary)
* [Lodash](https://lodash.com/docs/#unary)
* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#all-for-one)

Wraps a function of any arity (including nullary) in a function that accepts exactly 1 parameter. Any extraneous
parameters will not be passed to the supplied function.

## identity

* [Ramda](https://ramdajs.com/docs/#identity)
* [Lodash](https://lodash.com/docs/#identity)
* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#one-on-one)

This method returns the first argument it receives.

## constant

* [Lodash](https://lodash.com/docs/#constant)
* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#unchanging-one)

Creates a function that returns constant value.

## partial

* [Ramda](https://ramdajs.com/docs/#partial)
* [Lodash](https://lodash.com/docs/#partial)
* [Functional Light JS](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md#some-now-some-later)

Creates a function that invokes func with partials prepended to the arguments it receives. This method is like `.bind`
except it does not alter the this binding.

See also `partialRight`, `curry`.
