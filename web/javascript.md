<extoc></extoc>

# Javascript

[MDN JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

## Useful Built-in Methods

```javascript
clear();
console.log("Hi");
alert("Hello!");
var userName = prompt("What is your name?"); // input from user
```

## Control Flow

```javascript
x = "5"
x == 5
```

## Function

```javascript
//funciton declaration
function captilaize(str){
    return str.charAt(0).toUpperCase() + str.slice(1);
}
// function expression
var capitalize = function(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
}
```

## Scope Chain

the context that code is executed in.

### Hoisting

Hoisting is a JavaScript mechanism where **variables and function declarations** are moved to the top of their scope before code execution.

## Closure 闭包

```javascript
function f1(){
    var n = 999; // normally it cannot be accessed from outside
    nAdd = function(){ n += 1 }
    function f2(){ // via function f2, we can access n from outside
        alert(n);
    }
    return f2;
}
```

## BOM & DOM

The **BOM (Browser Object Model)** consists of the objects navigator, history, screen, location and document which are children of window


The **Document Object Model (DOM)** connects web pages to scripts or programming languages. 

- DOM nodes can have **event handlers** attached to them. Once an event is triggered, the event handlers get executed.

### Access DOM

```javascript
document.getElementById(id) //Find an element by element id
document.getElementsByTagName(name) //Find elements by tag name
document.getElementsByClassName(name) //Find elements by class name
```

## Event

```javascript
var div1 = document.getElementById('myid');

div1.onclick = function (ev) {
    alert("div is clicked!");
}

div1.addEventListener('click', function () {
    alert('this is div with id');
}, true)
```