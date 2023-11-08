# ![EJS - The Context Object](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

## The Context Object / Locals Object

When we call `res.render()`, we can also include an optional context object as an argument: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', {})
})
```

This object's properties define local variables for the view.

> The context object is how we get data into the template.

For example, if we add the following: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { msg: 'This is a message' })
})
```

We can now access `title` within `home.ejs`:

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

The context object is just a regular object, as such it can hold any type of data: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { 
    msg: 'This is a message',
    totalSales: 5000,
    inventory: [
      {name: 'Banana', qty: 4},
      {name: 'Apple', qty: 10},
      {name: 'Orange', qty: 3},
      {name: 'Pineapple', qty: 0}
    ]
  })
})
```






