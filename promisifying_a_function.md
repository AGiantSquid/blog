Let's say we have a js function that uses a callback

```javascript
let a = 0;
function IAintNoCallerBackGirl(cb) {
    setTimeout(function() {
        console.log('This wait ');
        a += 1;
        cb(a);
    }, 4000);
}
```
Now, we want to turn this into a promise.

First include promisify. Then, wrap the call back function like so.
```javascript
const { promisify } = require('util');
 
async function thisWait() {
    const IAintNoCallerBack = await promisify(IAintNoCallerBackGirl)();
    console.log('is bananas');
}
 
thisWait();
```
If you try and run this, you will get an error about 'UnhandledPromiseRejectionWarning: Unhandled promise rejection.' That is because you were naughty and didn't return null for your error to your callback, as you always should. Let's update that.

```javascript
let a = 0;
function IAintNoCallerBackGirl(cb) {
    setTimeout(function() {
        console.log('I ain\'t no caller back.');
        a += 1;
        cb(null, a); // much better
    }, 4000);
}
```

That's all you need. Go forth and conquer.
