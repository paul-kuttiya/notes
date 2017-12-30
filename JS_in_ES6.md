# Javascript ES6  
* [let vs const](#let-vs-const)
* [arrows function](#arrow-function)
* [default function argument](#default-function-argument)
* [Template literals](#template-literals)
* [strings](#strings)
* [Destructuring Objects](#destructuring-objects)
* [Using for of loop with array](#using-for-of-loop-with-array)
* [Using for in loop with object](#using-for-in-loop-with-object)
* [Array methods](#array-methods)
* [Array spread](#array-spread)
* [Array rest param](#array-rest-param)
* [Object literal](#object-literal)
* [Modules](#modules)
* [Prototypal Inheritance](#prototypal-inheritance)
------

### let vs const  
* `const` value can't be overwritten  

* `let` value can be written  

* ES5 uses IIFE to declare private scope for variables, while ES6 `let` and `const` are block scope  
```js
const name = "JS"; //name is window scope
console.log(name); // "JS"
```
```js
{
  const name = "JS"; //name is block scope
}
console.log(name); // ""
```

* `const` and `let` are not hoisting  
```js
console.log(name); //undefined
var name = 'a';
```

```js
console.log(name); // Uncaught ReferenceError
const name = 'a';
```

> use `const` when defined variable, `let` when varaible value will be updated, `var` shouldn't be used for ES6  

### Arrow function  
* Arrow function is an anonymous function(function without a name).  
If need name, use arrow function expression instead.  

* Arrow represent function block  
```js
const names = ['a', 'b', 'c'];

//ES5
const newNames = names.map(function(name) {
  return 'new' + name;
});

//ES6
const newNames = names.map((name) => {
  return 'new' + name;
});
```

* If have only one params can defined argument without parenthesis  
```js
//ES6
const newNames = names.map(name => {
  return 'new' + name;
});
```

* implicit return  
```js
const newNames = names.map(name => 'new' + name );
```

* need anonymous function; parenthesis, if no arg specified  
```js
const newNames = names.map(() => 'new' + name );
```

* If return an object in one-liner, needs to wrap with parenthesis  
```js
const newNames = names.map((name, i) => { name: name, index: i });
```

* ES6 can drop `key: value` to single name, if `key: value` has the same name  
```js
// same as { name: name }
const newNames = names.map((name, i) => { name, index: i + 1 });
```

> use `console.table(arg)` for chrome dev to display table array  

* use ES6 to inherit the context(`this`) from the parent scope
```js
//window
const box = document.querySelector('.box');

box.addEventListener('click', () => {
  console.log(this); //window
});
```

```js
//window
const box = document.querySelector('.box');

//use ES5 to get the object context
box.addEventListener('click', function() {
  console.log(this); // box object
});
```

```js
//window
const box = document.querySelector('.box');

//use ES5 to get the object context
box.addEventListener('click', function() {
  console.log(this); // box object

  //will bound to window
  setTimeout(function() {
    console.log(this); //window
  }, 1000);
});
```

```js
//window
const box = document.querySelector('.box');

//use ES5 to get the object context
box.addEventListener('click', function() {
  console.log(this); // box object

  //use ES6 to inherit the context as same as parent scope
  setTimeout(() => {
    console.log(this); // box object
  }, 1000);
});
```

* not working with `arguments` class `Array` keyword object  

### Default function argument  
* ES6 accepts default function argument; will use that argument if not defined when function is executed    
```js
function total(a, b=2, c=3) {
  return a + b + c
}

total(6) //1
total(1, 10, 20) //31
total(1, undefined, 20) // 21
```

### Template literals  
* use backtick to interpolate strings  
* inside the `${..}` block can also run with JS code, including function   
```js
const name = 'name';
`my name is ${name}`;
`my age is ${10 * 3}`;
```

* with ES6 multiline properties, can also use to create html template  
```js
const json = {
  name: "John",
  age: "22",
  city: "New York"
};

const template = `
  <div>
    <h1>Hi my name is ${json.name}</h1>
    <p>I am ${json.age}</p>
    <p>I'm from ${json.city}</p>
  </div>
`
```

* Template literals with array and iternary opeartor  
```js
const json = [
  { name: "john", age: 22 },
  { name: "sarah" }
];

const template = `
  <ul>
    ${json.map(person => {
      `<li>
        ${person.name}
        ${person.age ? `${person.age} years old` : ""}
      </li>`
    }).join('')}
  </ul>
`
```

### strings  
* new methods in es6  
```js
const name = "abcde123456";

//check the begining of the string, start with index "i"
name.startsWith("a") // true
name.startsWith("a", 5) //false

//check the end of the string, until index "i"
name.endsWith("6") // true
name.endsWith("e", 4) //true

//check the string contains the argument
name.includes("6") // true
name.includes("z") // false

//repeat the strings
"a".repeat(6) // aaaaaa
```

### Destructuring Objects  
* extracts prop from object to new variable  
```js
const person = {
  name: "john",
  age: "22"
}

//extract value then save as variable name as "key"  
//const name = "john";
//const age = 22;
const { name, age } = person;

const person = {
  name: {
    first: "john",
    last: "doe",
  },
  age: "22"
}

//extract "john" save to const first;
//extract "doe" save to const last;
const { first, last } = person.name;

//extract and save as other named constance;
const { first: firstName, last: lastName } = person.name;

//extract and set default value fallback for undefied value;
const { first, last, city="NY" } = person.name;
```

* extracts item from Array object to new variable  
```js
const arr = ["a", "b", "c"];

//const a = "a", b = "b", c = "c";
const [a, b, c] = arr

//use rest operator to assign the rest of arg to array.
// a = "a", subArr = ["b", "c"]
const [a, ...subArr] = arr
```

* swapping variable with ES6  
```js
let a = "a";
let b = "b";

//swap two variables
[a, b] = [b, a];
```

* extracts returned object from the function to variable  
```js
function getName() {
  const names = {
    eng: "joseph",
    esp: "jose",
    fre: "fose"
  }

  return names;
}

// const eng = "jose"
const { esp } = getName();
```

* passing in Destructuring Objects as argument into function  
```js
//set keys for a, b default 
//set default arg to empty obj
function total({ a = 1, b = 2, c = 0 } = {}) {
  return a + b + c;
}

total({ a: 2, b: 5 }) // 7
total({ b: 5, a: 2 }) // 7

//default obj set to {}, will look for default value
total() //3
```

### Using for of loop with array
* ES6 `for...of` loop  
```js
const names = ["a", "b", "c"];

for (const name of names) {
  console.log(name);
  if (name === "a") {
    continue;
  }
}
```

#### Using for in loop with object  
* `for...in` support both ES5 and ES6  
* create const as key and iterate object  
```js
const person = {
  name: "john",
  age: 22
};

for (const info in person) {
  const value = person[info];
  console.log(info, value)
} 
```

### Array methods  
* `Array.from(arrayLike)` apply array-like object to true array; mostly use when need array prototype properties  
```js
const lists = document.querySelectorAll('li'); //nodeLists of li
const listsArray = Array.from(lists); //listsArray becomes Array and has all Array prototype

//Array.from takes a function as second arg which can use to specify the return value of array obj  
const innerTexts = Array.from(lists, ele => {
  console.log(ele); //ele is the DOM; eg <li>text<li>
  return ele.textContent; //returns each DOM innerText in array 
});
```

* `Array.of(arg)` creates array from the passed in argument  
```js
const newArray = Array.of(1,2,3,4,5); //[1,2,3,4,5];
```

* `Array.find(function)` iterates each element and return the first matched element if function returns true  

* `Array.findIndex(function)` iterates each element and return the first matched element index if function returns true    
```js
const json = [
  {
    name: "john",
    age: 22
  },
  {
    name: "sam",
    age: 28
  }
];

//{name: "sam", age: 28}
json.find(element => {
  return element.name === "sam"
});

//one liner
json.find(element => element.name === "sam");

//1
json.findIndex(element => element.name === "sam");
```

>> `Array.find` returns the first element, `Array.filter` returns array  

### Array spread

* combine multiple arrays and value into single array  
* split strings into array of individual string  
* pass in as argument for each element  
```js
const a1 = ["a", "b", "c"];
const a2 = ["d", "e"];

const bigArray = [...a1, "add", ...a2]; // ["a", "b", "c", "add", "d", "e"];
const AnotherArray = [..."add"]; // ["a", "d", "d"]

//create a copy array rather than mutate from the original array by reference
var copyArr = [].concat(bigArray); //ES5
let copyArr = [...bigArray]; //ES6

//create new array with slice
const newArr = [...a1.slice(0, 1), ...a1.slice(2)]; //["a", "c"]

//pass in as argument
a1.push(...a2); // ["a", "b", "c", "d", "e"];

someThing(...a2); // someThing("d", "e")

function someThing(a, b) {
  console.log(a, b);
}
```

### Array rest param  
* convert the rest of arguments to array in function  
* destructuring into new variable and the rest into array    
```js
//convert rest of args to array  
getLetters("a", "b", "c", "d", "e"); //"a" "b" ["c", "d", "e"]

function getLetters(a, b, ...letters) {
  console.log(a, b, letters);
}

//destructuring array into new variable  
const arr = ["a", "b", "c", "d"];

const [a, b, ...letters] = arr ; //const a = "a", const b = "b", const letters = ["c", "d"]
```

### Object literal  
* drop `key:value` when create object to single variable if `key:value` has the same name  
* drop function syntax when create object function properties  
```js
//create object  
const first = "John",
      last = "Doe";

const person = { first, last } // person = { first: first, last: last }

//new ES6 syntax for object function properties
const cat = {
  //ES5 sleep: function() { ... }
  sleep() {
    //...
  },
  bite(param) {
    //...
  }
}

//create key value using string as key name  
const key = "abc";

const newObj = {
  [key]: "22", // abc: "22"
  //dynamicly create new key inside obj
  [`${key}de`]: "33" // abcde: "33"
}
```

### Modules  
* import and export js as module  
* export default will export and can be renamed in other module; can export default only 1 per file module  
```js
// file1.js
const someCode = {
  //...
};

export default someCode;
```
```js
// file2.js
// import from export default can be renamed directly 
import newConst from './file1'; // const newConst is someCode obj

// file3.js
// import dependencies don't need path
import React from 'react';
```

* export named variables and function will strictly export as named only; can be multiple per module    
```js
// file1.js
export const someCode = {
  //...
};

export const anotherCode = {
  //...
};

export default function User() {
  //...
}

export function functionExport() {
  //...
}
```
```js
// file2.js
// import User from export default in file1.js
// import someCode, anotherCode, functionExport from file1.js
import User, { someCode, anotherCode, functionExport } from './file1';

// file3.js
// import and rename need as to rename to new variable
import { someCode as newCode } from './file1';
``` 

### Prototypal Inheritance  
* ES5 prototype  
```js
// create constructor function to create instance properties
// object created from function constructor will have its own property 
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// add function methods to constructor function using prototype
// all object created from the same function constructor will inherit all methods from function constructors prototype
Person.prototype.talk = function() {
  //...
}

//this.name === "John";
//this.age === 22;
//John.talk === Person.prototype.talk;
const John = new Person("John", 22);
```

* ES6 class and inheritance  
```js
//define class decoration  
class Person {
  //initializer
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  //instance method
  talk() {
    //...
  }
  //class method
  static walk() {
    //...
  }
  //getter
  get profile() {
    return `${this.name} ${this.age}`;
  }
  //setter
  set city(city) {
    this.city = city;
  }
}

//class inheritance  
class Male extends Person {
  constructor(name, age, height) {
    //call super from parent class to get context('this' point to Person), pass in argument needed for parent class
    super(name, age)
    this.height = height
  }
}

//people have its own instance properties name and age, and have Person function methods
const people = new Person("John", 22);

//johny will inherit all Person properties, and have its own instance properties name, age and height
const johny = new Male("Johny", 22, 6.1);
```

```js
// Example create new class by extending Array class
// Array(element1, element2, ...)
class CollectionArr extends Array {
  //use rest operator to get the rest of arg
  constructor(string, ...items) {
    //class Array needs elements as arguments
    super(...items);
    this.string = string;
  }
  someMethod() {
    //...
  }
}

// costomArr = [{..}, {..}], this.string = "string"; 
const customArr = new CollectionArr("string", { name: "john", age: 22 }, { name: "sam", age: 26 })
```