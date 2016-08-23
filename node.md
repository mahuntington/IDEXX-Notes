# Node.js

## NPM

Whenever creating a new node project, use to set it up

```
npm init
```

[NPM](https://www.npmjs.com/) is a package manager for node.js and js libraries and frameworks.  You can look up packages there, and install them for your project with:

```
npm install package-name --save
```

## module.exports/require

Traditionally, importing JS files into other JS files has not been supported... until now!  There are several ways to do this, but node allows you to add things the to module.exports object.

```javascript
module.exports = 'foo';
```

Whatever is on there, will be the return value of

```javascript
require('yourJSFile.js');
```

You can assign this to a variable to use later

## Instantation

First install express with `npm install express --save` and require it

```javascript
var express = require('express'); //include express package
```

`express` has lots of abilities, but we just want to start up a server app:

```javascript
var app = express(); // create an express app
```

Then make it listen on a port

```javascript
app.listen(3000, function(){ //start the server
	console.log('listening on port ' + PORT);
});
```

## CRUD and HTTP Verbs

In comp sci, there are different kinds of action you can take on data

- create
- read
- update
- destroy

There are different kinds of 'methods' you can use to make a request to a server that map to these actions:

- post (create)
- get (read)
- put/patch (update)
- delete (delete)

PUT is for updating an entire model, PATCH is for changing just a few attributes

## Routing

Basic routing can be done at the app level

```javascript
app.get('/', function(req, res){ // route for /
	res.send('hi'); //respond with 'hi'
});
```

This sets up an event listener for any GET request that comes into the server with the path of `/`.  Give it a callback function which takes a request variable and a respond variable.  Each of these have different methods/properties which we'll learn about

## Middleware

We can define a callback function that is called or all requests and then continues on to other request handlers

```javascript
app.use(function(req, res, next){
	console.log('middleware');
	next();
})
```

`next();` tells express to continue processing the request.  `app.get(),app.post()`, etc have this ability too, but it's rarely used.

Just like with `app.get(),app.post()`, etc we can add the ability to handle just those requests that match a url pattern

```javascript
app.use('/foo', function(req, res, next){
	console.log('middleware');
	next();
})
```

## MVC

One of the main goals of express is to cleanly separate data from the view layer.  To do this, it follows the Model View Controller pattern, which creates a middleman (Controller) which passes data (Models) off to the presentation/html (View) layer

In addition, putting all your routes inside server.js can become difficult to maintain with a lot of variables.  We can group similar urls together into separate "controller" files.

```javascript
var runsController = require('./controllers/runs.js'); //require our own runsController
app.use('/runs/', runsController); //use it for anything starting with /runs
```

Now, create a controllers directory, create an appropriately named file, and use:

```javascript
var controller = require('express').Router(); //require express and create a router (controller)
controller.get('/', function(req, res){ //route for finding all routes by a the session user
	res.send('runs index');
});
module.exports = controller;
```

## Views

Let's separate the views from the controller.  Install express with `npm install ejs --save`

Create a directory called 'views' and create an appropriately named file with the extension .ejs.  Now we can reference it.  Express will assume the file path starts with the 'views' directory you created.

```javascript
var controller = require('express').Router(); //require express and create a router (controller)
controller.get('/', function(req, res){ //route for finding all routes by a the session user
	res.render('viewFile.ejs');
});
module.exports = controller;
```

EJS files are just html, but you can use javascript to dynamically create HTML:

```html
<ul>
	<% for(var i = 0; i < 4; i++) { %>
		<li>
			<%= i %><!-- add = to write a value to the html.  Omit the = and it will just run the JS, but not show anything visually -->
		</li>
	<% } %>
</ul>
```

You can pass data into the view file by adding a second parameter that's an object.  The properties of the object will become the variable name that's accessible in the view file.

```javascript
var controller = require('express').Router(); //require express and create a router (controller)
controller.get('/', function(req, res){ //route for finding all routes by a the session user
	res.render('viewFile.ejs', {
		variable1Name: 'variable 1 value'
	});
});
module.exports = controller;
```

Now inside the .ejs file, we can access `variable1Name` like so:

```html
Value: <%= variable1Name; %>
```

## URL Params/Query Strings

Data can be passed to the server through query strings (a.ka. GET parameters) which look like ?param1=value1&param2=value2

They can be accessed like so:

```javascript
app.get('/', function(req, res){
	var param1 = req.query.param1;
	var param2 = req.query.param2;
});
```

Your route can also have parameters in the path section

```javascript
app.get('/:id', function(req, res){
	var id = req.params.id;
});
```

## Body Parser
## REST
## Method Override
## Database
## Static
