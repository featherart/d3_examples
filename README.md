d3_examples
===========

Edward Tufte - The Visual Display of Quantitative Information
Statistician who wrote the bible on data display; a great reference for anyone wanting to explore this area further (also you should know who he is) - 
famous Voronoi data visualization used by physician John Snow in the 1850’s to identify the source of a cholera outbreak in London’s SoHo neighborhood.

Artist Sol LeWitt - conceptual artist who turned data visualization into an art form;
blurring line between art/data display

d3 was written by Mike Bostock, and all source is on Github. 

Great book on d3 called “Interactive Data Visualization” by Scott Murray, can be downloaded for free!
http://chimera.labs.oreilly.com/books/1230000000345/

Loads of beautiful d3 data graphs out there - often used in NYT articles, etc.
https://github.com/mbostock/d3/wiki/Gallery

D3 -
What it does:
- loads data into browser’s memory
- binds data to elements within the document
- transforms the elements for visual representation - allows you to show trends with data visually
- animates or transitions elements interactively between states in response to users input, so they can interact with data

- intended for explanatory visualization but doesn’t provide canned charts
- code is executed on the client, so usually more speedy than server calls BUT your data will be on the client & thus more easily accessible
- doesn’t support old versions of browsers; won’t work on old IE, for ex.
- doesn’t handle bitmaps but works well with anything vector-based (SVG, GeoJSON data, anything JSON, ...)
  Bitmaps => pixel-based, hard to resize & transform (Google maps)
	Vector images => based on lines, points, curves & easier to resize
- d3 can take data in almost any form! CSV files, TSV files, Hashes, Arrays, Arrays of Arrays, …

SVG - “scalable vector graphic”, an XML tool for drawing shapes, since it’s XML all tags must open & close (or self-close)

SVG.html page to show code examples

d3 binds to SVG elements the way that JQuery binds to DOM elements
We see the familiar “attr” but here it’s used to design the image
We also see closures, but rather than acting on an event, or “e” they will pass in datum, index or “d,i” and they will always return something


Important methods:
- .select to get the DOM element
- .selectAll to create the SVG element (it’s not really a good name for what it does as you are “selecting” things that don’t exist yet)
- .scale to map unruly data to a container - most commonly linear() but lots of other methods exist, including ordinal() for data that isn’t numeric or continuous
- .range(0, w) or (0,h) the pixels to map to, or the size of your diagram, .rangeRound gives a nice whole number to avoid anti-aliasing issues
- .domain(x, y) to state the upper & lower limit of data --> d3.min & d3.max to figure out on the fly
- accessor functions - closures entered into max or min that tells which data to use (in an array of arrays d[0], d[1] maps to x, y)


Animation:
transition() gives basic animation, can be chained to:
- duration(#time) to slow/quicken animation
- ease(“linear”) or ease(“bounce”) to give animation more pizazz
- delay(function) to make animations stagger
- each(“start”) or (“end”) to mark the start/end of a transition &/or shift in data

JQuery: transitions execute sequentially
d3: transitions execute on a trigger, so new ones will interrupt & override older

--> start is for immediate transitions only, but end can have more stuff b/c already executed by then

clipping path - like a mask - can define/assign an id or add visual elements w/in it

enter() --> to update data when it changes, first time it loads data but it can be chained to data changes: foo.enter( function(d,i) { more stuff happens here; }

Interaction:
Much like jQuery you have the standard on click, mouseover, mouseout event handlers
Unlike jQuery they are tied to changes in display when data updates
Also, new animations will interrupt older ones (jQuery does them sequentially)

Layouts: 
There are several different layouts in d3. A complete list is in the book in Chapter 11, but basically everything you want is in there, most likely. Pie charts are nice b/c you don’t have to think about Trig to build one.

Tool tip - you can attach a CSS style to these to make them super awesome

GeoJSON & maps - an entire chapter in the book is dedicated to this, Chapter 12. You will see how d3 creates paths:

var path = d3.geo.path();


chloropleths, or color-coded maps can be created using code like this:

var color = d3.scale.quantize().range([“rgb(237,248,233)”, “rgb(186,228,179)”, “rgb(116,196,118)”, “rgb(49,163,84)”, “rgb(0,109,44)”]);

d3.csv(“data”)

color.domain([d3.min(data, function(d) { return d.value; }),
		d3.max(data, function(d) { return d.value; }) ]);

The quantize scale function is linear but outputs values in a discrete range, and the domain closures are creating the relationship between data and color values.

More Resources:
start here:
http://d3js.org/

on selection!
http://bost.ocks.org/mike/selection/

more tutorials:
https://www.dashingd3js.com/table-of-contents

tons of examples from NY Times, etc.:
http://bost.ocks.org/mike/
