# You don't know Js yet: Scopes & Closures

## Chapter 6: Limiting Scope Exposure
In software engineering there is always going to be bugs, this is for sure, what we can do about it is to follow some rules to try to minimize this number, one way of doing it is by applying this rule related with scopes: _POLE_ (The principle of Least Privilege). In following POLE, what do we want to minimize the expo-sure of? Simply: the variables registered in each scope. There are some other pros:

- **Naming collisions**.
- **Unexpected behaviors**: Don't allow functions where are not supposed to.
- **Unintended dependency**: This creates unnecessary dependency that could be a hazard in the future.

### Hiding in Plain (function) scopes
consider this pieces of code that recursively calculates the facrotial of a number:
```js
var cache = {};

function factorial(n) {
  if (n < 2) return 1;
  
  if (! (n in cache) ) {
    cache[n] = n * factorial(n - 1);
  }
  return cache[n];
};

factorial(6);
// 120

factorial(7);
// 5040
```
Wouldn't be a way to hide the cache variable into the factorial function? It'd make more sense to be part of it, or better said, wouldn't make sense to be part of the outer scope. The answer is Yes, and we use the concepts of Scope we've just studied and closures, we encapsulate the _cache_ variable into another:
```js
// Outer global scope
function factorialCacheHidden() {
  // Middle scope, where we are going to hide the cache variable.
  var cache = {};

  function factorial(n) {
    if (n < 2) return 1;
    
    if (! (n in cache) ) {
      cache[n] = n * factorial(n - 1);
    }
    return cache[n];
};

  return factorial;
}

var factorial = factorialCacheHidden();

factorial(6);
// 120

factorial(7);
// 5040
```
The _factorialCacheHidden_ function serves no other purpose than to create a scope for cache to persist in across multiple calls to _factorial(n)_.

    Note:
    Keep in mind that in this example we are optimizing the multiple calls of factorial but this comes with a price which is memory. This technique is also called memoization which is spread used in functional programming, however the memory management is managed differently to not cause leaks.

To not have _factorialCacheHidden_ function in the outer scope, it can be contained in an IIFE to be part of the same scope as the cache itself:

An IIFE is useful when we want to create a scope to hide variables/functions. Since it’s an expression, it can be used in any place in a JS program where an expression is allowed.

Not every curly braces {...} with expressions in it creates scopes:

- Object literals use { .. } curly-brace pairs to delimit their key-value lists, but such object values are not scopes.
- class uses { .. } curly-braces around its body definition, but this is not a block or scope.
- A function uses { .. } around its body, but this is not technically a block it’s a single statement for the function body. It is, however, a (function) scope.
- he { .. } curly-brace pair on a switch statement(around the set of case clauses) does not define a block/scope.

The book recommends to never over expose a variable more than needer, consider:
```js
if (somethingHappened) {
  {
    let msg = somethingHappened.cause;
    notify(msg);
  }
  recoverFromError();
}
```
In this snippet of code we are creating a block and a scope just to send a notification error, this makes sense since the _msg_ variable is only being used in the next line and in the rest of the body of the function is not necessary to have created a variable _msg_, this avoid future naming collisions.

### Where using _let_ and _var_ ? (recommendation from the book)
The way to decide is to ask "What is the most minimal scope exposure that’s sufficient for this variable?". If a declaration belongs in a block scope, use _let_. If it belongs in the function scope, use _var_.

### Function declaration in Blocs (Fib)
You can create functions conditionally like so:
```js
if (true) {
  function ask() {
    console.log('is this going to work?');
  }
}

ask();
// is this going to work?
```
As you can se, even though the function is declared inside an _if_ statement, the function _ask_ is still being created and added to the outer scope. Use it carefully though, because some legacy engines could treat this in a different way.
