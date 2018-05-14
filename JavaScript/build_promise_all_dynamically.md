Let's say we have an asynchronous function we want to run, that calls a database.
```javascript
function updateUser(user) {
  return new Promise((resolve, reject) => {
    // do some db stuff
  });
});
```

Now let's say we want to apply this function to a bunch of users.
```javascript
const users = await getUsers();
```

We want to do some action, callWhenDone(), after all the users have been updated. We cannot do the following.
```javascript
users.forEach((user) => {
  updateUser(user);
});
 
callWhenDone();
```
The function `callWhenDone()` will be called before all the users have been looped over.



We solve this with await, Promise.all(), and map().
```javascript
const results = await Promise.all(users.map(user => updateUser(user)));
callWhenDone();
```
The `updateUser()` function will get mapped to all the results of getUsers(), and will be executed as fast as node can execute them.

This will run all the updates, and continue with the function callWhenDone(), after the updates have completed.
