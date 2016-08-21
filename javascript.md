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

## Objects/Arrays
## Equality
## Control Flow (loops, if/else)
## Functions are objects
## Events
## Callbacks
## Asynchronicity
## Constructor Functions
