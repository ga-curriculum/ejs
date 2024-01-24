# ![EJS - Syntax](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to effectively utilize EJS syntax to integrate JavaScript logic and expressions within HTML templates. 

## EJS syntax

EJS allows you to write regular HTML and specify where you want to include dynamic data. Think of it like making a fill-in-the-blanks template for a web page. You write the usual HTML, but leave spaces ('blanks') where you want data to appear. These spaces are marked using EJS's special syntax.

There are a variety of [EJS tags](https://ejs.co/#docs) to embed JavaScript code directly into a template. The two primary tags you'll use are the ***Scriptlet*** and ***Output*** tags.

## Scriptlet Tag `<%  %>`

EJS templates allow you to write JavaScript code directly within your HTML pages. One of the key tools for this is the *scriptlet* tag, represented as `<% ... %>`. 

- The scriptlet tag `<%` is used to execute JavaScript code within an EJS file. Any code you write between these tags is treated as regular JavaScript. 

- This tag is particularly useful for adding control flow logic (like `if`, `else`, `for` loops) to your templates. It allows you to dynamically display content based on certain conditions.

### How to use it

**Embedding Logic**

To use the scriptlet tag, simply wrap your JavaScript logic between `<%` and `%>`. This code won't directly produce any visible output in the HTML but will control the flow of how the HTML is rendered.

**Example:** 

```html
<% if(true) { %>
  <p> This shows up! </p>
<% } else { %>
  <p> Something else! </p>
<% } %>
```

**Multiline JavaScript**

Each JavaScript statement or block should be enclosed within its own scriptlet tags. Avoid trying to wrap multiple lines of code in a single set of scriptlet tags, as it can lead to errors.

**Bad example:**

```html
// Don't do this!
<% if(true) {
  <p> This shows up! </p>
} else {
  <p> Something else! </p>
} %>
```


## Output Tag `<%=  %>`

The *Output* tag allows you to display the results of JavaScript expressions directly in your HTML. 

### How to use it

To use this tag, write your JavaScript expression between `<%= ... %>`. The result of this expression will be output where the tag is placed in the HTML.

You can use the output Tag to dynamically insert data into your HTML. It's especially useful for displaying variables, calculations, or any dynamic content.

**Example**:


```html 
<p> Welcome, <%= user.name %> </p>
```

The output tag is ideal for simple expressions like arithmetic operations or accessing object properties.

**Test this out**:

```html
<p> 2 plus 2 is <%= 2 + 2 %> </p>
```

This will display "2 plus 2 is 4" in the paragraph.

Note that the closing tag for both tags is the same: `%>` 

> 💡 Best Practice: Try to keep complex logic out of your templates to make them easier to understand. Complex logic is better handled in your backend scripts.

> 🧠 It's not uncommon for developers to come up with playful  nicknames for various elements like scriptlet and output tags. Here are a few of our favorites: *Magic Sandwiches, Noodle Brackets, Wizard Hats, Mustache Brackets, Squids*


## 🎓 You Do 

Lets add a few new code snippets in `home.ejs` to test drive this new tag syntax.

**Use Conditional Rendering:** 

1. Create a JavaScript variable using the scriptlet tag `<%`. 

```html
<% let showMessage = true; %>
```

2. Below it, implement an `if` statement to render a paragraph (`<p>This is a dynamic message!</p>`) element only if showMessage is true.

3. Change the `boolean` value  to false and refresh the page. 

**Incorporate the Output Tag:** 

1. Create a JavaScript variable that holds a number. 

```html
<% let favoriteNumber = 7; %>
```

2. Below it, use the output tag `<%=` to display this number within a `<p>` in your HTML. 

```
"My favorite number is 7"
```