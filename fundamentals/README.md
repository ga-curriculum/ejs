<h1>
  <span class="headline">EJS</span>
  <span class="subhead">Fundamentals</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to render EJS view files from an express server to the browser.

## Getting started with EJS `views`

In the context of EJS (Embedded JavaScript) and web development, ***views*** are template files that contain a mix of HTML and JavaScript. These files are used to generate HTML content dynamically.

Let's add EJS to our application and explore it!

### Installing EJS

To add EJS to your project, you need to install it using `npm`:

```bash
npm i ejs
```

> 🧠 EJS and other view engines are unique - we don't need to require them in `server.js` to use them - Express knows how to find them all on its own.

## Organizing `.ejs` files

In Express applications, there's a convention for organizing your EJS templates. Express automatically searches for these templates in a specific folder named `views`. Store all your EJS template files in this directory and its subdirectories to keep things organized and functioning correctly.

> ♻️ **Repeatable pattern**: If you're using a template engine, such as EJS, in Express, the views you create will always go inside a `views` directory at the root of your project.

1. First, create a new directory named `views` in your project. This is where all your `.ejs` files will live:

   ```bash
   mkdir views
   ```

2. Next, create your first EJS template file. Let's name it `home.ejs`. This file will serve as the template for your homepage.

   ```bash
   touch views/home.ejs
   ```

   > ♻️ **Repeatable pattern**: EJS files will always have a `.ejs` extension.

3. Finally, inside `home.ejs`, add some HTML boilerplate by hitting `!` followed by pressing the `Tab` key.

   Change the `<title>` to hold the text `Home`. Inside the body, add an `<h1>` with the text content `We are rendering an EJS page!` - here is the result:

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
     <h1>We are rendering an EJS page!</h1>
   </body>
   </html>
   ```

Awesome, we've created our first `.ejs` file! How do we see it though?

## EJS rendering in Express

When working with Express and EJS, we transition from using `res.send()` to send plain text responses to using `res.render()` to display complete HTML pages created with EJS templates.

1. Open `server.js` and take a look at the example route. Here, we used `res.send()` to send back responses.

   ```js
   // server.js

   app.get('/', (req, res) => {
     res.send('The server is running!');
   });
   ```

2. To render EJS, we'll replace `res.send()` with `res.render()`. This informs Express to generate a full HTML page using an EJS template and then respond to the client with the generated template.

   The `res.render()` function requires one argument - the name of the EJS file or *view* you want to use. For example, we can render our template file named `home.ejs` located in the views directory:

   ```js
   // server.js

   app.get('/', (req, res) => {
     res.render('home.ejs');
   });
   ```

   > 🧠 `res.render('home.ejs')` instructs Express to look for `home.ejs` in the `views` directory and use it to create the HTML response. We don't need to include the `views` directory here because Express knows to look inside that directory to find templates to render automatically.

Refresh your browser, and you should see a header reading: **We are rendering an EJS page!**
