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
```
app.set("view engine", "ejs");
app.set("views", "views");
```
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%= title %></title>
    <link rel="stylesheet" href="/css/main.css" />
  </head>
  <body>
    <header class="main-header">
      <nav class="main-header__nav">
        <ul class="main-header__item-list">
          <li class="main-header__item"><a class="active" href="/">Shop</a></li>
          <li class="main-header__item">
            <a href="/admin/add-product">Add Product</a>
          </li>
        </ul>
      </nav>
    </header>

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
