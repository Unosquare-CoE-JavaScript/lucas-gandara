# You don't know Js yet: Scopes & Closures

## Chapter 1: What's the Scope?
The way Js know which variables are accessible by any given statement is a set of well defined rules called _Scope_. Since Js functions are _first-class values_ (which means that they can be assigned and passed around just like any other values such as numbers and strings) and can hol variables, they keep their scope no matter where they are called and this is called a _Closure_.

The previous discussion whether Js is a compiled or interpreted language matters because the Scope is determined during compilation time. Is then important to understand how compilation process work.