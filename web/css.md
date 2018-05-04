<extoc></extoc>

# Cascading Style Sheets (CSS)

Reference: 

[Udemy - The Web Developer Bootcamp Section 1-4](https://www.udemy.com/the-web-developer-bootcamp/learn/v4/content)

[Morilla MDN](https://developer.mozilla.org/zh-CN/)

[example created by me](example.html)

## General Rule

```css
selector {
    property: value;
    anotherProperty: value;
}
```

## Link CSS to HTML

- **Inline Style**
    - put in the element you want to select
    
    ```html
    <li style="color:purple;">Playing</li>
    ```
    
- **Internal Style**
    - put in the head
    
    ```html
    <style type="text/css">
        li {
            color: #000000;
        }
    </style>
    ```

- **External Style**
    - put link tag in the head
    
    ```html
    <link rel="stylesheet" type="style/css" href="css.css">
    ```
    
- **Default Style**


## CSS Selectors

- **Element Selector** - Select all instances of a given element

```css
h1 {
    background: green;
}
```

- **ID Selector** - Select an element with a given ID. Only one per page

```css
#ID1 {
    color: yellow;
}
```

- **Class Selector** - Select all elements with a given class

```css
.CLASS1{
    color: purple;
}
```

- **Muiltiple Class** for one element
```html
<p class="CLASS1 CLASS2">
```

实际开发中，一般把Class给CSS用，把ID给JavaScript用。

### Combinator Selectors

- **Star** - `*` - select all

```css
* {
    border: 1px solid;
}
```

- **Descendant Selectors** - `element1 element2`

```css
li a {
    color: red;    
}

li .hello{
    color: green;
}
```

- `element > element` - select all sons

- **Adjacent Selectors**

```css
h4 + ul {
    border: 4px solid red;
}
```

- **AND Selector** - `element : element`
- **OR Selector** - `element , element`
- **Attribute Selector** - `[attribute]` - select all elements with a given attribute 
    - `p[class="right"]`
    - `[attribute = value]` 
    - `[attribute ~= value]`

```css
a[herf="http://www.google.com"] {
    background: blue;
}
```

- **n-th of type**

```css
li:nth-of-type(even){
    background: blue;
}
li:nth-of-type(3){
    background: red;
}
```

- **Pseudo classes**
    - `:link` - (`a:link`) select all unvisited links
    - `:hover` - (`a:hover`) select links on mouse over 鼠标在上面停靠
    - `:active` - (`a:active`) select the active link
    - `:visited` - (`a:visited`) select all visited links
    - `:first-child`- (`p:first-child`)select every `<p>` element
-**Pseudo elements**
    - `::first-element` does not work on inline elements, such as span


### Specificity 

[Specificity Calculator](https://www.google.com/search?q=specificity+calculator&rlz=1C5CHFA_enUS760US761&oq=specificity+calc&aqs=chrome.1.69i57j0l5.5799j0j7&sourceid=chrome&ie=UTF-8)

when we have Multiple styles for one element:

- **More Specific** rules win
    - **Inline Styles** > **IDs** > **Classes, Attributes and pseudo-classes** > **Elements and peseudo-elements** > **Inherited Style**
- **Closer** rules win
    - **Inline Style** > **Internal Style** > **External Style** > **Inherited Style** > **Default Style**


## Properties

### Color

Tool: 
[Color Picker](https://www.google.com/search?q=color+picker&rlz=1C5CHFA_enUS760US761&oq=color+picker&aqs=chrome..69i57j0l5.4985j0j7&sourceid=chrome&ie=UTF-8)

- Built-in color
- Hexidecimal
- RGB
- RGBA
    - alpha makes color transparent.
    - in range [0, 1]

```css
h1 {
    color: red;
}
h2 {
    color: #00FF00;
}
h3 {
    color: rgb(0, 0, 255);
}
h4 {
    color: rgba(11, 99, 150, .2)
}
```

### Font

Tools:

[Google Fonts](https://fonts.google.com/)

- `font-family`
- `font-size`
    - `16px`, `1.0em` relative around 16px
- `font-weight`
    - `normal`, `bold`, `100` - `800`
- `text-decoration`
    - `underlined`

## The Box Model

- Composition
    - **`Content`**
    - **`Padding`** - inside
    - **`Border`**
    - **`Margin`** - outside
        - `20px 20px 20px 20px`
        - `auto` for left and right margin. If we set left or right margins to be auto, it will center for us.
        - **margin collapsing**
- `float`
    - `none` / `left` / `right` / `initial` / `inherit`
    - put float elements in front of non-float elements first
    - `clear` property specifies on which side of one element other floating elements are not allowed to float
- `position`
    - `static` / `dafault` - non-positioned
    - `relative` - relative to its original position
    - `absolute` - relative to the nearest positioned ancestor
    - `fixed` - relative to the viewport (stays in the exact same place even if the page is scrolled)
- `z-index`
    - only valid for positioned elements