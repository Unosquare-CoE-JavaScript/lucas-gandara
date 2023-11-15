# Hardcore Functional Programming in Javascript
## Functors
Following the mathematical definition, and relating in the programing world in a very simple way, _functors_ are a mapping using a function $f(x)$ (or composite function $f(g(x))$ for instance) on a category _A_ generating a category _B_, creating a new image, respecting the _morphism_. In other words, is any object we can map and apply a function generating another object instance of the same type and connections. Consider:
```js
[1, 2, 3]
.map(val => val * 2);
.map(num => num + 4);
//generates [6, 8, 10]
```
This comes with some advantages, since we create a composition of functions, we create state but we don't have to think about them intermediately, we are just making a composition. At the end a functor is a container that holds an object that is mapped over.

To create the identity functor, you could use:
```js
const Box = x => ({
  map: f => Box(f(x)),
  fold: f => f(x),
  inspect: `Box(${x})`
})
```