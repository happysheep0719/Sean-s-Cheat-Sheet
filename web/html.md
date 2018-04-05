<extoc></extoc>

# HTML

Reference: [Udemy - The Web Developer Bootcamp Section 1-4](https://www.udemy.com/the-web-developer-bootcamp/learn/v4/content)

Link: [example created by me](example.html)

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

### Semantic Tags in HTML5

- `<strong>` for `<b>`
- `<em>` for `<i>`

### List

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

### Image

`<img>` is a self-closing tag.

```html
<img src="">
```

### Link

```html
<a href="http://www.google.com"></a>
```

### Generic Container

- inlined container - `<span>`
- block level container - `<div>`

### Table

Inside tags:

- table head - `<th>`
- table row - `<tr>`
- table div - `<td>`

```html
<!--HTML style-->
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

<!--HTML5 Style-->
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

### Form

__Attributes__

- `action` - where the form send data to
- `method` - what HTTP method (`get`/`post`)
- `name` - the key of the input


Inside the form, we have __tags__ named with:

- `<input>`
    - **Attributes**
        - `type`
        - `name`
        - `value`
        - `id`
        - `placeholder`
        - `required`
        - `pattern`
        - `title`
- `<label>`
    - `for`
- `<select>`
    - **Inside Tags**: `<option>`

```html
<form action="example.html" method="GET">
	<p>
		<label for="firstname">First Name:</label>
		<input type="text" name="fn" id="firstname" placeholder="John" required="">
		<label for="lastname">Last Name:</label>
		<input type="text" name="fn" id="lastname" placeholder="Smith" required="">
	</p>
	<p>
		<input type="radio" name="g" value="m" id="male">
		<label for="male">Male</label>
		<input type="radio" name="g" value="f" id="female">
		<label for="female">Female</label>
	</p>
	<p>
		<label for="email">Email:</label>
		<input type="email" name="em" id="email" placeholder="your email" required>
		<label for="password"></label>
		<input type="password" name="pw" id="password" placeholder="your password" required title="None Empty Chars 3-6" minlength="3" maxlength="6" pattern="\w{2,}">
	</p>
	<p>
		<label>Birthday:</label>
		<select name="bd-m">
			<option value="">Month</option>
			<option value="1">Jan</option>
			<option value="2">Feb</option>
		</select>
		<select name="bd-d">
			<option value="">Day</option>
			<option>1</option>
			<option>2</option>
		</select>
		<select name="bd-y">
			<option value="">Year</option>
			<option>1994</option>
			<option>2018</option>
		</select>
	</p>
	<p>
		<label for="agree">I agree to the terms and conditions:</label>
		<input type="checkbox" name="agree">
	</p>
	<p><input type="submit" ></p>
</form>
```

