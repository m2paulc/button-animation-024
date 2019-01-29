# Breakdown on the Day 24 CSS challenge
*This is the skeleton or the structure of the button*
*Basically the **HTML** of this challenge*

*I using font awesome icons on this*

```
<body>
<div class="frame">
          <input type="checkbox" id="button" class="hidden">
          <label class="button" for="button">finish<i class="fas fa-check fa-2x checked"></i>
</label>
	<svg class="circle">
	         <circle cx="30" cy="30" r="29"/>
	</svg>
</div>
</body>
```

### Now for our CSS

*Import the font to use*
```
@import url(https://fonts.googleapis.com/css?family=Open+Sans:700,300);
```

### Style our div class frame used as a container to be centered
*This is a 400px x 400px container*
```
.frame {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  height: 400px;
  margin-top: -200px;
  margin-left: -200px;
  border-radius: 2px;
	box-shadow: 4px 8px 16px 0 rgba(0,0,0,0.2);
	overflow: hidden;
  background: linear-gradient(to right bottom, #9C27B0, #42A5F5);
  color: #333;
	font-family: 'Open Sans', Helvetica, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
```

#### Let's not display the input checkbox
```
.hidden {
	display: none;
}
```

### Now let's start to style our button
*Because this is an input element **(inline)** we need to manually style and have it as a  block element. Those are the first 3 lines. We want to position it so set to **absolute.**
*Set initial width and height for the block. align using top and left attributes. set borders for styling. align to center. set font size and line height for styling. set color and set cursor to pointer for the mouse to recognize as an element that we can interact with. Lastly, set transition for the animation. Upon hover we will set the background color to something else to indicate interaction.*
```
.button {
	box-sizing: border-box;
	position: absolute;
	display: block;
	width: 260px;
	height: 60px;
	top: 170px;
	left: 70px;
	border: 2px solid #fff;
	border-radius: 30px;
	font-size: 20px;
	font-weight: 600;
	text-align: center;
	letter-spacing: 2px;
	line-height: 56px;
	text-transform: uppercase;
	transition: all .3s ease-in-out;
	cursor: pointer;
	color: #fff;

	&:hover {
		background-color: #42A5F5;
	}
}
```

#### Now to position our check icon and set the opacity.
```
.checked {
	position:absolute;
	z-index: 2;
	top: 10px;
	left: 9px;
	opacity: 0;
	color: royalblue;
}
```

#### Now style and position our svg circle
```
.circle {
	position: absolute;
	width: 60px;
	height: 60px;
	z-index: 2;
	top: 170px;
	left: 170px;
	fill: none;
	stroke: #fff;
	stroke-width: 2px;
	stroke-linecap: round;
	stroke-dasharray: 183 183;
	stroke-dashoffset: 183;
	pointer-events: none;
	transform: rotate(-90deg);
}
```

## Animation

### Now let us set the animation for the button

*At 0% initialize the start of the animation then at 50% we will set the word "finish" to transparent and then as it gets to 100% border will shrink into a circle and to make background and border to be transparent making the effect of dissappearing element.*
```
@keyframes button {
	0% {
		width: 260px;
		left: 70px;
		border-color: #fff;
		color: #fff;
	}
	50% {
		color: transparent;
	}
	100% {
		width: 60px;
		left: 170px;
		border-color: transparent;
		background: transparent;
		color: transparent;
	}
}
```

#### Now let's set first the keyframe animation that I will be using on these elements.

*To make the button oval shape into a circle*

#### *stroke-dashoffset* property in CSS defines the location along an SVG path where the dash of a stroke will begin. The higher the number, the further along the path will begin.
```
@keyframes circle {
	0% {
		stroke-dashoffset: 183;
	}
	50% {
		stroke-dashoffset: 0;
		stroke-dasharray: 183;
		transform: rotate(-90deg) scale(1);
		opacity: 1;
	}
	90%, 100% {
		stroke-dasharray: 500 500;
		transform: rotate(-90deg) scale(2);
		opacity: 0;
	}
}
```

#### Now set the fill animation keyframes
```
@keyframes fill {
	0% {
		background: transparent;
		border-color: #fff;
	}
	100% {
		background: #fff;
	}
}
```

#### Now set the check animation to end

*This is a simple one as the animation will just show the check at the end of the animation*
```
@keyframes check {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
		}
	}
```

#### Now onto using the animation on the elements and putting it all together

**The key thing here is the use of the input element because that allows us to animate via CSS. Basically when user click on the checkbox then animation would start.**

**The (~) general sibling combinator attribute basically finds any matching element or class and targets only the 2nd element only if it follows the first element and both are children of the same parent element. In this case, button class is after the input element under the same parent, the frame class.**

**both**
*The animation will follow the rules for both forwards and backwards, thus extending the animation properties in both directions.*
```
input:checked {
	&~ .button {
		animation: button .5s ease both, fill .5s ease-out 1.5s forwards;
		.checked {
			animation: check .5s ease-out 1.2s both;
		}
	}
	& ~ .circle {
		animation: circle 2s ease-out .5s both;
	}
}
```
