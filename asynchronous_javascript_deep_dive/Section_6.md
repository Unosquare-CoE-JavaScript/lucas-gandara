# Asynchronous Javascript deep dive
## Section 6: Making Use of Generators.
A _Generator_ is a way to write code that you can pause and then continue a later time. When you start a generator function you can exit that function without running all its code and then re enter that function where you left, this is achieved by using the keyword _yield_ and prefixing the function name with an _*_:
```js
function *myGenerator() {
  let x = 0;
  x++;
  yield;
  x++;
  yield;
}

let generator = myGenerator();
console.log(generator.next());
// { value: 1, done: false }

console.log(generator.next());
// { value: 2, done: false }

console.log(generator.next().done);
// true
```
An example use of generator could be a function that generates random numbers like so:
```js
const randomNum = function *(end) {
  while (true) {
    let random = Math.floor(Math.random() * end) + 1;
    yield random;
  }
}

let random100 = randomNum(100);
// random number generator from 0 to 100

random100.next()
// 13 *random number
```
To create an iterator you need to define the _symbol iterator_ as part of the the object you want to iterate over:
```js
const arr = [1, 2, 3, 4];

// Since an array already has an iterator:
console.log(arr[Symbol.iterator]);
// f values()

// You can then re define how to iterate over it:
arr[Symbol.iterator] = function *() {
  for (let i = 3; i >=0; i--) {
    yield this[i];
  }
}

for (let v of arr) {
  console.log(v)
}
// 4
// 3
// 2
// 1
```