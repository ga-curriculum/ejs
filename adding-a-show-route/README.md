# ![EJS - Adding a Show Route](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to create a 'show' route in an Express application using EJS to display details of individual items from a data list.

## Show Route

Next, we'll add a show route to our app. The end goal is for each of the `li`'s in our fruit list become clickable links that take us to a page with information about the specific fruit we clicked on. This is typically referred to as a `show` page. 

We'll begin by organizing our data and setting up our show route. This route will enable users to view details of specific items by clicking on them in a list.

**Organizing Data:**

In `server.js`, move the array of fruit objects from the route handler to a global variable called `inventory` . This makes the data accessible to other route functions as well:

```js
const express = require('express')
const app = express()

// add the following: 
const inventory =  [
  {name: 'Banana', qty: 4},
  {name: 'Apple', qty: 10},
  {name: 'Orange', qty: 3},
  {name: 'Pineapple', qty: 0}
]

app.get('/', (req, res) => {
  res.render('home.ejs', { 
    msg: 'This is a message',
    // change the following line to: 
    inventory: inventory,
  })
})

app.listen(3000, () => {
  console.log('Listening on port 3000')
})
```
> Nothing has changed in terms of functionality, but now other functions can also access the data held in `inventory`. 


**Updating home.ejs:**

Next, in `home.ejs`, modify the list items to be clickable links, each directing to a unique route based on the item's index.

```html
<h1>We are rendering a page!</h1>
<p><%= msg %></p>
<ul>
  <!-- Add the index parameter -->
  <% inventory.forEach((fruit, index)=>{ %>
    <!-- Wrap each li in an a tag -->
    <a href="/<%= index %>">
      <li><%= fruit.name %>: <%= fruit.qty %></li>
    </a>
  <% }) %>
</ul>
```

### Establishing the `show`  route

At the moment, these links will all throw errors. This is because we have not established a route for them yet! 

Create a new route in `server.js` that listens for requests to `/:fruitId` and logs the `req.params` object.

```js
app.get('/:fruitId', (req, res) => {
  console.log(req.params)
})
```

For now, all this route will do is listen for a request and then `console.log` the attached `req.params`. Click on a few of the links in the browser, and examine your terminal. You should see that `req.params` is an object that looks something like `{ fruitId: 1 }`, where `1` will be replaced with the index of the item you clicked on. 

### Rendering the `show` page

Next, our goal is to ensure that when a user clicks on an item in our list, our application will display a page specifically dedicated to that item. This page will show detailed information about the item clicked. To achieve this, we first need to create a new EJS template file.

Create a new EJS file named `show.ejs` in the `views` directory:

```bash
touch views/show.ejs
```

Add HTML content to `show.ejs`, making use of the fruit object to display specific details.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= fruit.name %></title>
</head>
<body>
  <h1>This is a page about <%= fruit.name %>s</h1>
  <p>There are <%= fruit.qty %> left.</p>
</body>
</html>
```

> At this point `fruit` is undefined, but we'll address that in the next step. 

### Pass data to `show` page

We saw in an earlier example that `req.params` holds the index value of whichever index object was clicked on. Let's make a new variable called `index` and set it equal to the value passed to us by the `:fruitId` parameter. 

Modify the `/:fruitId` route to render `show.ejs` with the corresponding *fruit data* based on the clicked item's `index`.

```js
app.get('/:fruitId', (req, res) => {
  const index = req.params.fruitId
  // render show.ejs, and pass it a fruit object 
  res.render('show.ejs', { fruit: inventory[index] })
})
```

Because the list on our index page is generated from the `inventory` array, we can safely predict the order of ours link will be identical to the order of our objects. If we click `Banana`, the first element in our `inventory`, we expect `fruitId` to equal 0.

> Note: In real-world applications, we'd use more sophisticated methods to retrieve data rather than relying on array indices. However, for demonstration purposes in this small-scale example, using the index is sufficient.
