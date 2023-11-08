# ![EJS - Level Up - Partials](./assets/hero.png)

The <%- %> EJS tags are for outputting HTML

EJS Partial Templates are the best way to keep our views DRY.

EJS includes the ability to make our views more DRY by using partial views: 

```html
<%- include('./partials/html-head') %>
<%- include('./partials/nav') %>

<main>
  <h1><%= title %></h1>
</main>

<%- include('./partials/footer') %>
```
