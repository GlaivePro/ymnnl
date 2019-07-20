### Toggle styling

You can hide depending on value of checkbox. You can toggle the checkbox with a label
```html
<label for="toggler1" class="toggler__label">Toggle here</label>
<input type="checkbox" class="toggler__input" id="toggler1" checked>
<div class="toggler__togglable">
	Hidable content
</div>
```

Here are the styles:

```css
.toggler__input {
	display: none;
}

.toggler__togglable {
	display: none;
}

.toggler__input:checked + toggler__togglable {
	display: block;
}
```

<style>
	.toggler__input {
		display: none;
	}

	.toggler__togglable {
		display: none;
	}

	.toggler__input:checked + toggler__togglable {
		display: block; /* the style that you want to turn on/off */
	}
</style>

<label for="toggler1" class="toggler__label">Toggle here</label>
<input type="checkbox" class="toggler__input" id="toggler1" checked><div class="toggler__togglable">
	Hidable content
</div>

Of course, it's better to use [details](#details-is-the-spoiler-thing) if you just want to show and hide a block of content right after your label.


### Use the :target selector

While you don't want the address bar and browser's history littered on any changes of visual state, sometimes you do. Like when looking at a gallery of images. If so, you can select the relevant element using the `:target` pseudo-class.

```html
<a href="#image1">
	<img 
		class="gallery__image"
		id="image1" 
		src="http://placecorgi.com/100/300?a" >
</a>
<a href="#image2">
	<img 
		class="gallery__image"
		id="image2" 
		src="http://placecorgi.com/100/300?b" >
</a>
<a href="#image3">
	<img
		class="gallery__image" 
		id="image3"
		src="http://placecorgi.com/100/300?c" >
</a>
```

```css
.gallery__image {
	width: 100px;
	height: 100px;
	object-fit: cover;
}

.gallery__image:target {
	width: 300px;
	height: auto;
	object-fit: none;
}
```

<style>
	.gallery__image {
		width: 100px;
		height: 100px;
		object-fit: cover;
		filter: hue-rotate(33deg);
	}

	.gallery__image:target {
		height: auto;
		filter: none;
	}
</style>

<a href="#image1">
	<img 
		class="gallery__image"
		id="image1" 
		src="http://placecorgi.com/100/300?a" >
</a>
<a href="#image2">
	<img 
		class="gallery__image"
		id="image2"
		src="http://placecorgi.com/100/300?b" >
</a>
<a href="#image3">
	<img
		class="gallery__image" 
		id="image3" 
		src="http://placecorgi.com/100/300?c" >
</a>

You can create both [lightboxes](https://codepen.io/gschier/pen/HCoqh) and [galleries](http://thewebrocks.com/demos/targetgallery/) like that. By the way that final example is from the February of 2012.


### Validation

If you use HTML validation, you can also style your inputs using `:valid`, `:invalid` and other pseudo-classes.

```html
<input class="validation__range" type="number" min="1" max="3" value="7">
<span class="validation__error">The number should be between 1 and 3.</span>

<input class="validation__invalid" type="email" placeholder="enter an email" required>
```

```css
.validation__error {
	display: none;
}

.validation__range:out-of-range + .validation__error {
	display: inline;
}

input:required {
	border: 1px orange solid;
}

.validation__invalid:valid {
	border-bottom: 3px green solid;
}
```

<style>
	.validation__error {
		display: none;
	}

	.validation__range:out-of-range + .validation__error {
		display: inline;
	}

	input:required {
		border: 1px orange solid;
	}

	.validation__invalid:valid {
		border-bottom: 3px green solid;
	}
</style>

<input class="validation__range" type="number" min="1" max="3" value="7">
<span class="validation__error">The number should be between 1 and 3.</span>

<input class="validation__invalid" type="email" placeholder="enter an email" required>


### And other possibilities

There is a million things that can be done with just CSS. Including games like [this](https://codepen.io/elad2412/pen/hBaqo) and [this](https://codepen.io/jcoulterdesign/pen/NOMeEb) or even [without any HTML](https://codepen.io/SelenIT/pen/oXzMbR).

Recall the toggling example above? You could as well use radio buttons instead and make yourself a carousel. You don't even have to put every input just before the content, you can `.carousel__input:nth-of-type(4) ~ .carousel__slide:nth-of-type(4)` to have fourth input correspond to fourth slide. And in that way you refer to multiple elements that you style according to state of that input.

