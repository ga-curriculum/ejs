# ![EJS - Level Up - Partial Templates](./assets/hero.png)

## Partial Templates

EJS includes the ability to make our views more DRY by using partial templates. 

The <%- %> EJS tags are for outputting HTML





```html
<%- include('./partials/html-head') %>
<%- include('./partials/nav') %>

<main>
  <h1><%= title %></h1>
</main>

<%- include('./partials/footer') %>
```
