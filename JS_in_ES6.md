# Javascript ES6  
#### [let vs const](#let-vs-const)
#### [arrows function](#arrow-function)

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

