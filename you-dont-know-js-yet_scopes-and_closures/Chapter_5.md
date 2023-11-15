# You don't know Js yet: Scopes & Closures

## Chapter 5: The (Not so) secret lifecycle of Variables
If a variable declaration appears past the first statement of a scope, how will any references to that identifier before the declaration behave? What happens if you try to declare the same variable twice in a scope?

A function declaration is hoisted and initialized to its function value. A var variable is also hoisted, andthen auto-initialized to undefined

### Loops
Consider:
```js
var keepGoing = true;
while (keepGoing) {
  let value = Math.random();
  if (value > 0.5) {
    keepGoing = false;
  }
}
```
It doesn't throw an error because each loop iteration is its own scope instance. This means that you could use _const_ safely here.
