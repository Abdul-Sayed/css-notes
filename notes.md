## Box Model
{Content} => {Padding} => {Border} => {Margin}

The default box sizing is content box where the width and height properties include only the content. Padding and Border are not included

Use `box-sizing: border-box;` to include padding and border in the element's total width and height

----

## Setup Boilerplate

*, html, body {
    margin: 0;
    padding: 0;
		box-sizing: border-box;
    font-family: 'Raleway', sans-serif;  // list default font here
}

----

## Positioning

`position: static`
(Default) Positions documents in the order they are written in the HTML (normal document flow)

`position: absolute`
Allows you to define an element's position relative to the top left corner of the HTML container; top: 30%, right: 50% etc
This takes the element out of the normal document flow
If an element's parent also is positioned then the element is positioned relative to the parent, not the HTML container.  

`position: relative`
Allows you to define an element's position relative to where it would normally be in the document's flow.
Setting the top, right, bottom, and left properties will move the element from its normal position. 

`position: fixed`
Allows you to define an element's position relative to the top left corner of the viewport; top: 30%, right: 50% etc.
Elements keep that position even with scrolling. Useful for sticky navbars 

`position: sticky`
Mix between position relative and fixed
div {position: sticky, top: 0} behaves as `position: fixed` when scrolled to the top of the viewport. Otherwise, it behaves as `position: relative`
Used to apply `position: fixed` to content appearing somewhere in the middle of the document


`z-index: #`
Defines the order (under or on top) of elements. Works only for positioned (not static) elements.
Higher stacking order elements overlap on top of Lower ordered elements. 


Example: Text appearing over images
	.container {
		position: relative;
	}

	.center {
		position: absolute;
		top: 50%;
		width: 100%;
		text-align: center;
	}

	img { 
		width: 100%;
		height: auto;
		opacity: 0.3;
	}

	<div class="container">
		<img src="img_5terre_wide.jpg" alt="Cinque Terre">
		<div class="center">Centered Text</div>
	</div>


----

## Display property

`display: block`
Content will occupy its own line, excluding other elements from occupying its space. Can be assigned horizontal and vertical margin/padding.

`display: inline`
Content will not occupy its own line but will be placed in line with other elements. Can be assigned horizontal margin and padding but not vertical.

`display: inline-block`
Content will arrange inline until viewport reduction forces them to occupy a new line. Can be assigned vertical and horizontal spacing. 
--------------------

## Responsive Design

Flexbox
https://css-tricks.com/snippets/css/a-guide-to-flexbox/

CSS Grid  - essentially flexbox but for two dimensions instead of just one
https://css-tricks.com/snippets/css/complete-guide-grid/

----------------

## CSS Variables
Syntax:
	:root {
		--variableName: value;
	}
Example:
	:root {
		--myColor: red;
	}

	.child {
		background-color: var(--myColor, pink)  // the pink is a fallback color in  case the variable was undefined
	}

The variables are usually defined for the document root or body. Variable values can be reassigned elsewhere in the stylesheet

---------------

## Media Queries

<!-- Fill here -->

----

## Colors

You can use named colors; https://htmlcolorcodes.com/color-names/
Or define them with RGB, HEX, HSL  
rgb(Red 0-255, Green 0-255, Blue 0-255) or rgba(Red 0-255, Green 0-255, Blue 0-255, Opacity 0-1)
#00000000 - each two digits runs from 0-0 and then A-F. The first set represents Red, then Green, then Blue, then Opacity (optional)
hsl(HUE 0-360, Saturation 0%-100%, Lightness 0%-100%) or hsla(HUE 0-360, Saturation 0%-100%, Lightness 0%-100%, Opacity 0-1)


## Selectors

### Universal Selector

	* {
		font-family: "Times New Roman", Times, serif;
	}

This selects elements where the properties specified have not been styled by any other selectors. It has low specificity, so its used as a baseline style and subsequent styles are added to specific elements later. 

### Compound Selectors; elem1, elem2, elem3 {...}

This selects all matched elements in the compound set. This selector is indicated by a , comma separating the selectors of the set. Each element within the comma separated list will be styled the same.

	h1, h2, #box {
		font-family: Arial, Helvetica, sans-serif;
	}


### Descendent Selector; parent child {...}

This selects an element that is nested (at all levels) inside of the specified parent element. This selector is indicated by a space keyboard space between the parent and the child to be selected.

Matches all <li> elements that are descendants of a <ul> element

	ul li {
		⋮ declarations
	}

Selects all <p> elements inside <div> elements

	div p {
		background-color: yellow;
	}


### Child Selector; parent > child {...}

This selects an element that is nested only one level deep inside of the specified parent element. It only selects direct children and not grandchildren. This selector is indicated by a > (greater than) symbol between the parent and the child to be selected.

	#list > li {
		border: 1px solid black;
	}


### Adjacent Sibling; adjSibling1 + adjSibling2 {...}

This selects an element that appears directly after the former element assuming they are both siblings (in the same level of nesting, in the same parent).

	h3 + p {
		color: green;
	}


