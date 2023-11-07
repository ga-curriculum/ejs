# ![EJS - Syntax](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to tktk

## EJS syntax

EJS uses [a variety of tags](https://ejs.co/#docs) to embed JavaScript code directly into a template.

## Scriptlet Tag
`<%`

This tag is for executing JavaScript, such as control-flow. This tag produces no output. 

```html
<% if(true) { %>
  <p> This shows up! </p>
<% } else { %>
  <p> Something else! </p>
<% } %>
```

Note that each line of JavaScript code needs its own pair of scriptlet tags. Trying to wrap an entire multiline statement in a single scriptlet tag will cause errors: 

```javascript
// Don't do this!
<% if(true) {
  <p> This shows up! </p>
} else {
  <p> Something else! </p>
} %>
```


## Outlet Tag
`<%=`

This tag is for writing JavaScript expressions into the HTML page. It will output the value into the template. 

```html 
<p> <%= 'this will be capitalized'.toUpperCase() %> </p>
```


Note that the closing tag for both tags is the same: `%>` 

