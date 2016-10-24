---
layout:     post
title:      "Javascript Basic"
subtitle:   "AngularJS study path"
date:       2016-03-29 12:00:00
author:     "Shi"
header-img: "img/post-bg-01.jpg"
---

# Array

```javascript
var things = [
    1,
    '2',
    function(){
        alert('Hello');
    }
]

//Call function in array
things[2]();
```

## Array shift() Method
Remove the first item of an array

## Bracket notation

```javascript
var cat = {
    name: 'Fluffy', 
    color: 'White'
}

display(cat['color']) //Produce same result like: display(cat.color)

//You can also add a property using bracket notation
cat['eye'] = 'Green'
display(cat['eye']) //Print: Green
```

## Property  description

```javascript
var cat = {
    name: 'Fluffy', 
    color: 'White'
}

//Display property description
display(Object.getOwnPropertyDescriptor(cat, 'name'))

//Make a property immutable
Object.defineProperty(cat, 'name', 
  {
  	writable: false
  })
Object.freeze(cat.name)

//Loop every properties in object
for(var propertyName in cat){
	display(propertyName) // Print: name color
	display(cat[propertyName]) // Print: Fluffy White
}

//Set property enumerable
Object.defineProperty(cat, 'name', 
  {
  	enumerable: false // not enumerable: not to be print in iteration
  })
  

//Set property configuarable
Object.defineProperty(cat, 'name', 
  {
  	configuarable: false // not configuarable: can not redefine property
  })

//getter and setter
Object.defineProperty(cat, 'fullName', 
  {
    get: function() {
      return this.name.first + ' ' + this.name.last
    },
    set: function(value) {
      var nameParts = value.split(' ')
      this.name.first = nameParts[0]
      this.name.last = nameParts[1]
    }
  })
  
//Set name
cat.fullName = 'Muffin Top'
//Get name
display(cat.fullName)

//delete property
delete cat.name

//JSONrization
JSON.stringify(cat)

```

## Prototype
Use to inherit from or extend functionality in other objects.

Every function has a prototype

```javascript
var myFunc = function(){}
display(myFunc.prototype) // Output: {}
```    
Object does not hava a prototype but has proto

```javascript
var cat = {name: 'Carlo'}
display(cat.__proto__) // Output: Object {}
	
```

```javascript
Object.defineProperty(Array.prototype, 'lastElement', 
  {
    get: function() {
      return this[this.length - 1]
    }
  })

//Call lastElement method 
var arr = ['red','blue','green'] // Same as: var arr = new Array('red','blue','green')
var last = arr.lastElement

```

### Usage

```javascript
function Cat(name, color) {
    this.name = name
    this.color = color
}
var carlo = new Cat('Carlo','white')

Cat.prototype === carlo.__proto___//Return true. They are pointing to the exact same instance of an object

Cat.prototype.age = 3

display(Cat.prototype) //Output: Cat{ age:3 }
display(carlo.__proto___) //Output: Cat{ age:3 }

display(carlo.hasOwnProperty('age')) // Output: false

carlo.age = 5 
display(carlo.hasOwnProperty('age')) // Output: true. carlo now has his own property

```

### Prototype chains

#### Create prototype chains without using class syntex

```javascript
function Animal(voice){
    this.voice = voice || 'grunt'
}
Animal.prototype.speak = funciton(){
    display(this.voice)
}

function Cat(name){
    Animal.call(this, 'Meow') // Step 1 (to create a prototype chain)
    this.name = name
}

Cat.prototype = Object.create(Animal.prototype) //Step 2
Cat.prototype.constructor = Cat //Step 3

var carlo = new Cat('Carlo')
carlo.speak()
```

#### Create prototype chains using class syntex

```javascript
class Animal {
  constructor(voice) {
    this.voice = voice || 'grunt'
  }
  
  speak() {
    display(this.voice)
  }
}

class Cat extends Animal {
  constructor(name, color) {
    super('Meow')
    this.name = name
    this.color = color
  }
}

var fluffy = new Cat('Fluffy', 'White')
fluffy.speak()

display(fluffy) //Output: {voice:Meow name:Fluffy color:White}

display(Object.keys(fluffy.__proto__.__proto__)) //Using class syntex, Members of classed are not enumerable. So this speak function is not an enumrable property of the animal class
display(fluffy.__proto__.__proto__.hasOwnProperty('speak')) // Output: true

```

