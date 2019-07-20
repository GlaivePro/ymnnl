### Semicolons in JavaScript

Did you notice that none of the JavaScript examples had any semicolons? There is a feature called automatic semicolon insertion (ASI) in JS. You can read up on it yourself, but a general rule is that you don't need to terminate your statements with a semicolon unless you start the next line with a `[` or `(`.

### Optional tags

#### Closing tags

Some the HTML tags are optional to close. It's often to see `<p>` without a closing tag. But `body` and `html` are also optional to close. And is there ever a point to have `</body>` and `</html>` included in your document? It's even optional to close `head`. You can just start the body.

Other tags that are closed automatically include `li`, `option`, `dt`, `dd`, `tr`, `th`, `td`, `thead`, `tbody`, `tfoot`. This is not a complete list but these are the common ones that are often more readable if just followed by the next sibling instead of closing tag.

Here is a nice example from [WHATWG](https://html.spec.whatwg.org/multipage/syntax.html) that shows how readable is a table without closing tags inside.

```html
<table>
 <caption>37547 TEE Electric Powered Rail Car Train Functions (Abbreviated)
 <colgroup><col><col><col>
 <thead>
  <tr> <th>Function                              <th>Control Unit     <th>Central Station
 <tbody>
  <tr> <td>Headlights                            <td>✔               <td>✔
  <tr> <td>Interior Lights                       <td>✔               <td>✔
  <tr> <td>Electric locomotive operating sounds  <td>✔               <td>✔
  <tr> <td>Engineer's cab lighting               <td>                 <td>✔
  <tr> <td>Station Announcements - Swiss         <td>                 <td>✔
</table>
```

#### Opening tags

Some of the opening tags are also optional. For example, many of us have written a table with tree such as this.

```html
<table>
	<tr> <td>first   <td>second   <td>third
	<tr> <td>fourth  <td>fifth    <td>sixth
</table>
```

Have you noticed that the rows get wrapped in a `tbody` automatically? It turns out that both the opening and closing tags of `tbody` are optional - you don't have to specify them if you want them left at the default positions.

And you actually don't have to include `<html>`, `<head>` and `<body>`... with the caveat that you need to specify tag if you want any attributes there and you usually want `<html lang=..>`.

A more complete discussion on tag omission can be found [here](https://html.spec.whatwg.org/multipage/syntax.html#syntax-tag-omission) at WHATWG.

Some [guidelines](https://google.github.io/styleguide/htmlcssguide.html#Optional_Tags) even suggest skipping all of the optional tags. I do the same unless I'm working with Vue.
