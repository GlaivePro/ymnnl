### Toggle styling

You can hide depending on value of checkbox. You can toggle the checkbox with a label
```html
<label for="toggler1" class="toggler__label">Toggle here</label>
<input type=checkbox class="toggler__input" id="toggler1" checked>
<div class="toggler__togglable">
	Hidable content
</div>
```

Here are the styles:

```css
.toggler__input {
	display: none;
}

toggler__togglable {
	display: none;
}

toggler__input:checked + toggler__togglable {
	display: block;
}
```

<blockquote>
	<style>
	.toggler__input {
		display: none;
	}

	toggler__togglable {
		display: none;
	}

	toggler__input:checked + toggler__togglable {
		display: block;
	}
	</style>

	<label for="toggler1" class="toggler__label">Toggle here</label>
	<input type=checkbox class="toggler__input" id="toggler1" checked>
	<div class="toggler__togglable">
		Hidable content
	</div>
</blockquote>
