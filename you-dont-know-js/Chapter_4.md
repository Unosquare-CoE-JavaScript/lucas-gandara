# You dont know js yet

## Chapter 4: The Bigger Picture.

### Pillar 1: Scopes and Closures.
Scopes nest inside each other, and for any given expression orstatement, only variables at that level of scope nesting, or inhigher/outer scopes, are accessible; variables from lower/in-ner scopes are hidden and inaccessible.
This is how scopes behave in most languages, which is calledlexical scope. The scope unit boundaries, and how variablesare organized in them, is determined at the time the programis parsed (compiled). In other words, it’s an author-timedecision: where you locate a function/scope in the programdetermines what the scope structure of that part of the pro-gram will be.

when all variables declared anywhere in a scope are treated as if they’re declared at the beginning of the scope is called _hoisting_.

Consider:
```js
function mainFunc() {
    alert(name);
    var name = 'Jorden';
}
mainFunc();
```
When it is processed by a JavaScript engine it will be interpreted in this way:
```js
function mainFunc() {
  var name;
  alert(name);
  name = 'Jorden';
}
mainFunc();
// alert(name)displays it undefined instead of an error claiming that the variable does not exist.
```

If we were to use let instead:
```js
function mainFunc() {
  alert(name);
  let name = 'Michael';
}
mainFunc();
// Uncaught ReferenceError: Cannot access 'name' before initialization
```

We have to validate if nowdays this still causing errors.

### Pillar 2: Prototypes.
Javascript is protoype based, the difference with OOP can be subtle and thats why so many programmers are tempted to implement the OOP pattern. Those are different paradigms tho. Just remember that classes are not the only way to create objects and there is not only 2 paradigms, there are many.
