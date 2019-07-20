<!doctype html>

<title>You Might Not Need a Library</title>

<style>
	.comparison {
		display: grid;
	}
</style>

# You Might Not Need a Library

JavaScript and CSS improves on most sunny days. They add support for features that were previously done by libraries, sometimes even mimicking the API. And sometimes there was a native feature all along that has slipped past many of us. This page aims to provide a collection of things like that.

Beware that these examples include code that might be unsupported in some browsers with IE and Safari being the most often victims.

## Raw JavaScript can do it

### Selecting elements

The [Selectors API](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors) let's you select the elements just like in CSS and jQuery.

```javascript
const element = document.querySelector('p.charming')  // returns first match
const list = document.querySelectorAll('p.strange')  // return NodeList
```

<details>
	<summary>jQuery equivalent</summary>
	```javascript
	const element = $('p.charming').first()
	const list = $('p.charming')
	```
	Note: the jQuery examples end up with a jQuery object not a raw element or NodeList so they are technically not equivalent. But it seemed silly to add `[0]` as that's not used if you actually work with jQuery.
</details>

Some people like to alias these to `$('p.charming')` and `$$('p.strange')`, but it might be mistaken for jQuery.

Remember that NodeList has a `forEach` method and the `length` property. You can loop over it however you like without creating an array or retrieving `Array.prototype.forEach`.

#### Children, descendants

The same API works for selecting inside an element.

```javascript
const descendantElement = element.querySelector('p.charming')
const list = element.querySelectorAll('p.strange')

const children = element.children
// to select among direct descendants use :scope pseudo-class that refers to element
const selectedChildren = element.querySelectorAll(':scope > p')
```

<details>
	<summary>jQuery equivalent</summary>
	```javascript
	const childElement = $(element).find('p.charming').first()
	const list = $(element).find('p.strange')
	const children = $(element).children()
	const selectedChildren = $(element).children('p')
	```
</details>


#### Parents, ancestors

```javascript
const parent = element.parentNode // there is also .parentElement if you want to get confused

// go up the tree until something matches
const ancestor = element.closest('div.container')
```

<details>
	<summary>jQuery equivalent</summary>
	```javascript
	const parent = $(element).parent()
	const ancestor = $(element).closest('div.container')
	```
</details>


#### The old selectors

These still work and are faster than anything else.

```javascript
document.getElementById('higgs')
document.getElementsByClassName('top')
document.getElementsByTagName ('input')
document.getElementByName('attachments[]')  // let me know if you have ever used this

// or search descendants in an element
element.getElementsByClassName('bottom')
element.getElementsByTagName ('label')
element.getElementByName('attachments[]')
```

### DOM manipulation

```javascript
// move or insert (if it's a new node)
parent.append(child)
parent.append(childA, childB, 'just a text string', childC)
parent.prepend(childX, childY)

sibling.after(anotherSibling)
sibling.after(aSx, aSy)
sibling.before(anotherSibling)

// remove
element.remove()

// empty
element.innerHTML = ''

// copy
const dupe = element.cloneNode(true)  // true -> copy subtree, false -> just the element without any content
```

<details>
	<summary>jQuery equivalent</summary>
	```javascript
	$(parent).append(child) // or $(child).appendTo(parent)
	$(parent).append(childA, childB, 'just a text string', childC)
	$(parent).prepend(childX, childY) // $([childX,childY]).prependTo(parent)

	$(sibling).after(anotherSibling) // or $(anotherSibling).insertAfter(sibling)
	$(sibling).after(aSx, aSy) // or $([aSx, aSy]).insertBefore(sibling)
	$(sibling).before(anotherSibling) // or $(anotherSibling).insertBefore(sibling)

	$(element).remove()

	$(element).empty()

	const dupe = $(element).clone(false)  // true -> copy jquery data and events as well
	```
</details>

<details>
	<summary>Equivalent in old/supported JavaScript</summary>
	```javascript
	parent.appendChild(child) // can't insert many at once
	parent.insertBefore(child, null)  // yup, this is how you prepended

	parent.insertAfter(newSibling, sibling)
	parent.insertBefore(newSibling, sibling)

	element.parentNode.removeChild(element)

	element.innerHTML = ''

	const dupe = element.cloneNode(true)
	```
</details>

### These still work as well

```javascript
element.innerHTML = ''  //empty it
```

## Element manipulation

### Classes

```javascript
element.classList.add('strange')  // or element.classList.toggle('strange', true)
element.classList.add('stranger', 'charming')

// when you're tired of spelling element.classList
const cl = element.classList

cl.remove('stranger')  // or cl.toggle('stranger', false)
cl.toggle('charming')
cl.replace('strange', 'strangest')

var hasClass = element.classList.contains('charming')
```

<details>
	<summary>jQuery equivalent</summary>
	```javascript
	$(element).addClass('strange') // or $(element).toggleClass('strange', true)
	$(element).addClass('stranger charming')

	// when you're tired of spelling $(element)
	const el = $(element)

	el.removeClass('stranger')  // or el.toggleClass('stranger', false)
	el.toggleClass('charming')
	el.switchClass('strange', 'strangest')

	var hasClass = el.hasClass('charming')
	```
</details>

Note: the toggle with a boolean value is used to simplify this:

```javascript
if (condition)
	element.classList.add('strange')
else
	element.classList.remove('strange')

// into 
element.classList.toggle('strange', condition)
```

### Data

```javascript
element.dataset.myProperty = '123'  // set data-my-property="123" on the element
```



## AJAX

GETting is easy these days.

```javascript
fetch(url).then(responseCallback)

// often you unpack the response immediatelly
fetch(url)
	.then(response => response.json())
	.then(callBackDealingWithTheJsonData)
```

You can also [do more](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) complicated things with the Fetch API. But maybe that's where you'd want a library...

## You can do it without JS



## You only need HTML for some things

## And there are some things you don't even need
