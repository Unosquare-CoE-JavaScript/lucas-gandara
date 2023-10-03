# You don't know Js Yet
## AppendixA: Exploring Further
### Values vs References
As mentioned in Chapter 3:
In Js the only way you can have a reference to a primitive value is with closures. This is because Js is in charge of the memory management for you, you have no control over the heap and the stack.

### Many ways to create a function
```js
var awesomeFunction = function(coolThings) {
// ..
return amazingStuff;
};

var awesomeFunction = function someName(coolThings) {
// ..
return amazingStuff;
};
awesomeFunction.

// generator function declaration
function* generator(i) {
  yield i;
  yield i + 10;
}

const gen = generator(10);

console.log(gen.next().value);
// Expected output: 10

// IIFE functions (Inmediately Invoked Function Expressions)
(function(){ .. })();
(function namedIIFE(){ .. })();

// async function declaration
async function three() { .. }
// async functions are out of the scope of this book.
```

### Coercive and Conditional comparisons
```js
var x = 'Hello';
console.log(Boolean(x))

if(x == true) {
  console.log('OK!')
}
// Whys this doesn't log 'OK!' ?
```

### Prototypal "Classes"
```js
function Classroom() {
// ..
}

Classroom.__proto__.greet = function greet() {
  console.log('Greeting')
}

console.log(Classroom.greet())
// Greeting
```

