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

First require express:

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

## Routing
## MVC
## Views
## Params/Query Strings
## CRUD and HTTP Verbs
## REST
## Middleware
## Body Parser
## Method Override
## Database
## Static
