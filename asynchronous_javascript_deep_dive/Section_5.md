# Asynchronous Javascript deep dive
## Section 5: Async await.
An _async_ function declaration creates a binding of a new async function to a given name. The _await_ keyword is permitted within the function body, enabling asynchronous, promise-based behavior to be written in a cleaner style and avoiding the need to explicitly configure promise chains.
```js
function resolveAfter2Seconds() {
  return new Promise((resolve) => {
    setTimeout(() => {	
      resolve('resolved');
    }, 2000);
  });
}

async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
  // "resolved"
}

asyncCall();
```
Since now wer are dealing with "Synchronous" code we have to somehow deal with errors, that's why is mandatory to surround our await calls with a _try catch_ block.