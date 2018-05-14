```javascript
const array = ['mac', 'pc', 'linux'];
for (const a in array) {
  console.log(a); // array index
  console.log(array[a]); // each element
}
 
for (const a of array) { // array value
  console.log(a);
}
 
array.forEach((item, index) => {
  console.log(item); // logs each element in array
  console.log(index);
});
 
const obj = { banana: 'yellow', cherry: 'red' };
for (const k in obj) { // object keys
  console.log('key:', k);
  console.log('value:', obj[k]);
}
 
for (const k of Object.keys(obj)) {
  console.log('key:', k);
  console.log('value:', obj[k]);
}
 
Object.keys(obj).forEach((k) => {
  console.log('key:', k);
  console.log('value:', obj[k]);
});
 
Object.entries(obj).forEach(([k, v]) => {
  console.log('key:', k);
  console.log('value:', v);
});
 
function argsIteratorForOfLoop(...args) { // ...args makes arguments an array
  for (const arg of args) {
    console.log(arg);
  }
}
 
function argsIteratorForInLoop(...args) { // ...args makes arguments an array
  for (const arg in args) {
    console.log(args[arg]);
  }
}
 
function argsIteratorForEach(...args) {
  args.forEach((arg) => {
    console.log(arg);
  });
}
 
argsIteratorForOfLoop('dogs', 'monkeys', 'kittens');
argsIteratorForInLoop('dogs', 'monkeys', 'kittens');
argsIteratorForEach('dogs', 'monkeys', 'kittens');
```
