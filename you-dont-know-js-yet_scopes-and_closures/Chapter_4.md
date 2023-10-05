# You don't know Js yet: Scopes & Closures

## Chapter 4: Around the Global Scope.
It might seem just obvious that the global scope of the application is in the outermost portion of a file. Depending on the environment, the global scope can be accessed through different browser-hosted dependant exposed variable, int the case of browsers this variable is called _window_.

always use var for globals. Reserve let and const for block scopes.

One surprising behavior in the global scope you may en-counter with browser-based JS applications: a DOM element with an id attribute automatically creates a global variable that references it. Consider this markup:

```html
<ul id="my-todo-list">
  <li id="first">Write a book</li>
  ..
</ul>
<script>
  console.log(first);
  // <li id="first">..</li>

  console.log(window["my-todo-list"]);
  // <ul id="my-todo-list">..</ul>
</script>
```
If the id value is a valid lexical name (like first), the lexical variable is created. If not, the only way to access that global is through the global object (window[..]).

    Though this is possible, never use the global variables to access DOM elements even though they will always be silently created.

### Web workers
Web Workers are a web platform extension on top of browser-JS behavior, which allows a JS file to run in a completely separate thread (operating system wise) from the thread that’s running the main JS program.

Just as with main JS programs, var and function declarations create mirrored properties on the global object (aka,self), where other declarations (let, etc) do not.

### ES Modules(ESM)
Every module creates it's own _global Scope_. Global variables are not created when in a top file of a module, instead they're global just for the module, so is "module global".

### Standardized way to access global Scope.
As of ES2020, JS has finally defined a standardized reference to the global scope object, called globalThis. So, subject to the recency of the JS engines your code runs in, you can use globalThis in place of any of those other approaches.
