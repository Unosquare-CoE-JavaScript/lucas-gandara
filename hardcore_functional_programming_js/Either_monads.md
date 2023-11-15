# Hardcore Functional Programming in Javascript
## Monads
When making a _[Functor](Functors.md)_, it could happen that the function signatures are not compatible, for instance, if we have a square root function: `const square(int) => int * int;` and we are composing it:
```js
const x = 10;
console.log(square(square(x)));
// 1000
```
 and we'd like to add a log in the middle like so:
```js
const squareWithLog(int) => {
  log = `the value of x is: ${x}`
  return (int * int, log);
}
```
Suddenly we can no compose anymore since the expected inputs are not compatible, should we change the function _Square_ contract to accept now a log? No! We can leverage the monads which is just a variance of a functor that handles this parameter compatibility:
```js
const bind = (func, tuple) {
  response = func(tuple[0]);
  return (response[0], tuple[1] + response[1]);
}

// Now I can bind together the two functions
console.log(
  bind(square_with_print_return, (bind(square_with_print_return, unit(2))))
)
```
As you can see is a functor, but since we are handling parameter incompatibility is called a monad.