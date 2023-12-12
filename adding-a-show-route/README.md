# ![EJS - Adding a Show Route](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be understand how to create a show route for a list of data.

## Show Route

Next, we'll add a show route to our app. The goal is to have each of the `li`'s in our `home.ejs` view be clickable links that will take us to a page with information about the specific object we clicked on. This is typically referred to as a `show` page. 

In `server.js`, we'll move our array of fruit objects out of `app.get()` and assign it to a variable named `inventory`. In the context object of our route, we'll assign this new `inventory` variable as the value:

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

Nothing has changed in terms of functionality, but now other functions can also access the data held in `inventory`. 

Underneath our first route in `server.js`, add a new route: 

```js
app.get('/:fruitId', (req, res) => {
  console.log(req.params)
})
```

For now, all this route will do is listen for a request and then console.log the attached `req.params`. Click on a few of the links in the browser, and examine your server terminal. You should see that `req.params` is an object that looks something like `{ fruitId: 1 }`, where `1` will be replaced with whatever the index of the link you clicked was. 

Next, we want to make it so that whenever a user hits the route above by clicking on an object's name in the list, we render a template page with the data from that specific object. 

For that, we'll first need a new `ejs` file. In your `views` directory, make a new file named `show.ejs`: 

```bash
touch views/show.ejs
```

In `show.ejs`, add the following: 

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

`fruit` is still undefined, but we'll address that in the next step. 

We saw in an earlier example that `req.params` holds the index value of whichever index object was clicked on. Let's make a new variable called `index` and set it equal to the value passed to us by the `:fruitId` parameter. 

```js
app.get('/:fruitId', (req, res) => {
  const index = req.params.fruitId
  // render show.ejs, and pass it a fruit object 
  // based on the index the user clicked on: 
  res.render('show.ejs', {
    fruit: inventory[index]
  })
})
```

Because the list on our index page is generated from the `inventory` array, we can safely predict the order of ours link will be identical to the order of our objects. If we click `Banana`, the first element in our `inventory`, we expect `fruitId` to equal 0. If we click `Pineapple`, we expect `fruitId` to equal 3. We can in turn use this number to identify which link was clicked on. If a user clicks on `Pineapple`, the number 3 can be used to access the object at index 3 in `inventory`. 

Once we start working with external servers, we'll use more sophisticated or accurate methods to find the data than an index. For a small scale example, using the index of the object in our data array works fine to demonstrate the relationship between the "front-end" and "back-end" in our app. 




