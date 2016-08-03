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
# ES6

## ES6 class example
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
