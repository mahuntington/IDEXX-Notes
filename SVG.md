# SVG

SVG tag is an inline element

## Positioning
- (0,0) - x = 0, y = 0
- starts at top left
- y increases vertically down
- can use negative values
	- -x goes left
	- -y goes up

## Circle

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

## Line

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

## Rectangle
## Ellipse
## Polygon
## Polyline
## Path
## Text

- Content of tag is the text

## Transform

Is an attribute

- `transform = "translate(x,y)"`
- `transform = "scale(factor)"`
- `rotate = "rotate(degrees)"`

## Group

- `<g></g>`
- can put multiple elements inside it.
- positioning and styling apply to children

## Styling

Can be done with attributes:

- `fill=red` or `fill=#ff0000` fill color
- `stroke=red` or `stroke=#ff0000` stroke color
- `stroke-width=4` width of stroke

Can also be done with CSS:

```css
circle {
	fill:red;
	stroke:blue;
	stroke-width:3;
}
```