## Defining getters and setters

```javascript
var o = {
  a: 7,
  get b() { 
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2
  }
};

console.log(o.a); // 7
console.log(o.b); // 8
o.c = 50;
console.log(o.a); // 25

```
			
# ES6

[ES6 compatibility table](http://kangax.github.io/compat-table/es6/)

## let, var, const

Always use let instead of var.

```javascript
const PI = 3.1415;
PI = 3; // TypeError: Assignment to constant variable.

const foo = Object.freeze({}); //Const for an object
```

## For loop
```javascript
let productId = 42;
for (let productId = 0; productId < 10; productId++)
{

}
```

## For ... of loop
```javascript

var categories = ['hardware', 'software', 'vaporware'];

for (var item of categories) {

}
```

## Template Literals
```javascript
let invoiceNum = '1350';
console.log(`Invoice Number: ${invoiceNum}`);
```

## Destructuring
```javascript
let salary = ['32000', '50000'];
let low, average, high;
[ low, average, high = '88000' ] = salary;
console.log(average); //Output: 50000

let salary = ['32000', '50000', '75000'];
let [ low, ...remaining ] = salary;
console.log(remaining); //Output: ["50000", "75000"]

let salary = {
	low: '32000'
	average: '50000'
	high: '75000'
};
let { low, average, high} = salary;
console.log(high); //Output: 75000

```


## Arrow functions

```javascript
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression // equivalent to:  => { return expression; }

// Parentheses are optional when there's only one parameter:
(singleParam) => { statements }
singleParam => { statements }

// A function with no parameters requires parentheses:
() => { statements }

function(s){ return s.length } 
s => s.length
```

## Rest and Spread Operators
```javascript
var showCategories = function (productId, ...categories) {
	console.log(categories); //Output: ['search', 'advertising']
};
showCategories(123, 'search', 'advertising');
```

## Module

[traceur-compiler](https://github.com/google/traceur-compiler)

```javascript
File base.js:
import { projectId as id, projectName } from 'module1.js';
console.log(`${projectName} has id: ${id}`);

File module1.js:
export let projectId = 99;
export let projectName ='BuildIt';


File base.js:
import someValue from 'module1.js';
console.log(someValue);

File module1.js:
let projectName ='BuildIt';
export let projectId = 99;
export default projectName;

```

## ES6 class 
```javascript
class Cat {
  constructor(name, color) {
    this.name = name
    this.color = color
  }
  
  speak() {
    display('Meeooow')
  }
}

var cat = new Cat('Fluffy', 'White')

display(cat)
cat.speak()
```

### Constructor

```javascript
class Project {
    constructor() {
		console.log('constructing Project');
	}
}

class SoftwareProject extends Project {
	constructor() {
		super();
		console.log('constructing SoftwareProject');
	}
}

let p = new SoftwareProject(); //Output: constructing Project /  constructing SoftwareProject
```

### Static members
```javascript
class Project {
	static getDefaultId() {
		return 99;
	}
}
console.log(Project.getDefaultId());//Output: 99
```

### new.target

#### Point to the original function that called
```javascript
class Project {
	constructor() {
		console.log(new.target.getDefaultId());
	}
}
class SoftwareProject extends Project {
	static getDefaultId() { return 99; }
}
var p = new SoftwareProject();//Output: 99
```

## Symbol

```javascript
const CALCULATE_EVENT_SYMBOL = Symbol('calculate event');
console.log(CALCULATE_EVENT_SYMBOL.toString()); // Output: Symbol(calculate event)
```

```javascript
let s = Symbol('event');
let s2 = Symbol('event');
console.log(s === s2);// Output: false
```

```javascript
let s = Symbol.for('event');
let s2 = Symbol.for('event');
console.log(s === s2);// Output: true
```

```javascript
let article = {
	title: 'Whiteface Mountain',
	[Symbol.for('article')]: 'My Article'
};
let value = article[Symbol.for('article')];
console.log(value);// Output: My Article
```

#### Object Extensions

```javascript
let a = { a: 1 }, b = { a: 5, b: 2 };
let target = {};
Object.assign(target, a, b);
console.log(target);// Output: {a: 5, b: 2}
```

```javascript
// Object.is() replace ===
let amount = NaN;
console.log(Object.is(amount, amount));// Output: true
console.log(amount === amount);// Output: false
```

#### String

```javascript
let title = 'Santa Barbara Surf Riders';
console.log(title.startsWith('Santa'));// Output: true
console.log(title.endsWith('Rider'));// Output: false
console.log(title.includes('ba'));// Output: true

var s = 'Hello world!';
//second param is the init point
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false

let wave = '\u{1f30a}';
console.log(wave.repeat(10)); //Output: 🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊🌊
```

#### Number

```javascript
let sum = 408.2;
console.log(Number.isInteger(sum));// Output: false

let a = Math.pow(2, 53) - 1;
console.log(Number.isSafeInteger(a));//true
a = Math.pow(2, 53);
console.log(Number.isSafeInteger(a));//false

console.log(Math.sign(-20));// -1
console.log(Math.sign(20));// 1

//trunc() the integer part of a number
console.log(Math.trunc(27.1)); //27
```

## Iterator

```javascript
let ids = [9000, 9001, 9002];
let iter = ids[Symbol.iterator]();
iter.next();
iter.next();
console.log(iter.next());// Output: {done: false, value: 9002}

//Example 2
let idMaker = {
	[Symbol.iterator]() {
		let nextId = 8000;
		return {
			next() {
				let value = nextId>8002?undefined:nextId++;
				let done = !value;
				return { value, done };
}};}};
for (let v of idMaker)
console.log(v);// 8000 8001 8002
```

## Generators

### similar to iterator

```javascript
function *process() {
	yield 8000;
	yield 8001;
}
let it = process();
console.log(it.next());// Output: {done: false, value: 8000}

//Example 2
function *process() {
	let nextId = 7000;
		while(true)
			yield(nextId++);
}

//This is a generator
for (let id of process()) {
if (id > 7002) break;
console.log(id);
}

```

## Yielding in Generators

```javascript
function *process() {
	yield 42;
	yield* [1,2,3];
}

let it = process();
console.log(it.next().value);//42
console.log(it.next().value);//1
console.log(it.next().value);//2
console.log(it.next().value);//3
console.log(it.next().value);//undefined 
```

## throw and return

```javascript
function *process() {
	try {
		yield 9000;
		yield 9001;
		yield 9002;
	}
	catch(e) {
	}
}
let it = process();
console.log(it.next().value);//9000
console.log(it.throw('foo'));//{done:true, value:undefined}
console.log(it.next());//{done:true, value:undefined}
```

## Promise 

### For async request

```javascript
function doAsync() {
	let p = new Promise(function (resolve, reject) {
		console.log('in promise code');
		setTimeout(function () {
			console.log('resolving...');
			resolve('someData');
			// or reject('database error!');
		}, 2000);
	});
	return p;
}
let promise = doAsync();// Output: in promise code (2 second delay) resolving...

//function then take two params: success function and reject function
doAsync().then(function (value) {
	console.log('Fulfilled!'+ value);
},
function () {
	console.log('Rejected!');
})
//you can chain another function by
.then(function(value) {
	console.log('Really! ' + value);
});
//when the error occurs, you can call catch
.catch(function (reason) {
	console.log('Error: ' + reason);
});


```

### Multiple promises

```javascript
let p1 = new Promise(...);
let p2 = new Promise(...);
Promise.all([p1, p2]).then(
	function (value) { console.log('Ok') },
	function (reason) { console.log('Nope') }
);
// assume p1 resolves after 1 second,
// assume p2 is rejected after 2 seconds

// Output: (2 second delay) Nope
```

```javascript
//Race returns when one task finishes
Promise.race([p1, p2]).then(
	function (value) { console.log('Ok') },
	function (reason) { console.log('Nope') }
);

// assume p1 is rejected after 3 second,

// assume p2 resolves after 5 seconds
// Output: (3 second delay) Nope

```

## Array

### Array Extension

```javascript
let salaries = Array.of(90000);

let amounts = [800, 810, 820];
let salaries = Array.from(amounts, v => v+100 );
console.log(salaries); //[900,910,920]

//Third param is an object which is visiable in 'this'
let amounts = [800, 810, 820];
let salaries = Array.from(amounts, function (v) {
	return v + this.adjustment;
}, { adjustment: 50 });

console.log(salaries);//[850,860,870]

// -> function do not let you change 'this', this will be always the context you setted when it appares, so you can not change it.
let amounts = [800, 810, 820];
let salaries = Array.from(amounts, v => v + this.adjustment,{ adjustment: 50 });
console.log(salaries);//[NaN, NaN, NaN]

let salaries = [600, 700, 800];
salaries.fill(900);
console.log(salaries);//[900, 900, 900]

let salaries = [600, 700, 800];
salaries.fill(900, 1);//Start to fill arrary from index 1
console.log(salaries); //[600, 900, 900]

let salaries = [600, 700, 800];
salaries.fill(900, 1, 2); //Start to fill arrary from index 1, stop at index 2 (not inclusive)
console.log(salaries);//[600, 900, 800]

let salaries = [600, 700, 800];
salaries.fill(900, -1);//Start counting from the end of array
console.log(salaries);//[600, 700, 900]

let salaries = [600, 700, 800];
let result = salaries.find(value => value >= 750);//Scan array, and for each element will call the function
console.log(result);//800

let salaries = [600, 700, 800];
let result = salaries.find(value => value >= 650); //As soon as find the element, it will stop the scan and return it
console.log(result);//700

let salaries = [600, 700, 800];
salaries.copyWithin(2, 0);// 2 refer to the destination index, 0 is the source index (start reading from)
console.log(salaries);//[600, 700, 600]

let ids = [1, 2, 3, 4, 5];
ids.copyWithin(0, 1);//Start reading from position 1, so read  2, 3, 4, 5, then place it from position 0, got [2, 3, 4, 5, 5] which the last position is not touched
console.log(ids);//[2, 3, 4, 5, 5]

let ids = [1, 2, 3, 4, 5];
ids.copyWithin(3, 0, 2);//only want to copy two values
console.log(ids//[1, 2, 3, 1, 2]

let ids = ['A', 'B', 'C'];
console.log(...ids.entries());//[0,"A"], [1,"B"], [2,"C"]  entries create an array for each element [index, value]

let ids = ['A', 'B', 'C'];
console.log(...ids.keys());//0 1 2

let ids = ['A', 'B', 'C'];
console.log(...ids.values());//A B C
```

### ArrayBuffer and Typed Arrays

#### ArrayBuffer is array of 8 bytes , is useful to hold binaray data like image and video 

#### Typed Arrays, access data in the array buffer

```javascript
let buffer = new ArrayBuffer(1024); //1024 is the length of new byte array
console.log(buffer.byteLength); //1024
```

### Map

```javascript
let employee1={ name: 'Jake' };
let employee2 ={ name: 'Janet' };

let employees= new Map();
employees.set(employee1, 'ABC');
employees.set(employee2, '123');

console.log(employees.get(employee1)); //ABC

employees.delete(employee2);
console.log(employees.size);//1

employees.clear();
console.log(employees.size);//0

let arr = [
	[employee1, 'ABC'],
	[employee2, '123']

];
let employees = new Map(arr);
console.log(employees.size);//2
console.log(employees.has(employee2));//true

let list = [...employees.values()];
console.log(list);//['ABC', '123']

let list= [...employees.entries()];
console.log(list[0][1]); //ABC

//iterate map
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world

```

### Set

```javascript
let perks = new Set();
perks.add('Car');
perks.add('Super Long Vacation');
perks.add('Car');

console.log(perks.size);//2

let perks= new Set([
	'Car',
	'Jet'
]);
console.log(perks.size);//2

let newPerks= new Set(perks); //newPerks is a copy of perks
console.log(newPerks.size);//2
console.log(perks.has('Jet'));//true
console.log(...perks.keys());//Car Jet
console.log(...perks.values());//Car Jet
console.log(...perks.entries());//Car,Car Jet,Jet

//Do not put object in set, they are considered as two different obj
let perks = new Set([
	{ id: 800 },
	{ id: 800 }
]);

console.log(perks.size);//2
```

### Subclassing

```javascript
class Perks extends Array{
	sum(){
		let total =0;
		this.map(v => total += v);
		return total;
	}
let a = Perks.from([5, 10, 15]);

console.log(a.sum());//30

```

## The Reflect API

### Reflect.construct(target, argumentsList[, newTarget])

```javascript
class Restaurant {
	constructor(name, city) {
		console.log(`${name} in ${city}`);
	}
}

let r = Reflect.construct(Restaurant, ["Zoey's", "Goleta"]);//similar to let r= new Restaurant("Zoey's", "Goleta");
console.log(r instanceof Restaurant);//true


```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```

### 

```javascript

```
# Note

## Books

ECMAScript 6 入门: http://es6.ruanyifeng.com/#docs/intro
