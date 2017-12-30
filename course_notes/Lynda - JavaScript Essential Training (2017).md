* [condition logic](#condition-logic)  
* [array methods](#array-method)  
* [function](#function)  
  * [function declaration](#function-declaration)
  * [function expression](#function-expression)  
  * [immediately invoked(IIFE)](#immediately-invoked(IIFE))  
* [let vs const](#let-vs-const)  
* [Object](#object)  
  * create object  
  * constructor  
  * prototype

## condition logic
```js
// test for truthy
const obj = "something";

if (obj) {
  // ...
}
```

```js
// test for falsey
const obj = "something";

if (!obj) {
  // ...
}
```
<hr>

## array method
```js
const pens = ["red", "blue", "green", "orange"];

// PROPERTIES:
// Get a property of an object by name:
console.log("Array length: ", pens.length);

// Reverse the array:
pens.reverse();

// Remove the first value of the array:
pens.shift();

// Add value(s) to the front of the array:
pens.unshift("purple", "black");

// Remove the last value of the array:
pens.pop();

// Add value(s) to the end of the array:
pens.push("pink", "prussian blue");

// Find the specified position(idx) and remove n number of items from the array.  
// pens.splice(idx, n):
pens.splice(1, 2) // Starts at idx 1 and removes two items.

// Create a copy of an array including from position(idx) to end(not include). Typically assigned to a new variable:
var newPens = pens.slice();
var partialPens = pens.slice(1, 3); // ["blue", "green"]

// Return the first element that matches the search parameter after the specified index position. Defaults to index is 0. 
// pens.indexOf(search, index):
var result = pens.indexOf("blue", 0);

// Join array with separator
// pens.join(separator):
var arrayString = pens.join(separator);
```
<hr>

## function  
### function declaration
* defines a function statement  

* hoisted
```js
anoFunc(2, 4); // 6

function anoFunc(a, b) {
  return a + b;
}
```

### function expression
* not hoisted

* need to invoke after declaration only
```js
// anoFunc(2, 4); TypeError if execute before declaration

// anonymous function
var anoFunc = function(a, b) {
  return a + b;
}

anoFunc(2, 4);
```

### immediately invoked(IIFE)
* function that runs as soon as it is defined.

* prevent scope pollution  
```js
(function () { 
    // Variable name is not accessible from the outside scope
    var aName = "Barry";
}());

aName // throws "Uncaught ReferenceError: aName is not defined"
```

```js
// Immediately creates the output and store in variable
var result = (function (a, b) { 
    return a + b;
}(1, 2)); // undefined

result; // 3
```
<hr>

## let vs const
* `const` is immutable  
```js
const a = 2;
a = 2; // 'a' has already been declared
```

* `let` is mutable and is a `BLOCK` scope  

* can be re-assigned within the same scope  
```js
function letTest() {
  let x = 1;

  if (true) {
    let x = 2;  // different variable
    console.log(x);  // 2

    x = "what's up";
    console.log(x) // what's up
  }

  console.log(x);  // 1
}

letTest();
```