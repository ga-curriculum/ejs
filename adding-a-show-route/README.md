<h1>
  <span class="headline">EJS</span>
  <span class="subhead">Adding a Show Route</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to create a show route in an Express application using EJS to display details of individual items from a data list.

## Show route

Next, we'll add a show route to our app. The end goal is for each of the `<li>`'s in our inventory list to become clickable links that take us to a page with information about the specific item we clicked on. This is typically referred to as a `show` page.

We'll begin by organizing our data and setting up our show route. This route will enable users to view details of specific items by clicking on them in a list.

## Organizing data

In `server.js`, move the `inventory` array from the route handler to a global variable called `inventory`. This makes the data accessible to other route functions:

```js
// server.js

const express = require('express');
const app = express();

// add the following:
const inventory = [
  { name: 'Candle', qty: 4 },
  { name: 'Cheese', qty: 10 },
  { name: 'Phone', qty: 1 },
  { name: 'Tent', qty: 0 },
  { name: 'Torch', qty: 5 }
]

app.get('/', (req, res) => {
  res.render('home.ejs', { 
    msg: 'Here is your inventory',
    player: {
      name: "friend"
    },
    // change the following line to: 
    inventory: inventory,
  });
});

app.listen(3000, () => {
  console.log('Listening on port 3000');
});
```

> 💡 Nothing has changed in terms of functionality; you can refresh the home page, and everything is the same as before. However, now other functions can also access the data held in `inventory`!

## Updating `home.ejs`

Next, in `home.ejs`, modify the list items to be clickable links, each directing to a unique route based on the item's index.

```html
<!-- views/home.ejs -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Home</title>
</head>
<body>
  <h1>We are rendering a page!</h1>
  <p><%= msg %>, <%= player.name %>!</p> 
  <ul>
    <!-- Add the index parameter -->
    <% inventory.forEach((item, index) => { %>
      <!-- Wrap each li in an <a> tag -->
      <a href="/<%= index %>">
        <li><%= item.name %>: <%= item.qty %></li>
      </a>
    <% }); %>
  </ul>
</body>
</html>
```

## Establishing the `show` route

At the moment, these links will all throw errors. This is because we have not established a route for them yet!

Create a new route in `server.js` that listens for requests to `/:itemId` and logs the `req.params` object.

```js
// server.js

app.get('/:itemId', (req, res) => {
  console.log(req.params);
});
```

For now, all this route will do is listen for a request and then `console.log` the attached `req.params`. Click on a few of the links in the browser and examine your terminal. You should see that `req.params` is an object that looks something like `{ itemId: 1 }`, where `1` will be replaced with the index of the item you clicked on.

### Pass data to `show` page

So we've established that `req.params.itemId` holds the index value of whichever index object was clicked on. Let's make a new variable called `index` and set it equal to that.

Modify the `/:itemId` route to render a `show.ejs` page with the corresponding ***item data*** based on the clicked item's `index`. Note that we haven't created this `show.ejs` page yet, but we will soon.

```js
// server.js

app.get('/:itemId', (req, res) => {
  const index = req.params.itemId;
  // render show.ejs, and pass it a single item object 
  res.render('show.ejs', {
    item: inventory[index]
  });
});
```

Because the list on our index page is generated from the `inventory` array, we can safely predict the order of the links will be identical to the order of objects in the array. If we click **Candle** - the first element in our `inventory` - we expect `req.params.itemId` to equal `0`.

> Note: In real-world applications, we'd use more sophisticated methods to retrieve data rather than relying on array indices. However, using the index is sufficient for demonstration purposes in this small-scale example.

## Rendering the `show` page

Next, our goal is to ensure that when a user clicks on an item in our list, our application will display a page specifically dedicated to that item. This page will show detailed information about the item clicked.

To achieve this, we first need to create a new EJS template file. Create a new EJS file named `show.ejs` in the `views` directory:

```bash
touch views/show.ejs
```

Add HTML content to `show.ejs`, making use of the `item` object to display specific details.

```html
<!-- views/show.ejs -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= item.name %></title>
</head>
<body>
  <h1>Welcome to the <%= item.name %> page!</h1>
  <p>There are <%= item.qty %> left.</p>
</body>
</html>
```
