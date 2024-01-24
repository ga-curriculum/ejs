# ![EJS - Fundamentals](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to render EJS view files from an express server to the browser.

## Getting started with EJS `views`

In the context of EJS (Embedded JavaScript) and web development, "views" are template files that contain a mix of HTML and JavaScript. These files are used to generate HTML content dynamically. 

Let's add EJS to our application and explore! 

### Installing EJS

To add EJS to your project, you need to install it using `npm`:

```bash
npm i ejs
```

> EJS and other view engines are special - we don’t need to import them in `server.js` to use them - Express knows how to find them all on its own.

### Organizing `.ejs` files

In Express applications, there's a convention for organizing your EJS templates. Express automatically searches for these templates in a specific folder named `views`. So, to keep things organized and functioning correctly, you should store all your EJS template files in this folder.

1. First, create a new directory named `views` in your project. This is where all your `.ejs` files will live: 

  ```bash
  mkdir views
  ```

2. Next, create your first EJS template file. Let's name it `home.ejs`. This file will serve as the template for your homepage.

  ```bash
  touch views/home.ejs
  ```

3. Finally, inside `home.ejs`, add the following HTML: 

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
</body>
</html>
```

> Files for EJS swill always have the `.ejs` extension, even though their contents look like HTML. This extension tells Express that these are template files.

### EJS rendering in Express 

When working with Express and EJS, we transition from using `res.send()` for sending plain text responses to using `res.render()` for displaying complete HTML pages created with EJS templates.

1. Open server.js and take a look at the example route. Previously, we might have used `res.send()` to send back responses.

```js
app.get('/', (req, res) => {
  res.send('Server is running')
})
```

2. Now, we'll replace `res.send()` with `res.render()` to tell Express to generate a full HTML page using an EJS template.

    The `res.render()` function requires one argument - the name of the EJS file or *view* you want to use. For example, we can render our template file named `home.ejs` located in the views directory:

  ```js
  app.get('/', (req, res) => {
    res.render('home.ejs')
  })
  ```

  > Here, `res.render('home.ejs')` instructs Express to look for `home.ejs` in the `views` folder and use it to create the HTML response.


Refresh your browser, and you should see *'We are rendering a page!'* 