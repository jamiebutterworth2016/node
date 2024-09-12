# Pug
app.ts
```
app.set("view engine", "pug");
```

# Handlebars
`npm i --save express-handlebars@3.0`
`npm i --save-dev @types/express-handlebars`

app.ts
```
import engine from "express-handlebars";

app.engine(
  "hbs",
  engine({
    layoutsDir: "views/layouts",
    defaultLayout: "main-layout",
    extname: "hbs",
  })
);
app.set("view engine", "hbs");
```

`echo > views/404.hbs`  
`echo > views/layouts/main-layout.hbs`

# EJS (Embedded JavaScript templates)
Can mix JS with HTML.  
app.ts
```
app.set("view engine", "ejs");
app.set("views", "views");
```

views/includes/navigation.ejs
```
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title><%= title %></title>
  <link rel="stylesheet" href="/css/main.css" />
</head>
```

views/shop.ejs
```
<!DOCTYPE html>
<html lang="en">
  <%- include('includes/head.ejs') %>
  <body>
    <%- include('includes/navigation.ejs') %>
    <main>
      <% if (prods.length > 0) { %>
      <div class="grid">
        <% for (product of prods) { %>

        <article class="card product-item">
          <header class="card__header">
            <h1 class="product__title"><%= product.title %></h1>
          </header>
          <div class="card__image">
            <img src="" alt="" />
          </div>
          <div class="card__content">
            <h2 class="product__price">$19.99</h2>
            <p class="product__description">A very interesting book.</p>
          </div>
        </article>
        <% } %>
      </div>
      <% } else { %>
      <h1>No products.</h1>
      <% } %>
    </main>
  </body>
</html>
```
