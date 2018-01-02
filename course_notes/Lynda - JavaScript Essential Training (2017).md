* [condition logic](#condition-logic)  
* [array methods](#array-method)  
* [function](#function)  
  * [function declaration](#function-declaration)
  * [function expression](#function-expression)  
  * [immediately invoked(IIFE)](#immediately-invoked(IIFE))  
* [let vs const](#let-vs-const)  
* [Object](#object)  
  * [create object](#create-object)  
  * [constructor and prototype](#constructor-and-prototype)  
* [closure](#closure)  
* [DOM](#dom)  
* [DOM events](#dom-events)  
* [loop](#loop)  

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
<hr>

## Object
### create object
```js
// create obj with new keyword
let obj = new Object();

obj.title = "title";
obj.level = 1;
obj.someMethod = function(a, b) {
  return a + b;
}
```
```js
// create obj with bracket
let obj = {
  title: "title",
  level: 1,
  someMethod: function(a, b) {
    return a + b;
  }
}
```

## constructor and prototype
* Javascript use constructor to create class(template for obj instance)  
```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// add methods or properties to existing constructor(class) with prototype
Person.prototype.update = function(name) {
  this.name = name;
}
```

## closure
* a function within a function scope that relies on the variables from outer function scope  

> use with object-oriented programming -- in particular, data hiding and encapsulation.(ES5)
```js
function makeSizer(size) {
  return function() {
    // access size variable from outer scope
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12); // size12 return function
size12(); // invoke function closure
```
<hr>

## DOM
* browser is an obj(window obj)  

* `document`(DOM) is a window obj that access to `html` elements, which are nodes inside document object  

* when document is loaded in a browser, it creates a node tree with hierarchical nested relationship from parent to child node

```js
// document properties
document.body;
document.title;
document.URL;
```
* document methods to get nodes  
```js
// get the first element matching specified selector(s)
document.querySelector(".nav a"); // html element

// get all nodeLists(array-like lists) that match selector(s)
document.querySelectorAll("#navbar a"); // nodeLists
// get all nodeLists with or matching selector(s)
document.querySelectorAll("#navbar a, #nav li"); // nodeLists
```

* access and change element  
```js
// get text html inside the element with innerHTML prop
document.querySelector("h2.title").innerHTML; // return text
// get html inside the element with outerHTML prop
document.querySelector("h2.title").outerHTML; // return html
// set text html inside the element with innerHTML prop
document.querySelector("h2.title").innerHTML = "some text";
// set id of html element
document.querySelector("h2.title").id = "slide";
// get class name 
document.querySelector("h2").className; // return class string
// get class name(s) as DOM list 
// return array-like lists of associated class
document.querySelector("h2").classList; // read only
```

* access and change class
```js
// add class to selector
document.querySelector(".title").classList.add("new-class");
// remove class to selector
document.querySelector(".title").classList.remove("title");
// toggle class to selector, returns boolean
document.querySelector(".title").classList.toggle("slide"); 
// check if selector has specific class, returns boolean
document.querySelector(".title").classList.contains("slide");
```

* access and change attribute
```js
const someElement = document.querySelector(".title a");

// check if attribute exists
someElement.hasAttribute("target"); // returns true/false

// get attribute lists
someElement.attributes; // returns array-like attribute lists

// set attribute
someElement.setAttributes("target", "_blank");
```

* add DOM element  
```js
const someImg = document.querySelector(".featured img");

// 1 create element
let imgFig = document.createElement("figcaption");
// 2 create text node that will go inside the element
let figText = document.createTextNode("some image text");
// 3 add text node to the element
imgFig.appendChild(figText);
// 4 all element to DOM tree
someImg.appendChild(imgFig);
```

```js
// use append(not support for older browser)'
const someImg = document.querySelector(".featured img");

// create element
let imgFig = document.createElement("figcaption");
// append text to element
imgFig.append("some text bla bla bla");
// append created element to existing element
someImg.append(imgFig);
```

* apply inline CSS
```js
document.querySelector("h1").style.color = "green";

document.querySelector("h1").style = {
  color: "green",
  backgroundColor: "red"
}
```
<hr>

> alternatively, the best way is to add class and style class with new CSS

## DOM events
DOM events is the representative of any event which takes place in the DOM or browser  

* common events are `Browser-level events`, `DOM events`, `media events` and `css events`

* To interact with the DOM events use event target method `target.addEventListener(eventType, eventListener[, options])`  

> DOM event such as `onclick()` can handle only one event at a time, use event handler instead.  

> check MDN docs for lists of events that can be used.

### event handlers and callbacks
* when event is trigger, a callback function(eventListener function that registered when event is occured) can be tied to the event

```js
// target.addEventListener(eventType, eventListener[, options])
const someImg = document.querySelector("img");
const someText = document.querySelector("p.text");

someImg.addEventListener("click", (e) => {
  e.preventDefault();
  someText.classList.toggle("highlight");
}, false) // or drop the false since the default is false anyway
```

```js
// alternately create a function and assign as a callback
const someImg = document.querySelector("img");
const someText = document.querySelector("p.text");

const toggle = (e) => {
  e.preventDefault();
  someText.classList.toggle("highlight");
}

someImg.addEventListener("click", toggle, false) // or drop the false since the default is false anyway
```

* pass extra argument in event listener function by wrap it in anonymous function call  

* then pass extra arg in anonymous function(including `e`) and listener(without `e`)  
```js
const someImg = document.querySelector("img");
const someText = document.querySelector("p.text");

const toggle = (e, arg) => {
  e.preventDefault();
  console.log(arg);
  
  someText.classList.toggle("highlight");
}

// wrap it in anonymous function and pass extra arg in anonymous function and listener 
someImg.addEventListener("click", (e, arg) => { toggle(arg) })
```

> The event propagation mode determines the order in which elements receive the event

* With bubbling(true), the event is first captured and handled by the innermost element and then propagated to outer elements.

* With capturing(false), the event is first captured by the outermost element and propagated to the inner elements.

> Use the `addEventListener(type, listener, [useCapture])` to register event handlers for in either `bubbling(default)` or `capturing mode`. To use the capturing model pass the third argument as `boolean`.
<hr>

## loop 
* with `loop`
```js
// loop array
const someImg = document.querySelectorAll('img');

for (let i = 0; i < someImg.length; i++) {
  // do something
}
```

* with `while`
```js
let n = 1;

while (n < 10) {
  n++;
  console.log(n);
}
```

* `break` and `continue`
```js
// continue will skip the rest of excution and run next loop
for (let i = 0; i < 11; i++) {
  if (i === 2) {
    continue;
  }

  console.log(i)
}

// break will skip the rest of loop and exit
for (let i = 0; i < 11; i++) {
  if (i === 2) {
    break;
  }

  console.log(i)
}

console.log('break');
```