### General Sibling; sibling1 ~ sibling 2 {...}

This selects all indicated elements that appear directly after the former element, in the same level of nesting, in the same parent. 

	h2 ~ p {
		color: black;
	}


### Attribute Selector

This selects an element with a matching attribute value. This selector is indicated by [] square brackets, followed by the attribute property and value of the selected element within the brackets.

Note: The data-* attributes are called data attributes. They provide a way to store custom data in an HTML attribute so it can then be easily extracted and used;

	<li data-vegetable>Tomatoes</li>
	<li data-vegetable="liquid">Olive oil</li>

	[data-vegetable] {
		color: green;
	}
	[data-vegetable="liquid"] {
		background-color: goldenrod;
	}


	img[alt="Cat"] {
		border: 1px solid black;
	}

This will target any image with an alt= "Cat"

	<img src="myimage.jpg" alt="Cat">

#### Other Attribute Selectors:

	a[href^="https"] {
		background-color: yellow;
	}

The ^= 'caret symbol and equals' sign select elements that start with the matching value, such as <a href="https://www.w3schools.com" target="_blank">Visit W3Schools.com!</a>
----
	p[class$="dog"] 

The $= 'dollar and equals' sign select elements that end with the matching value, such as all classes that end with "dog"

	<p class="bigdog">...</a>.

----
	img[alt*="love"] 

The *= 'asterisk and equals' sign select elements that have the matched characters appearing anywhere within the value, such as 

	<img src="myimage.jpg" alt="Your lovely elbow.">.

----
	p[class~="monkey"] 

The ~= 'tilde and equals' sign select elements that contain the term within a space separated value, such as 

	<p class="zoo monkey details">...</p>.

----
	p[class|="birds"] 

The |= pipe symbol selects elements that contain the term within a dash separated value, such as 

	<p class="new-birds-today">...</p>.


### Pseudo Class Selectors

This selects an element based on the state described in the selector. This selector is indicated by the : colon symbol, followed by the pseudo class state

	a:link {
		text-decoration: none;
	}

#### Other Pseudo Class Selectors Include:

	`a:link`

selects links in their default state before the visitor has interacted with them.
----
	`a:visited`

selects links after the user has already clicked on them and is visiting that page again.
----
	`a:hover` 

selects links when the user is hovering their mouse over the link.
----
	`a:active` 

selects links for only the moment when the mouse button is pressed when clicking on the link.
----
	`:checked`

selects radio buttons or check boxes that have been checked

	input[type=radio]:checked {
		border: 1px solid black;
	}
----

	`p:first-child` 

selects elements that are the first child when appearing inside a common parent. Such as 

	<div>
		<p>I'm selected</p>
		<p>I'm not</p>
		<p>Neither am I</p>
	</div>
----

	`p:last-child` , `p:last`

selects elements that are the last child when appearing inside a common parent. Such as 

	<div>
		<p>I'm not selected</p>
		<p>Neither am I</p>
		<p>I'm selected</p>
	</div>

----
	`:nth-child(n)`

selects the specified child or set of children;

	li:nth-child(2) , li:nth-child(2n)

To select the 2nd list item or every second list item. 

----
	`X:nth-last-child(n)`

	li:nth-last-child(2) {
		color: red;
	}

select the indicated number from the last list item
----

	`X:nth-of-type(n)`

	ul:nth-of-type(3) {
		border: 1px solid black;
	}

selects the 3rd ul
----

	:not

selects all elements except the one indicated;

	div:not(#container) {
		color: blue;
	}

## CSS Transitions

	div {
		width: 100px;
		height: 100px;
		background: red;
		transition-property: width;  // CSS property to apply transition to, required
		transition-duration: 2s;  // required
		transition-timing-function: linear;  // options: ease (default), linear, ease-in, ease-out, ease-in-out, cubic-bezier(n,n,n,n)
		transition-delay: 1s;
		transition: width 2s linear 1s;  // shorthand
	}

To use the transition, specify the end state of the transitioned CSS property;

		div:hover {
			width: 300px;
		}

## Fonts

### Web Fonts Icons

Create img tags for only the font icons your using rather than importing an entire font library; https://icons8.com/icons

Download icons for local use here;  https://simpleicons.org/


### Local Fonts
In the fonts folder of your project, create a webfont file. Then use it in a css file as;

@font-face {
	font-family: 'Skolar';
	src: url(../fonts/Skolar.webfont),
			 url(../fonts/Booter) format("woff")
}

p {font-family: 'Skolar', Georgia, serif;}

### Font sizing

`em` is based on the font of the parent element. So if body { font-size: 20px }, then 1 em = 20px;
`rem` is based on the font size of the browser's root document, usually 16px. This allows elements to adjust their size when zooming. 


## Full Page BAckground image
	body, html {
		height: 100%;
	}

	.bg { 
		/* The image used */
		background-image: url("img_girl.jpg");

		/* Full height */
		height: 100%; 

		/* Center and scale the image nicely */
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
		background-color: rgba(0,0,0,0.6);
    background-blend-mode: multiply;
	}