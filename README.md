# D3.js

## Basics

- Selection
	- `d3.select()`
		- like document.querySelector()
	- `d3.selectAll()`
		- like document.querySelectorAll()
	- can make selections from within selections
		-`d3.select('main').selectAll('span');`
- .style()
	- sets the style for an element
		- `d3.select('div').style('color', 'orange');`
	- can pass an object
		- `d3.select('div').style({'color': 'blue', 'font-size': '40px'});`
- style will return the selection for chaining
	- `d3.select('div').style('color', 'orange').style({'color': 'blue', 'font-size': '40px'});`
- .attr()
	- adds/changes an attribute on an selection
	- `d3.select('div').attr('anExampleAttribute', 'someValue');`
- .classed()
	- checks to see if all elements in selection contain the chosen class
	- `d3.selectAll('.house').classed('house');`
		- returns true
	- `d3.selectAll('div').classed('house');`
		- returns false if not all divs contain class `house`
	- chaining doesn't work since it returns true or false
	- can add the class using
		- `d3.selectAll('div').classed('frog', true);`
		- returns the selection, so you can chain
	- can remove the class using
		- `d3.selectAll('div').classed('frog', false);`
- .append()
	- append html to a selection
	- returns the appended element
	- `d3.selectAll('div').append('span')`
- .html()
	- change the inner html of an element
- .text()
	- set the content of the selection to the exact text (no html)

## SVG
- SVG tag is inline
- Positioning
	- (0,0) - x = 0, y = 0
	- starts at top left
	- y increases vertically down
	- can use negative values
		- -x goes left
		- -y goes up
- Styling
	- attributes
		- `fill` fill color
		- `stroke` stroke color
		- `stroke-width` width of stroke
	- can also be set inside the `stroke` attribute
- Group
	- `<g></g>`
	- can put multiple elements inside it.
	- positioning and styling apply to children
- Circle
	- attributes
		- `r` radius
		- `cx` x position
		- `cy` y position

	```xml
	<svg height="800" width="500">
		<circle/>
		<circle r="50"/>
		<circle r="50" cx="200" cy="300"/>
	</svg>
	```

- Line
	- attributes
		- `x1` starting x position
		- `y1` starting y position
		- `x2` ending x position
		- `y2` ending y position

	```xml
	<svg height="800" width="500">
		<line/>
		<line x1="0" y1="0" x2="100" y2="100"/> <!-- no stroke, so invisible -->
		<line x1="0" y1="0" x2="100" y2="100" stroke="purple"/>
		<line x1="10" y1="0" x2="10" y2="100" stroke="red"/>
		<line x1="30" y1="10" x2="130" y2="10" stroke="blue"/>
	</svg>
	```

- Text
	- Content of tag is the text
- Transform
	- `transform = "translate(x,y)"`
	- `transform = "scale(factor)"`
	- `rotate = "rotate(degrees)"`

## Request

- AJAX functions
	- `d3.json('path', function(error, data){});`
	- `d3.csv('path', function(error, data){});`
	- `d3.text('path', function(error, data){});`
	- `d3.html('path', function(error, data){});`
	- `d3.tsv('path', function(error, data){});`
	- `d3.xml('path', function(error, data){});`

## Data binding

- make a "ghost call" to all circles, even if there are none already
	- `d3.selectAll('circle').data(dataArray).enter().append('circle');`
	- `.data(dataArray)` joins each element in dataArray to an element in the selection
	- `.enter()` returns the sub section of dataArray that has not been matched with DOM elements
	- `.append()` - creates a DOM element for each of the remaining dataArray elements
	- once data has been bound to elements, you can call something like `selection.attr('r', function(d,i){ })` or `selection.style('fill', function(d,i){ })`
		- callback will be executed for each DOM element
		- `d` is data for the current element
		- `i` is the index of that element in the array

## Linear Scale

A scale will map a data value to a visual value.

1. Create a scale.  There are many types.  Here we'll use a linear scale

	```javascript
	var yScale = d3.scale.linear();
	```

1. Set up a visual range

	```javascript
	yScale.range([height,0]);
	```

1. Find maximum and minimum of the data set (called the "domain" of the data set)

	```javascript
	var yMax = d3.max(data, function(element){
		return parseInt(element.TMAX);
	})
	var yMin = d3.min(data, function(element){
		return parseInt(element.TMAX);
	})

	var yDomain = [yMin, yMax];
	```

	- Can combine this into one call if max/min come from same element:

	```javascript
	var yDomain = d3.extent(data, function(element){
		return parseInt(element.TMAX);
	});
	```

1. Add the domain

	```javascript
	yScale.domain(yDomain);
	```

1. Can check range and domain after initialization

	```javascript
	yScale.range();
	yScale.domain();
	```

1. Can now pass a data value into the scale to get a visual value

	```javascript
	yScale(361); //returns the visual value that maps to this data value
	```

1. Can go the opposite way

	```javascript
	yScale.invert(800); //returns the data value that maps to this visual value
	```

## Time Scale

1. Create the scale

	```javascript
	var xScale = d3.time.scale();
	```

1. Set up the visual range

	```javascript
	xScale.range([0, width]);
	```

1. Set up the date format

	```javascript
	var dateParser = d3.time.format("%Y%m%d");
	```

	- you can now parse strings of this format into dates

		```javascript
		dateParser.parse('20010101');//returns a date object
		```

	- can get a formatted string from a date object

		```javascript
		dateParser(new Date());
		```

## Axes

- Create the x axis

	```javascript
	var xAxis = d3.svg.axis();
	```

- Associate the scale with the axis

	```javascript
	xAxis.scale(xScale);
	```

- Set where on the graph the axis should appear

	```javascript
	xAxis.orient('bottom');
	```

- Set the number of ticks

	```javascript
	xAxis.ticks(8);
	```

- Append a group containing the axis after data has populated the scale

	```javascript
	viz.append('g').call(yAxis);
	```

## Events

```javascript
select.on('mouseenter', function(data, index){
	d3.select(this); //select just element that was hovered
	console.log(d3.event); //the event object
})
```

click, mouseenter and mouseleave are common

use `d3.event.sourceEvent.stopPropagation();` when events conflict

## Behaviors

### Zooming

```javascript
//generator for a behavior
//scale from 1 - 10
//.on function says, when there's an event of type 'zoom', call the 'zoomed' function.  Could be any event
var zoom = d3.behavior.zoom().scaleExtent([1,10]).on('zoom', zoomed);
var svg = d3.select('#viz-wrapper').append('svg').call(zoom);
function zoomed(){
	console.log(d3.event.translate);//get mouse position
	console.log(d3.event.scale);//bounded by 1,10 as set up above
	viz.attr('transform', 'translate(' + d3.event.translate + ')' + 'scale(' + d3.event.scale + ')');
}
```

### Dragging

```javascript
var drag = d3.behavior.drag()
	.on('dragstart', dragStart)
	.on('drag', drag)
	.on('dragend', dragEnd);
//....
dotsGroup.call(drag);
//....
function dragStart(d){ //d is the data for the dragged object
	d3.select(this); //the visual object
	d3.event.x; //x position of cursor
	d3.event.y; //y position of cursor
}
```

You can use the xScale.invert and yScale.invert to get data from d3.event.x and d3.event.y
