### Toggle styling

You can hide depending on value of checkbox. You can toggle the checkbox with a label
```html
<label for="toggler1" class="toggler__label">Toggle here</label>

<input class="toggler__input" id="toggler1" checked>
<div class="toggler__togglable">
	Hidable content
</div>
```

Here are the styles:

```css
.toggler__input {
	display: none;
}

toggler__input:checked + toggler__togglable {
	display: block;
}

toggler__input:not(:checked) + toggler__togglable {
	display: none;
}
```

<blockquote>
	<style>
	.toggler__input {
		display: none;
	}

	toggler__input:checked + toggler__togglable {
		display: block;
	}

	toggler__input:not(:checked) + toggler__togglable {
		display: none;
	}
	</style>

	<label for="toggler1" class="toggler__label">Toggle here</label>

	<input class="toggler__input" id="toggler1" checked>
	<div class="toggler__togglable">
		Hidable content
	</div>
</blockquote>
