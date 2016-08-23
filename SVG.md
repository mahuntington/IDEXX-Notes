# SVG

## Base tag

Everything goes inside here

```xml
<svg></svg>
```

## Positioning

SVG tag is an inline element

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
<circle r="50" cx="200" cy="300"/>
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

- attributes
	- `x` x position of top left
	- `y` y position of top left

```xml
<rect x="50" y="20" width="150" height="150"></rect>
```

## Ellipse
## Polygon
## Polyline
## Path

## Styling

Can be done with attributes:

- `fill=red` or `fill=#ff0000` fill color
- `stroke=red` or `stroke=#ff0000` stroke color
- `stroke-width=4` width of stroke
- `fill-opacity=0.5` transparency of fill
- `stroke-opacity=0.5` transparency of stroke
- `transform = "translate(2,3)"`
- `transform = "scale(2.1)"`
- `transform = "rotate(45deg)"`


Can also be done with CSS:

```css
circle {
	fill:red;
	stroke:blue;
	stroke-width:3;
	fill-opacity:0.5;
	stroke-opacity:0.1;
	transform:rotate(45deg) scale(0.4) translate(155px, 1px);
}
```

## Text

Content of tag is the text

```xml
<text x="0" y="15">I love SVG!</text>
```

Can use font-family and font-size CSS styling

## Group

- `<g></g>`
- can put multiple elements inside it.
- positioning and styling apply to children


## Documentation

https://developer.mozilla.org/en-US/docs/Web/SVG/Element
