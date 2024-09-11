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

app.engine("hbs", engine({}));
app.set("view engine", "hbs");
```

`echo > views/404.hbs`
