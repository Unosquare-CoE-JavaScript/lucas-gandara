# Hardcore Functional Programming in Javascript
## Pre - concepts
- **Pure functions**: a pure function has three characteristics which are that has to be **total**, this means that for any input, there's have to be an output. The second one is that is has to be **deterministic** which means that for an input, the output has to always be the same. The third one is that a function should not have any observable side - effects which means that can no modify anything from the outside.
```js
// Not a functions, since is mutating the user object
const birthday = user => {
  user.age += 1;
  return user;
}

// Pure function, is total, deterministic and no side-effects.
const shout = word => 
  word.toUpperCase().concat('!');
```

## Currying
To define what _Currying_ is, first we have to define what _[Lambda Calculus](https://en.wikipedia.org/wiki/Lambda_calculus)_. Lambda Calculus (λ-Calculus), originally created by Alonzo Church, is the world's smallest programming language. Despite not having numbers, strings, booleans, or any non-functional data types, the lambda calculus can be used to represent any Turing machine.

Lambda calculus is made up of 3 elements: **variables, functions and applications**:

|Name|Syntax|Example|Explanation|
|----|------|-------|---------- |
|Variable|\<name>|x|A variable called 'x'|
|Function|λ\<parameter>.\<body>|λx.x|A function with parameter 'x' and body 'x'
|Application|<function><variable or function>|(λx.x)a|A call to the function '(λx.x)a' with argument a

With that in mind we can now introduce the concept of _Currying_, which is the decomposition of a lambda expression into more lambda expression. Consider:
```js
function sum(a, b) {
  return a + b;
};

function curriedSum(a) {
  return (b) => {
    return a + b;
  }
}

curriedSum(a)(b) === sum(a, b)
// true
```
This concept also leverages the feature of javascript of _closures_ since the inner function closes over the upper variable _a_.
