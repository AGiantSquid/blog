When calling a function that calls a promise, you do not need an async/await on the middle functions, if the middle functions return a function that calls a promise. Only the final function needs the async syntax to work.

```javascript
one() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log('function one ran');
      resolve(true);
    }, 3000);
  });
}
 
function two() {
  return one();
}
 
function three() {
  return two();
}
 
async function promiseAwaiter() {
  await three();
  console.log('now I can run');
}
 
promiseAwaiter();
```
If a function in the chain needs to execute something after a promise, that function will need the async/await syntax added

```javascript
function one() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log('function one ran');
      resolve(true);
    }, 3000);
  });
}
 
async function two() {
  await one();
  console.log('function two ran');
}
 
function three() {
  return two();
}
 
async function promiseAwaiter() {
  await three();
  console.log('now I can run');
}
 
promiseAwaiter();
```
Awaits can be used in a for loop to wait for each promise, although the linter does not like it. I should find a new way to do this.

```javascript
function one() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log('function one ran');
      resolve(true);
    }, 3000);
  });
}
 
function awaitInLoop() {
  return new Promise(async (resolve) => {
    for (const el of [1, 2, 3]) {
      await one();
    }
    console.log('finished waiting');
    resolve();
  });
}
```