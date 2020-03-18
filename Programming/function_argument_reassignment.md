In the following code, the function mutator() will add the key 'third' to the dataStruct passed into it.
Calling that function will change the actual reference to the object passed to it.

```javascript
const dataStruct = {
  first: true,
  second: false,
};
 
function mutator(obj) {
  obj.third = false;
}
 
mutator(dataStruct);
 
console.log(dataStruct); // { first: true, second: false, third: false }
```

The following function, however, does not change the reference. It creates a new local reference with the same name as the argument.

```javascript
const dataStruct = {
  first: true,
  second: false,
};
 
function mutaterWithLocalArg(obj) {
  obj = {};
  obj.third = false;
}
 
mutater(dataStruct);
 
console.log(dataStruct); // { first: true, second: false }
```
It seems like the variable that a function uses can be reassigned to something else in the function. As long as it has not been reassigned, it continues to point to the original object that was passed in, and so changes to the function argument will change the object itself. This is probably why the linter does not like reassigning arguments.



This function will change the variable passed to it, as in the first example.

```javascript
const dataStruct = {
  first: true,
  second: false,
};
 
function mutator(obj) {
  obj = obj;
  obj.third = false;
}
 
mutator(dataStruct);
 
console.log(dataStruct); // { first: true, second: false, third: false }
```
If we get silly, we see that we can reassign the input variable to itself, and if we then try to reassign that to an empty struct, it still becomes a new local variable. 

```javascript
const dataStruct = {
  first: true,
  second: false,
};
 
function mutator(obj) {
  obj = obj;
  console.log(obj);  // { first: true, second: false }
  obj = {};
  console.log(obj);  // {}
  obj.third = false;
}
 
mutator(dataStruct);
 
console.log(dataStruct); // { first: true, second: false }
```
The same can be said for arrays.

```javascript
const dataArray = [
  'one', 2, '3',
];
 
function mutator(arrayArg) {
  arrayArg = [];
}
 
mutator(dataArray);
 
console.log(dataArray); //  [ 'one', 2, '3' ]

```
```javascript
const dataArray = [
  'one', 2, '3',
];
function mutator(arrayArg) {
  arrayArg.push(4);
}
 
mutator(dataArray);
 
console.log(dataArray); //  [ 'one', 2, '3', 4 ]
```
Attempting to reference the argument with the arguments object will yield the same results.

```javascript
const dataArray = [
  'one', 2, '3',
];
 
function mutator(arrayArg) {
  arrayArg = [];
  arguments[0].push(10);
  console.log(arrayArg); // [ 10 ]
}
 
mutator(dataArray);
 
console.log(dataArray); // [ 'one', 2, '3' ]
```
The same behavior exists in other languages, like Python

```python
data_struct = {
  "first": True,
  "second": False,
};
 
def mutator(obj):
    print(obj) # {'second': False, 'first': True}
    obj = {}
    obj["third"] = False
    print(obj) # {'third': False}
 
mutator(data_struct)
 
print(data_struct) # {'second': False, 'first': True}
```

