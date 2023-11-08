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

Partial templates are just regular HTML. 

Take the following nav as an example: 

```html
<body>
  <nav>
    <a href="/link-one"> Example Link 1 </a>
    <a href="/link-two"> Example Link 2 </a>
    <a href="/link-three"> Example Link 3 </a>
  </nav>
```


Let's take this a step further. Our HTML boilerplate is also the same in every view. Since this is the case, we can also make a partial for the HTML head: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><%= title %></title>
</head>
```

The only value that will be unique view to view is the `title`, so as long as we supply a title in the context object of each view we render, we can convert all of our boilerplate to use this partial template. 

Our updated code will look like this: 

```html
<%- include('./partials/html-head') %>
<%- include('./partials/nav') %>

    <main>
      <h1>Content</h1>
    </main>
  <body>
</html>
```

