# You don't know Js yet: Scopes & Closures

## Chapter 8: The Module pattern.
### What is a Module?
A module is a collection of related data and functions (often referred to as methods in this context), characterized by a division between hidden private details and public accessible details, usually called the “public API.”

### Namespaces (Stateless Grouping)
If you group a set of related functions together, without data, then you don’t really have the expected encapsulation a module implies. The better term for this grouping of stateless functions is a namespace:
```js
// namespace, not module
var Utils = {
  cancelEvt(evt) {
    evt.preventDefault();
    evt.stopPropagation();
    evt.stopImmediatePropagation();
  },
  wait(ms) {
    return new Promise(function c(res){
      setTimeout(res,ms);
    });
  },
  isValidEmail(email) {
    return /[^@]+@[^@.]+\.[^@.]+/.test(email);
  }
};
```

### Module definition:
- There must be an outer scope, typically from a module factory function running at least once.
- The module’s inner scope must have at least one piece ohidden information that represents state for the module.
- The module must return on its public API a reference to at least one function that has closure over the hidden module state (so that this state is actually preserved).

### Modern ES Modules (ESM)
```js
// Variables
export getName;


// functions
export function getName(studentID) {
  // ..
}

// Another variation
export default funtcion getName(studentId) {
  //..
}

// To use a module
import { getName } from "/path/to/students.js";
```