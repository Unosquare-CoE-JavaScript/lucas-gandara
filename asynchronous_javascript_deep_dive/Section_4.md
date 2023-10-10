# Asynchronous Javascript deep dive
## Section 4: Promises.
A _Promise_ is a proxy for a value not necessarily known when the promise is created. A _promise has one of these states:
- Pending: Initial state, neither fulfilled nor rejected.
- Fulfilled: meaning that the operation was completely successfully.
- Rejected: meaning that the operation failed.

The eventual state of a pending promise can either be fulfilled with a value or rejected with a reason (error). When either of these options occur, the associated handlers queued up by a promise's then method are called. If the promise has already been fulfilled or rejected when a corresponding handler is attached, the handler will be called, so there is no race condition between an asynchronous operation completing and its handlers being attached.

    A promise is said to be settled if it is either fulfilled or rejected, but not pending.

### Fetch API
Fetch API is a property defined as part of the window object, is not a feature of javascript itself. The _Fetch API_ provides a JavaScript interface for accessing and manipulating parts of the protocol, such as requests and responses. It also provides a global _fetch()_ method that provides an easy, logical way to fetch resources asynchronously across the network. Since a fetch call could take reasonably amount of time, is the perfect candidate to use promises on.
```js
const apiRoot = 'https://swapi.dev/api/films/1/';

fetch(apiRoot)
.then(response => response.json())
.then(people => console.log(people.title))
// A New Hope

// Example with JQuery
$.getJSON(apiRoot)
.then(response => console.log(response));
// A New Hope
```

### Promise Constructor
The _Promise_ constructor creates _Promise_ objects. It's primary used to wrap callback-based APIs that do not already support promises. It receives an executor parameter which is a _function_ to be executed by the constructor. It receives two functions as parameters: _resolveFunc_ and _rejectFunc_. Any errors thrown in the _executor_ will cause the promise to be rejected, and the return value will be neglected.

A promise then, has 3 instance methods that can be called:

#### Promise.prototype.catch()
Appends a rejection handler callback to the promise, and returns a new promise resolving to the return value of the callback if it is called, or to its original fulfillment value if the promise is instead fulfilled.

#### Promise.prototype.then()
Appends a handler to the promise, and returns a new promise that is resolved when the original promise is resolved. The handler is called when the promise is settled, whether fulfilled or rejected.

#### Promise.prototype.finally()
Appends fulfillment and rejection handlers to the promise, and returns a new promise resolving to the return value of the called handler, or to its original settled value if the promise was not handled (i.e. if the relevant handler _onFulfilled_ or _onRejected_ is not a function).

```js
const wrappedFunction = new Promise((reject, resolve) => {
  // Your callback.based code goes here.
})

wrappedFunction
.then(response => /* you code goes here... */)
.catch(error => /* Your error handler goes here... */)
.finally(() => {
  /* a callback to be called no matter the promise got
  resolved or rejected */
});
```

### The promise race (Promise concurrency)
When you have multiple variables, you have tools to facilitate the async task at the same time rather than handle each promise separately when needed:

#### Promise.all(iterable)
The _Promise.all()_ static method takes an iterable of promises as input and returns a single Promise. This returned promise fulfills when all of the input's promises fulfill (including when an empty iterable is passed), with an array of the fulfillment values. It rejects when any of the input's promises rejects, with this first rejection reason. Consider:
```js
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3])
.then((values) => {
  console.log(values);
});
// [3, 42, "foo"]
```

#### Promise.allSettled(iterable)
The _Promise.allSettled()_ static method takes an iterable of promises as input and returns a single Promise. This returned promise fulfills when all of the input's promises settle (including when an empty iterable is passed), with an array of objects that describe the outcome of each promise. Consider:
```js
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => setTimeout(reject, 100, 'foo'));
const promises = [promise1, promise2];

Promise.allSettled(promises)
.then((results) => {
  results.forEach((result) => console.log(result.status))
});
// "fulfilled"
// "rejected"
```

#### Promise.any(iterable)
The _Promise.any()_ static method takes an iterable of promises as input and returns a single Promise. This returned promise fulfills when any of the input's promises fulfills, with this first fulfillment value. It rejects when all of the input's promises reject (including when an empty iterable is passed), with an _AggregateError_ containing an array of rejection reasons. Consider:
```js
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 100, 'quick'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 500, 'slow'));

const promises = [promise1, promise2, promise3];

Promise.any(promises).then((value) => console.log(value));
"quick"
```

### Promise.race(iterable)
The _Promise.race()_ static method takes an iterable of promises as input and returns a single Promise. This returned promise settles with the eventual state of the first promise that settles.
```js
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one');
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
  // Both resolve, but promise2 is faster
});
"two"
```

#### Can I abort a Promise?
Even though is not something that is done frequently, it could happen that you want to cancel a promise, this can be done with the _AbortController_. Just keep in mind that is not part of the ECMAScript Spec but rather a Browser feature. You can pass the returned object of the _AbortController_ which is called a _signal_.
```js
// Creation of an AbortController signal
const controller = new AbortController();
const signal = controller.signal;

// Call a promise, with the signal injected into it
doSomethingAsync({ signal })
	.then(result => {
		console.log(result);
	})
	.catch(err => {
		if (err.name === 'AbortError') {
			console.log('Promise Aborted');
		} else {
			console.log('Promise Rejected');
		}
	});
```
An asynchronous functions that takes signals into account could be defined like so:
```js
// Example Promise, which takes signal into account
function doSomethingAsync({signal}) {
	if (signal.aborted) {
		return Promise.reject(new DOMException('Aborted', 'AbortError'));
	}

	return new Promise((resolve, reject) => {
		console.log('Promise Started');

		// Something fake async
		const timeout = window.setTimeout(resolve, 2500, 'Promise Resolved')

		// Listen for abort event on signal
		signal.addEventListener('abort', () => {
			window.clearTimeout(timeout);
			reject(new DOMException('Aborted', 'AbortError'));
		});
	});
}
```
To abort the promise:
```js
document.getElementById('stop').addEventListener('click', (e) => {
	e.preventDefault();
	controller.abort();
});
```