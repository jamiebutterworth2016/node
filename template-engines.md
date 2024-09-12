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

# EJS
```
app.set("view engine", "ejs");
app.set("views", "views");
```
