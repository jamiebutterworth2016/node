# Views
`mkdir views`\
`echo > views/view.html`\
`html5`

app.js
```
import express from "express";
import path from "path";

const app = express();

app.get("/", (req, res) => {
  res.sendFile(path.join(__dirname, "views", "home.html"));
});

app.listen(3000);
```

# Styles
`mkdir public/css`\
`echo > public/css/main.css`

app.ts
```
app.use(express.static(path.join(__dirname, 'public')));
```

main.css
```
body {
  font-family: sans-serif;
}
```
Add link to views
```
<link rel="stylesheet" href="/css/main.css">
```

# Routes
`mkdir routes`
