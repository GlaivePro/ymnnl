### Selecting elements

The [Selectors API](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors) let's you select the elements just like in CSS and jQuery.

```javascript
const element = document.querySelector('p.charming')  // returns first match
const list = document.querySelectorAll('p.strange')  // return NodeList
```

<details markdown="1">
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

<details markdown="1">
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

<details markdown="1">
<summary>jQuery equivalent</summary>
```javascript
const parent = $(element).parent()
const ancestor = $(element).closest('div.container')
```
</details>


#### The old selecting

Remember that these still work and are faster than anything else.

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
```

<details markdown="1">
<summary>jQuery equivalent</summary>
```javascript
$(parent).append(child) // or $(child).appendTo(parent)
$(parent).append(childA, childB, 'just a text string', childC)
$(parent).prepend(childX, childY) // $([childX,childY]).prependTo(parent)

$(sibling).after(anotherSibling) // or $(anotherSibling).insertAfter(sibling)
$(sibling).after(aSx, aSy) // or $([aSx, aSy]).insertBefore(sibling)
$(sibling).before(anotherSibling) // or $(anotherSibling).insertBefore(sibling)

$(element).remove()
```
</details>

<details markdown="1">
<summary>Equivalent in old/supported JavaScript</summary>
```javascript
parent.appendChild(child) // can't insert many at once
parent.insertBefore(child, null)  // yup, this is how you prepended

parent.insertAfter(newSibling, sibling)
parent.insertBefore(newSibling, sibling)

element.parentNode.removeChild(element)
```
</details>


### Element manipulation

#### Classes

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

<details markdown="1">
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

Note: the toggle with a boolean value is used:

```javascript
// to simplify this
if (condition)
	element.classList.add('strange')
else
	element.classList.remove('strange')

// into this
element.classList.toggle('strange', condition)
```

#### Data

```javascript
element.dataset.myProperty = '123'  // sets data-my-property="123" on the element
const someData = element.dataset.stuff  // retrieves value of data-stuff attribute
```

### AJAX

GETting is easy these days.

```javascript
fetch(url).then(responseCallback)

// often you unpack the response immediatelly
fetch(url)
	.then(response => response.json())
	.then(callBackDealingWithTheJsonData)
```

You can also [do more](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) complicated things with the Fetch API. But maybe that's where you'd want a library...

### And more...

If you are stuck on jQuery just for the convenience, remember that a lot of classic JS methods and properties are simple and usable like `element.textContent`, `element.innerHTML`, `element.nextElementSibling`, `element.style`, `getComputedStyle(element)`, `element.getAttribute('some-attr')`, ...

You can read about a lot of that on [YMNNJ](http://youmightnotneedjquery.com/).
