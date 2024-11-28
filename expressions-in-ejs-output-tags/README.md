<h1>
  <span class="headline">EJS</span>
  <span class="subhead">Expressions in EJS Output Tags</span>
</h1>

**Learning objective:** By the end of this lesson, students will understand how to best utilize the EJS output tag with JavaScript expressions.

## Expressions vs. statements in JavaScript

Remember, we can only write JavaScript expressions inside the EJS output tags `<%= %>`. JavaScript expressions evaluate to a single value. They can be:

- Assigned to a variable
- Provided as an argument to a function
- Returned from a function
- Passed to a `console.log()`

Statements perform actions, and applications consist primarily of statements.

## Using conditional expressions

Let's examine the code for our show page:

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

We have a slight grammatical error when we visit this page if there is only one of an item left - you can see this for yourself if you visit the phone's show page:

```plaintext
There are 1 left.
```

This isn't great, but it's nothing some conditional logic can't fix using an expression. A ternary is an expression that resolves to a single value, so we can use that here:

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
  <p>There <%= item.qty === 1 ? "is" : "are" %> <%= item.qty %> left.</p>
</body>
</html>
```

If there is only one of an item the text `is` will be used. If there is any other amount, the text `are` will be used.

This means that when there is only one item, we use the correct grammar to describe it. Cool!

Most logic should typically be handled before data is passed to the view, but it's appropriate to handle smaller logic like this in a view.
