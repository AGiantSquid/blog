In Javascript, sometimes you want to use Promise.all to do all the things at once. But what if you are doing an unknown number of things? You might have thousands of parallel calls, that could run out of memory really quick. The answer is to limit the parallel execution.

```js
// import bluebird promise library, it comes with a function to limit parallel executions
const Promise = require('bluebird');

function promiseFunc(arg) {
  return new Promise((resolve, reject) => {
        setTimeout(() => {
          console.log(arg);
          resolve();
        }, 500);
      },
    );
  });
}

async function doIt(bigAssArray) {
  // bluebird Promise.map http://bluebirdjs.com/docs/api/promise.map.html
  await Promise.map(
    bigAssArray,
    element => promiseFunc(element), // the element is from the bigAssArray
    { concurrency: 10 }, // limit the number of promises that can go at once
  );
  console.log('successfully did it');
}
 
doIt(['one', 'two', /* skip a few */ 'ninty-nine', 'one hundred']);
```
