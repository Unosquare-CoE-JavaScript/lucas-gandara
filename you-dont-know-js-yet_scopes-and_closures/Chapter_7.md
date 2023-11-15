# You don't know Js yet: Scopes & Closures

## Chapter 7: Using Closures
The main purpose of understanding in deep the _Scope_ is to now understand and use effectively _Closures_. For variables that are needed to be used across the entire program, instead of placing them in larger or the most outer scope, we can encapsulate them in a more narrow scope but still having access to them from the functions we need.

    If you've ever written a callback that accesses variables outside its own scop, that's a closure.

Closure is a behavior for function and only functions. An object can not have closure, nor does a class. For closure to be observed, the function must be called from another branch of the scope than it was originally created. Consider:
```js
// outer/global scope (1).
function lookupStudent(studentID) {
  // function scope (2).
  var students = [
    { id: 14, name: "Kyle" },
    { id: 73, name: "Suzy" },
    { id: 112, name: "Frank" },
    { id: 6, name: "Sarah" }
  ];

  return function greetStudent(greeting) {
    // function scope (3).
    var student = students.find(
      student => student.id == studentID
    );
    return `${ greeting }, ${ student.name }!`;
  };
}
var chosenStudents = [
  lookupStudent(6),
  lookupStudent(112)
];

// accessing the function's name:
chosenStudents[0].name;
// greetStudent

chosenStudents[0]("Hello");
// Hello, Sarah!

chosenStudents[1]("Howdy");
// Howdy, Frank!
```
Here, _Closure_ allows the _greetStudent_ function to access the _student_ variable even though when the lookupStudent function already Scope is finished. Instead of the instances of students and studentID being GC’d,they stay around in memory. At a later time when either instance of the _greetStudent_ functions are invoked those variable still exist.

The most cited example of Closures:
```js
function adder(n) {
  return function addTo(x) {
    return n + x;
  }
}
var add10To = adder(10);
var add42To = adder(42);

add10To(20);
// 30

add42To(8);
// 50
```
Here, each instance of the _adder_ functions is closing over their own _n_ and _x_ variables, this means, even though adder function Scope is finished, it can still be accessible through their returned references _add10To_ and _add42To_. Keep in mind that this reference is not read only, we can reassign it as well. 

A misconception that could rise is the fact that we can close over values instead of variables, consider:
```js
var studentName = 'Lucas';

var greeting = function hello() {
  // Here, we're closing over studentName variable
  // not over the value 'Lucas'
  console.log('Hello: ', studentName);
}

studentName = 'UnoSquare';

greeting();
// UnoSquare
```
The formal definition of a _Closure_:

    Closure is observed when a function uses variable from outer scope even while running in a scope where those variable(s) wouldn’t be accessible.

### The Closure LifeCycle and Garbage Collection.
When a variable is not needed in any Scope anymore is removed and collected by the garbage collector, that's why is important to keep in mind and being aware of how to use closures, a wrong usage could lead into a variable being hold for no reason, this has a cost in the memory.

Conceptually, closure is per variable rather than per scope.