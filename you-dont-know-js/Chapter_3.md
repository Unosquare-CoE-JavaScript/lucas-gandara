# You dont know js yet

## Chapter 3: Digging to the root of Js.

### Iterators and iterables.
The _for .. of_ loop:

```js
const it = [1, 2, 3, 'Lucas']

for (let val of it) {
	console.log(val);
}
// 1
// 2
// 3
// 'Lucas'
```

The spread _..._ operator has two variations, spread and rest. Consider the following expression:

```js
// Spread operator used to "spread" a variable into an array
const it = [1, 2, 3, {nombre: 'Lucas', appellido: 'Gandara'}];
const [one, two, ...rest] = [...it]
console.log(rest[1] == it[3])

// Rest operator can used to gather together a set of variables into a single array.
function addTogether(...rest)
{
	console.log(rest);
	// [1, 2, 3]
	let accumulator = 0;
	for (val of rest)
	{
		accumulator += val;
	}
	return accumulator;
}

const result = addTogether(1, 2, 3);
console.log(result);
// 6

```

ES6 defined the basic data structure/collection types in JS asiterables. This includes strings, arrays, maps, sets, and others.

### The concept of shallow copy. (Taken from: [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy))
A shallow copy of an object is a copy whose properties share the same references (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you may also cause the other object to change too. That behavior contrasts with the behavior of a deep copy, in which the source and copy are completely independent.

More formally, two objects o1 and o2 are shallow copies if:

1. They are not the same object (o1 !== o2).
2. The properties of o1 and o2 have the same names in the same order.
3. The values of their properties are equal.
4. Their prototype chains are equal.

Consider:

```js
const x = [0, 1, 2, 3, {nombre: 'lucas'}]

const y = [...x];

y[4].nombre = 'mateo';
y[0] = 100;
console.log(y);
// [ 100, 1, 2, 3, { nombre: 'mateo' } ]

console.log(x)
// [ 0, 1, 2, 3, { nombre: 'mateo' } ];

console.log(x == y);
// false
```

The copy of an object whose properties all have primitive values fits the definition of both a deep copy and a shallow copy. 

In Js the only way you can have a reference to a primitive value is with closures. This is because Js is in charge of the memory management for you, you have no control over the heap and the stack.

All iterators in Js has this 3 properties:
- keys-only(keys())
- values-only(values())
- entries()

### Create your own iterator:
To create an iterator the object needs to have a propertie _Symbol.iterator_, which is a function that returns a _next_ function:

```js
// Could be any object
const myIterator = {}

// Make it iterable
myIterator[Symbol.iterator] = function() {
	let n = 0;
	let done = false;
	return {
		next() {
			n += 1;
			done = n > 4 ? true : false;
			return {value: n, done};
		}
	}
}

// The Symbol.iterator method is called automatically by for..of.
for (let num of myIterator) {
  console.log(num);
}
// 1
// 2
// 3
// 4
```

### Closures.
Definition taken from the book:

	Closure is when a function remembers and continues to access variables from outside its scope, even when the function is executed in a different scope.

Consider:

```js
function counter(step = 1) {
	var count = 0;
	return function increaseCount() {
		count = count + step;
		return count;
	};
}

let incrementBy5(5);

incrementBy5();
// 5
incrementBy5();
// 10
```

As mentioned before, a closure is the only way to create a reference to a primitive in Js.

### this Keyword.
When a function is defined, it is attached to its enclosing scope via closure and the Scope is the set of rules that controls how references to variables are resolved. The characteristic that defines the scope and what can a function access is called _execution context_ and it’s exposed to the function via its this keyword.

### Protoypes.
Prototype is a characteristic of an object and specifically resolution of a property access. A series of objects linked together via prototypes is called the "prototype chain".
Consider:
```js
let homework {
	topic: 'Js'
}
```
The homework object only has a single property on it: topic.However, its default prototype linkage connects to the Ob-ject.prototype object, which has common built-in meth-ods on it like toString() and valueOf(), among others.

The true importanceshines of _this_ when considering how it powers prototype-delegatedfunction calls. Indeed, one of the main reasons _this_ supportsdynamic context based on how the function is called is so thatmethod calls on objects which delegate through the prototypechain still maintain the expected _this_.