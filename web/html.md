<extoc></extoc>

# HTML

[Test](test.html)

## Document
```html
<!DOCTYPE html> <!-- this is for html 5. -->
<html>
<head>
    <title>my title</title>
</head>
<body>
</body>
</html>
```

## Elements & Attributes

Link: [MDN element reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

Link: [Attribute List](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)


- inline element: `<b>`, `<i>`, `<spam>`, `<a>`
- block level element: `<h1>`, `<h2>`, `<h6>`, `<p>`, `<div>`.

__Semantic Tags in HTML5__

- `<strong>` for `<b>`
- `<em>` for `<i>`

__List__

- Ordered List
- Unordered List

```html
<h1>HTML</h1>
<ul>
	<li>Stands for <strong>Hyper Text Markup Language</strong></li>
	<li>Lots of tags</li>
		<ul>
			<li>Boilerplate</li>
			<li>Headings</li>
		</ul>
	
</ul>
```

__Image__

`<img>` is a self-closing tag.

```
<img src="">
```

__Link__

```html
<a href="http://www.google.com"></a>
```

__Generic Container__

- inlined container - `<span>`
- block level container - `<div>`

__Table__

- HTML style

```html
<table border="1">
	<tr>
		<th>Name</th>
		<th>Age</th>
	</tr>
	<tr>
		<td>Rusty</td>
		<td>2</td>
	</tr>
	<tr>
		<td>Wyatt</td>
		<td>3</td>
	</tr>
</table>
```

- HTML5 Style

```html
<table border="1">
<thead>
	<tr>
		<th>Name</th>
		<th>Age</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>Rusty</td>
		<td>2</td>
	</tr>
	<tr>
		<td>Wyatt</td>
		<td>3</td>
	</tr>
</tbody>
</table>
```

__Form__

Attributes with:

- `action` - where the form send data to
- `method` - what HTTP method (`get`/`post`)
- `name` - the key of the input


Inside the form, we have tags named with:

- `input`
- `label` - two different ways of writing a label.

```html
<!-- It tries to get: https://www.wikipedia.org/?nUser=ass&nPW=dd-->
<form action="http://wikipedia.com" method="GET">
	<label>
		Username:
		<input name="nUser" type="text" placeholder="username">
	</label>
	<label for="password">Password:</label>
	<input id="password" name="nPW" type="password" placeholder="password">
	<input type="submit">
</form>
```


