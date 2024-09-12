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
import express from "express";
import path from "path";
import { adminRouter } from "./routes/admin";
import shopRoutes from "./routes/shop";

const app = express();
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static(path.join(__dirname, "public")));

app.set("view engine", "ejs");

app.use("/admin", adminRouter);
app.use(shopRoutes);

app.use((req, res, next) => {
  res.render("404", { title: "Page not found", path: "/404" });
});

app.listen(3000);
```

views/includes/head.ejs
```
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title><%= title %></title>
  <link rel="stylesheet" href="/css/main.css" />
</head>
```

views/includes/navigation.ejs
```
<header class="main-header">
  <nav class="main-header__nav">
    <ul class="main-header__item-list">
      <li class="main-header__item">
        <a class="<%= path === '/' ? 'active' : '' %>" href="/">Shop</a>
      </li>
      <li class="main-header__item">
        <a
          class="<%= path === '/admin/add-product' ? 'active' : '' %>"
          href="/admin/add-product"
          >Add Product</a
        >
      </li>
    </ul>
  </nav>
</header>
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
