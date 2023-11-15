# You don't know Js yet: Scopes & Closures

## Chapter 1: What's the Scope?
The way Js know which variables are accessible by any given statement is a set of well defined rules called _Scope_. Since Js functions are _first-class values_ (which means that they can be assigned and passed around just like any other values such as numbers and strings) and can hol variables, they keep their scope no matter where they are called and this is called a _Closure_.

The previous discussion whether Js is a compiled or interpreted language matters because the Scope is determined during compilation time. Is then important to understand how compilation process work.

### The compilation process:
In the traditional compiled-language process, the program will undergo typically, three steps before it is executed, roughly called _compilation_:
- Tokenizing
- Parsing
- Code generation

Is important to mention that the compilation process is much more complex, but for the sake of simplicity we stick to these 3 steps which are:

Tokenizing consist of turning the string of characters (the raw file) into a meaningful pieces called tokens, for instance:
```js
var foo = 5;
// This program would generate thw following tokens:
// var, foo, =, 5 and ;
```

Parsing then consist on taking a stream of tokens and convert them into a tree of nested elements, which altogether represent a grammatically structure of the program, this trees are called Abstract Syntax Tree(AST).

Lastly the code generation takes this AST and convert it to executable code.

The code being compiled and parsed before executions brings some features which can be listed next:

1. Syntax Errors from the Start
  
    Consider:
    ```js
    var greeting = "Hello";
    console.log(greeting);
    greeting = ."Hi";
    // SyntaxError: unexpected token .
    ```
    This code won't have any output even though the first two lines are well formed, instead a SyntaxError exception is thrown at compilation time.

2. Early errors
    
    Now consider:
    ```js
    console.log("Howdy");
    saySomething("Hello","Hi");
    // Uncaught SyntaxError: Duplicate parameter name not
    // allowed in this context

    function saySomething(greeting,greeting) {
      "use strict";
      console.log(greeting);
    }
    ```
    Even though the strict mode is set on a function lastly defined, the parsing process inform about this error, which in this case is caused because the _strict_ mode doest not allow to have duplicate parameter names in functions.

3. Hoisting

    Variables declarations in Js are assigned to memory during compilations time. A more easy way to understand this concept is to think about as moving the declaration of the variables to the top of their scopes.
    
    Consider:
    ```js
    catName("Maurizzio");

    function catName(name) {
      console.log("The name of my cat is: " + name);
    }
    // The result would be: "The name of my cat is: Maurizzio"
    ```

### Targets and sources.
In a Js program, all occurrences of a variables can serve either one of this roles: _target_ of an assignment or _source_ of a value. To distinguish between one another is just to check wether a value is being assigned to it, if so it's a target, otherwise is a source.

### A way to cheat the current Scope.
The _eval_ keyword is a way to run on the fly Js code, is a bad practice to use it as a modifier of the current scope. However there is another way. This is the _with_ keyword which essentially dynamically turns an object into a local scope its properties are treated as identifiers in that new scope’s block:
```js
const badIdea = { oops: 'Ugh!' };

with (badIdea) {
  console.log(oops); // Ugh!
}
```
The global scope was not modified here, but _badIdea_ was turned into a scope at runtime rather than compile time and its _oops_ property becomes available in that scope.

### Lexical Scope
"Lexing" is associated with the "lexing" stage of the compilation process.If you place a variable declaration inside a function, the compiler handles this declaration as it’s parsing the function,and associates that declaration with the function’s scope. Ifa variable is block-scope declared (let / const), then it’s associated with the nearest enclosing { .. } block, rather than its enclosing function (as with var).
