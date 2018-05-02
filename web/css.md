<extoc></extoc>

# Cascading Style Sheets (CSS)

Reference: [Udemy - The Web Developer Bootcamp Section 1-4](https://www.udemy.com/the-web-developer-bootcamp/learn/v4/content)

Link: [example created by me](example.html)

## General Rule

```css
selector {
    property: value;
    anotherProperty: value;
}
```

## Link CSS to HTML

**Priority**: Inline Style > Internal Style > External Style > Default Style

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


### CSS Syntax and Selectors

Selector

实际开发中，一般把Class给CSS用，把ID给JavaScript用。

Combinator

- `element element` - select descendents
- `element > element` - select all sons
- `element, element` - select the union of two elements
- `[attribute]` - select all elements with a given attribute 
    - Eg. `p[class="right"]`
    - `[attribute = value]` 
    - `[attribute ~= value]`
- pseudo classes
    - `:link` - (`a:link`) select all unvisited links
    - `:hover` - (`a:hover`) select links on mouse over
    - `:active` - (`a:active`) select the active link
    - `:visited` - (`a:visited`) select all visited links
    - `:first-child`- (`p:first-child`)select every `<p>` element

## Properties

### Color

Tool: 
[Color Picker](https://www.google.com/search?q=color+picker&rlz=1C5CHFA_enUS760US761&oq=color+picker&aqs=chrome..69i57j0l5.4985j0j7&sourceid=chrome&ie=UTF-8)

- Built-in color
- Hexidecimal
- RGB
- RGBA - alpha makes color transparent

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