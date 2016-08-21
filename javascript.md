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
## Control Flow (loops, if/else)
## Functions are objects
## Events
## Callbacks
## Asynchronicity
## Constructor Functions
