# Hardcore Functional Programming in Javascript
## Composition
In mathematics, **function composition** is an operation $\circ$ takes two functions $f$ and $g$, and produces the function $h = g \circ f$ such that $h(x) = g(f(x))$. In this operation, the function $g $is applied to the result of applying the function $f$ to $x$.

In programming, this is achieved with functions as so:
```js
const exclaim = str => str + '!';
const toUpper = str => str.toUpperCase();


const compose = (f, g) => x => f(g(x))

const shout = compose(exclaim, toUpper);


console.log(shout('hello world'));
// HELLO WORLD!
```
The final result is a string that is appended a '!' and then turned to upper case. Is possible to compose as many functions as you need.

At this point, is then possible to have _Currying_ and function _Composition_ together like so:
```js
const doStuff = _.compose(
  join(''),
  _.filter(x => x.length > 3),
  reverse,
  /*
  etc
  */
)
```
An example of a complex composition case could be:
```js
// Refactor availablePrices with compose.

let availablePrices = function (cars) {
    const available_cars = _.filter(_.prop('in_stock'), cars);
    return available_cars.map(x => formatMoney(x.dollar_value)).join(', ');
}

availablePrices = _.compose(_.join(', '), formatMoney, _.map(_.prop('dollar_value')), _.filter(_.prop('in_stock')));

QUnit.test("Bonus 1: availablePrices", assert => {
    assert.deepEqual(availablePrices(CARS), '$700,000.00, $1,850,000.00');
})
```
Note that we are using [rambda](https://ramdajs.com/docs/#prop) library and [accounting](http://openexchangerates.github.io/accounting.js/) library.