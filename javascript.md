# Javascript Fundamentals Review

## Primative Data Types

Javascript has several basic data types:

```javascript
'this is a string' // string (text)
123 // number (int)
1.2 // number (float)
true // boolean
false // boolean
```

They can be combined in the usual ways

```javascript
2+2
3.2*4
5/2
9.6-2
'first string ' + 'second string.';
```

## Variables

Declaring variables is done with the keyword `var`.  Variables are dynamically typed (decided during execution) since there is no compilation process.

```javascript
var foo = 'string';
var bar = 1;
```

Reassignment is done by omitting the var keyword.  Variables are loosely typed (can be reassigned to any other value, regardless of their initial value)

```javascript
var foo = 'a string';
foo = 123.4;
```

## Functions and Scope

Declare functions with keyword `function`.  Do not need to specify return type.

```javascript
function myFunc(){
	return 5;
}
```

To execute a function, invoke its name with parentheses

```javascript
myFunc();
```

Can pass parameters into functions

```javascript
function addFive(numberToAddFiveTo){
	return numberToAddFiveTo + 5;
}
addFive(6); // returns 11
```

Variables declared inside a function cannot be accessed outside of it

```javascript
function foo(){
	var myVar = 1;
	return myVar;
}
console.log(myVar); // error
```

but variables declared outside a function are accessible within it

```javascript
var myVar = 1;
function foo(){
	return myVar;
}
console.log(foo());
```

## Objects

Objects in javascript are just key/value pairs

```javascript
var myObj = {
	property1: 'value1',
	property2: 'value2'
}
```

Can retrieve values using dot notation

```javascript
myObj.property1
```

Can modify an object's properties like so:

```javascript
myObj.property1 = 'new value';
myObj.newProperty = 'asdf';
```

## Arrays

Can create arrays, which are lists of elements of whatever type

```javascript
var numbers = [1,'string',3.234,true];
```

Can access an array element by index (which start at 0)

```javascript
numbers[0]; //first element in array
```

Can alter values at a preexisting index.  Type does not matter

```javascript
numbers[1] = 123;
```

Arrays are objects, so they have properties

```javascript
numbers.length //gives you the length of the array
numbers.pop() //remove the last element and returns it
numbers.push(26) //adds a number to the last position of the array
numbers.shift() //remove the first element and returns it
numbers.unshift(56) //adds a number to the first position of the array and pushes everything down
```

## Equality

Can test for equality with `==`

```javascript
1 == 2 //false
1 == 1 //true
'asdf' == 'asdf' //true
'asdf' == 'asdfasdf' //false
```

These are not exact and will attempt type conversion

```javascript
'1' == 1 //true?!?!
```

To make it exact, use `===`

```javascript
`1` === 1 //false
```

## Control Flow (loops, if/else)

We can use equality in if/else statements

```javascript
if(1 === 2){
	console.log('should not run');
} else if (1 === 3){
	console.log('also should not run');
} else {
	console.log('runs if all else fails');
}
```

## Loops

We can repeat a block of code over and over again while a certain statement is true

```javascript
var i = 1;
while(i < 5){
	console.log(i);
	i++;
}
```

We can use `for` loops as a shorthand for the above

```javascript
for(var i = 1; i < 5; i++){
	console.log(i);
}
```

## Functions are objects

Functions can be assigned to variables

```javascript
var myFunc = function(){

}

myFunc();
```

Can be assigned to properties of objects.  These functions are referred to as methods of the object

```javascript
var myObj = {
	functionProperty: function(){

	}
}

myObj.functionProperty();
```

When invoking methods, you can reference other properties of the object with the keyword `this`

```javascript
var myObj = {
	color: 'blue',
	functionProperty: function(){
		console.log(this.color);
	}
}

myObj.functionProperty(); //logs 'blue'
```

Can be passed as parameters to other functions

```javascript
function invokingFunction(callbackFunctionParam){ //referenced without ()
	console.log('event handler');
	callbackFunctionParam(); //invoked by adding ()
}

var callbackFunction = function(){
	console.log('inside callback function');
}

invokingFunction(callbackFunction); //passed as an object by omitting ()
```

This can be done **anonymously**

```javascript
function invokingFunction(callbackParam){
	console.log('event handler');
	callbackParam();
}

invokingFunction(function(){
	console.log('inside callback function');
});
```

Remember that functions can access variables defined outside their scope.  When dealing with functions executed after they declaration, make sure you examine what the values of the variables are


```javascript
function invokingFunction(callbackParam){
	callbackParam();
}

var foo = 1;

var callbackFunction = function(){
	console.log(foo);       
}

foo = 2;

invokingFunction(callbackFunction); //logs 2
```

## Asynchronicity, Events, and Callbacks

Javascript is **event driven**, meaning that we define event handling functions that just sit around for something to happen and then execute a callback function

```Javascript
//setTimeout is the event handling function here.  It is built into Node.  The event it handles is the passing of two seconds.  Once this event occurs, it executes its callback function
setTimeout(function(){
	console.log('callback function executed!');
}, 2000);
```

Node is aware of all event handler functions that are still waiting to execute their callback functions.  It will not return control to the user until either all event handlers have finished waiting or the user forces the process to stop.

It is **VERY** important to be aware that variables outside a callback function's scope can change value even after it has been registered, but before it is called

```javascript
var foo = 1;

setTimeout(function(){
	console.log(foo); // log 2, even though foo is 1 at time of registration
}, 500);

foo = 2;
```

## Object Oriented JS

If you need to create multiple objects of the same type, object literals (`{ property:'value'}`) can be inefficient.  We can create constructor functions, which act like class declarations.

```javascript
var Person = function(){
	this.numArms = 2; //use the this keyword to create properties and methods
	this.numLegs = 2;
}

var me = new Person(); //use the new keyword to instantiate a new object
var someoneElse = new Person();
console.log(me);
console.log(someoneElse);
```

We can pass parameters into constructor functions to make instances unique

```javascript
var Person = function(name){
	this.name = name;
	this.numArms = 2; //use the this keyword to create properties and methods
	this.numLegs = 2;
}

var me = new Person('Matt'); //use the new keyword to instantiate a new object
var someoneElse = new Person('Joey Jo-Jo Junior Shabadoo');
console.log(me);
console.log(someoneElse);
```

Methods act just like adding properties

```javascript
var Person = function(name){
	this.name = name;
	this.numArms = 2; //use the this keyword to create properties and methods
	this.numLegs = 2;
	this.sayHello = function(){
		console.log("Hello, my name is " + this.name);
	}
}

var me = new Person('Matt'); //use the new keyword to instantiate a new object
me.sayHello();
```

Since functions are objects, we can create static properties/methods (properties and methods that relate to the class, not the instances of the class) by using dot notation

```javascript
var Person = function(){
	/*
	usual stuff here...
	*/
}

Person.genders = ['male', 'female'];
console.log(Person.genders);
```

We can have a "class" inherit from another class, using the `.call` static method of a function

```javascript
var Car = function(){
	this.wheels = 4;
}

var Humvee = function(){
	Car.call(this);
	this.numAmericanFlags = 4;
}

var murica = new Humvee();
console.log(murica);
```
