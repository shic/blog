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

traceur-compiler https://github.com/google/traceur-compiler

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

