# ![EJS - The Locals Object](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will understand how to pass data into EJS templates using the locals object. 

## Passing Data into templates

When using `res.render()` in Express, an optional object, known as the *locals object*, can be included. This object defines local variables for the view being rendered. The structure of the locals object is simple: the key is the variable's name in the EJS file, and the value is what that variable will hold.

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', {})
})
```

> The locals object is how we get data into the template. Anything we put into this object will be available for us in the rendered view. 

Any data included in the locals object becomes available in your EJS template. 

For example:

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { msg: 'Welcome to the page!' })
})
```

## Using data in views

We can now access the `msg` variable within `home.ejs`:

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

### Handling complex data structures

The locals object is versatile and can handle different data types, including arrays and objects. Let's pass an example array of objects, representing an inventory of fruit.

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { 
    msg: 'Our Fruit Inventory',
    inventory: [
      { name: 'Banana', qty: 4 },
      { name: 'Apple', qty: 10 },
      { name: 'Orange', qty: 3 },
      { name: 'Pineapple', qty: 0 }
    ]
  })
})
```

In your EJS file, loop through the inventory array to display each fruit item:

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
  <ul>
    <% inventory.forEach(fruit => { %>
      <li><%= fruit.name %>: <%= fruit.qty %></li>
    <% }) %>
  </ul>
</body>
</html>
```

> 💡 Remember, the locals object is a powerful way to pass dynamic data to your EJS templates. It's a simple yet effective method to create interactive and personalized web pages.
