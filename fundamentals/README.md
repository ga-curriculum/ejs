# ![EJS - Fundamentals](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

## What is EJS?

A view engine is a library that works in conjunction with a web app framework that handles the process of generating dynamic HTML content from templates and data. The view engine is responsible for rendering the final output (HTML code) to be sent to the client. 

EJS is a type of view engine that can generate dynamic HTML content by embedding JavaScript code within HTML templates.






## Installing EJS

To install the EJS view engine package: 

```bash
npm i ejs
```

EJS and other view engines are special - we don’t need to import them - Express knows how to find them all on its own.

## Using EJS to render .ejs files

Express applications are usually architected using the MVC design pattern, so we will put all view templates inside a views folder:

```bash
mkdir views
touch views/home.ejs
```

`.ejs` is the file extension for the EJS view engine.

