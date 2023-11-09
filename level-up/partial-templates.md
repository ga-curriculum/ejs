# ![EJS - Level Up - Partial Templates](./assets/hero.png)

## Partial Templates

Picture that you have an app with 10 different views. Then, 
imagine that you have a nav bar that you want to include at the top of each view. You __could__ manually copy and paste the same HTML code at the top of each view, which would lead to the same nav across multiple pages. 

But then imagine that you need to add a new link to the nav. You would have to go through and manually update the HTML for across all ten views. 

Fortunately, EJS includes the ability to make our views more DRY by using partial templates! 

The <%- %> EJS tags allow us to output HTML, meaning we can directly inject HTML code from other files into our views. 

To use a partial template in a view, we use the following `include` syntax: 

```html
<%- include('filename') %>
```

## Creating partial templates

Let's implement some partial templates in our existing code.

```bash
mkdir views/partials
touch views/partials/html-head.ejs
touch views/partials/nav.ejs
```

Our HTML boilerplate is the same in every view. Since this is the case, it makes sense to create a partial for the HTML head: 

In `partials/html-head.ejs`, add the following: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= title %></title>
</head>
```

> 🧠  Note that we don't close the `html` tag - that's ok, because it will be closed in the HTML file that this is imported into. 


The only value that will be unique view to view is the `title`, so as long as we supply a title in the context object of each view we render, we can convert all of our boilerplate to use this partial template!

Let's address that quickly - in `server.js`: 

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs', { 
    // add a title property: 
    title: 'Home Page',
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

Next, in `partials/nav.ejs`, add the following: 

```html
<body>
  <nav>
    <a href="/link-one"> Example Link 1 </a>
    <a href="/link-two"> Example Link 2 </a>
    <a href="/link-three"> Example Link 3 </a>
  </nav>
```

With these partials created, we can refactor `home.ejs`.

Our updated code will look like this: 

```html
<%- include('./partials/html-head') %>
<%- include('./partials/nav') %>

    <h1>We are rendering a page!</h1>
    <p><%= msg %></p>
    <ul>
      <% inventory.forEach((item) => { %>
        <li> <%= item.name %> - <%= item.qty %> </li>
      <% }) %>
    </ul>
  <body>
</html>
```

