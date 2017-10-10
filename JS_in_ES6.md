# Javascript ES6  
#### [let vs const](#let-vs-const)
#### [arrows function](#arrow-function)
#### [default function argument](#default-function-argument)
#### [Template literals](#template-literals)
#### [strings](#strings)
#### [Destructuring Objects](#destructuring-objects)
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