# You don't know Js yet: Scopes & Closures

## Chapter 3: The Scope Chain.
### Shadowing:
Consider:
```js {.line-numbers}
var studentName = 'Suzy';

function printStudent(studentName) {
  studentName = studentName.toUpperCase();
  console.log(studentName);
}

printStudent('Frank');
// FRANK

console.log(studentName);
// Suzy
```

Two things are happening here, first, as mentioned in book 1, you can not create references to primitives values, that's why even though in the _printStudent_ function we are re assigning the value of studentName to be upper case, the global value of the function remains the same, When you do this intentionally is called shadowing, since there is no way that in the _printStudent_ lexical scope we can access the global reference to the variable _studentName_.

    is technically possible, however is a bad practice to do it, accessing to the global variable _windows_.

It's also important to note that other forms of global scope declarations do not create mirrored global object properties:

```js
var one = 1;
let notOne = 2;
const notTwo = 3;
class notThree {}

console.log(window.one);      // 1
console.log(window.notOne);   // undefined
console.log(window.notTwo);   // undefined
console.log(window.notThree); // undefined
```

### Arrow functions.
ES6 added an additional function expression form to the language, called “arrow functions”:
```js
var myFunction = () => {
  //...
}
```
When _{...}_ used, a _return_ statement is needed.

Arrow functions are lexically anonymous, meaning they have no directly related identifier that references the function.The assignment to askQuestion creates an inferred name of“askQuestion”, but that’s **not the same thing as being non-anonymous**.

An often misconception of the arrow functions is that they don't add lexical scope, **They do** and behave exactly the same as a functions scope.
