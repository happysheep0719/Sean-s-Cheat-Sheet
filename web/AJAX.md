<extoc></extoc>

# AJAX

[MDN Ajax](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX)

AJAX is short for **Asynchronous JavaScript + XML**.

- A browser built-in `XMLHttpRequest ` object (to request data from a web server)
- JavaScript and HTML DOM (to display or use the data)

```javascript
var req = new XMLHttpRequest();
req.open("GET", "a.jpg", true);
req.send();
```

**When use POST?**

- A cached file is not an option (**update a file or database on the server**).
- **Sending a large amount of data** to the server (POST has no size limitations).
- **Sending user input** (which can contain unknown characters), POST is more robust and secure than GET.
