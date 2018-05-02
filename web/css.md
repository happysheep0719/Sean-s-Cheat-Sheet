<extoc></extoc>

# Cascading Style Sheets (CSS)

Reference: [Udemy - The Web Developer Bootcamp Section 1-4](https://www.udemy.com/the-web-developer-bootcamp/learn/v4/content)

Link: [example created by me](example.html)

## General Rule

```css
selector {
    property: value;
    antoherProperty: value;
}
```

## Link CSS to HTML

**Priority**: Inline Style > Internal Style > External Style > Default Style

- **Inline Style**
- **Internal Style**
- **External Style**
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

## Styles