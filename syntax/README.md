<h1>
  <span class="headline">EJS</span>
  <span class="subhead">Syntax</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to effectively utilize EJS syntax to integrate JavaScript logic and expressions within HTML templates.

## EJS syntax

There are a variety of [EJS tags](https://ejs.co/#docs) to embed JavaScript code directly into a template. The two primary tags you'll use are the ***Scriptlet*** and ***Output*** tags.

## Scriptlet tag

The scriptlet tag `<%  %>` executes JavaScript code within an EJS file. Any code written between these tags is treated as regular JavaScript. This code won't directly produce any visible output in the HTML.

This tag helps add control flow logic (like `if`, `else`, and loops) to your templates.

### Using the scriptlet tag

To use the scriptlet tag, write JavaScript logic between `<%` and `%>`

```html
<% if(true) { %>
  <p>This shows up!</p>
<% } else { %>
  <p>Something else!</p>
<% } %>
```

As you can see from this example, each line of JavaScript or block should be enclosed within scriptlet tags. Don't wrap multiple lines of code in a single set of scriptlet tags, as shown below. This will lead to errors.

```html
<!-- Don't do this! -->

<% if(true) {
  <p>This shows up!</p>
} else {
  <p>Something else!</p>
} %>
```

> 🧠 It's not uncommon for developers to develop playful nicknames for various elements like scriptlet and output tags. Here are a few of our favorites: *Magic Sandwiches, Noodle Brackets, Wizard Hats, Mustache Brackets, Squids*

## Output tag

The output tag `<%=  %>` allows you to display the results of JavaScript expressions directly in your HTML.

You'll primarily use this tag to insert dynamic data into your HTML. Use it to display variables, calculations, or anything that resolves to a single value.

### Using the output tag

To use this tag, write your JavaScript expression between `<%=` and `%>`. Note that if you write the following code and refresh the page, you'll receive an error, but as an example:

```html
<p>Welcome, <%= player.name %></p>
```

The output tag is ideal for accessing object properties, as shown above, or simple expressions like arithmetic operations. Test it out:

```html
<p>2 plus 2 is <%= 2 + 2 %></p>
```

This will display `2 plus 2 is 4` in the paragraph.

Note that the closing tag for both tags (and every other tag) is the same: `%>` (there are a couple of alternatives, but you're unlikely to encounter them often).

> 💡 Best Practice: Keep complex logic out of your templates to make them easier to understand. Complex logic is better handled in your back-end scripts.

## 🎓 You Do

Let's add a few new code snippets in `home.ejs` to test drive this new tag syntax.

### Use conditional rendering

1. Create a JavaScript variable using the scriptlet tag `<%`.

   ```html
   <% let showMessage = true; %>
   ```

2. Below it, implement an `if` statement to render a paragraph (`<p>This is a dynamic message!</p>`) element only if showMessage is true.

3. Change the `boolean` value to `false` and refresh the page.

### Incorporate the output tag

1. Create a JavaScript variable that holds a number.

   ```html
   <% let favoriteNumber = 7; %>
   ```

2. Below it, use the output tag `<%=` to display this number within a `<p>` in your HTML so that this text is shown when you visit the page in the browser:

   ```plaintext
   My favorite number is 7.
   ```
