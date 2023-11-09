# ![EJS - Fundamentals](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to define and use EJS.

## What is EJS?

EJS is a templating language that lets you generate HTML markup with plain JavaScript.

It does this through the use of template tags, which wrap JavaScript code in an HTML document. 

Notably, it complies with the Express view system, and as a result it is a popular choice when working with an Express app.

## Installing EJS

To install the EJS view engine package, use the following command: 

```bash
npm i ejs
```

EJS and other view engines are special - we don’t need to import them - `Express` knows how to find them all on its own.

## Using EJS to render .ejs files

`Express` applications automatically look inside of a `views` directory for template files, so we will put our view templates inside a `views` folder:

```bash
mkdir views
touch views/home.ejs
```
`.ejs` is the file extension for the EJS view engine.

In `server.js`, we're currently using `res.send()` to send an HTTP response. In order to use our new EJS file, we want to instead have `Express` render an entire view. 

To do so, we'll use `res.render()` instead of `res.send()`.

`res.render()` takes a `view` argument, which will be the file path of the view to render:

```javascript
app.get('/', (req, res) => {
  res.render('home.ejs')
})
```

 As mentioned earlier, Express will automatically look in the `views` directory, so `home.ejs` is sufficient for the template to be located correctly. 


Finally, inside `home.ejs`, add the following HTML: 

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

Run the server, and you should see 'We are rendering a page!' 