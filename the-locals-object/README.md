# ![EJS - The Context Object](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be understand how to pass data into a template. 

## The Locals Object

When we call `res.render()`, we can also include an optional object as an argument: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', {})
})
```

This object is the locals object, and it's properties define local variables for the view being rendered. 

> The locals object is how we get data into the template. Anything we put into this object will be available for us in the rendered view. 

For example, if we add the following: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { msg: 'This is a message' })
})
```

We can now access the `msg` property within `home.ejs`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Home</title>
</head>
<body>
  <h1>We are rendering a page!</h1>
  <p><%= msg %></p> 
</body>
</html>
```

[tktk ss]

The locals object is just a regular object, as such it can hold any type of data. Let's pass an example array of objects, representing an inventory of fruit.

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { 
    msg: 'This is a message',
    inventory: [
      {name: 'Banana', qty: 4},
      {name: 'Apple', qty: 10},
      {name: 'Orange', qty: 3},
      {name: 'Pineapple', qty: 0}
    ]
  })
})
```





