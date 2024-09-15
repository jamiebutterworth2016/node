`npm i --save mysql2`  
`mkdir util`  
`echo > util/database.ts`  

database.ts
```
import mysql from "mysql2";

const pool = mysql.createPool({
  host: "localhost",
  user: "root",
  database: "node-complete",
  password: "pass",
});

export default pool.promise();
```

app.ts
```
import express from "express";
import path from "path";
import adminRoutes from "./routes/admin";
import shopRoutes from "./routes/shop";
import pageNotFound from "./controllers/error";
import database from "./util/database";

const app = express();

database
  .execute("SELECT * FROM products")
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  });

app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static(path.join(__dirname, "public")));

app.set("view engine", "ejs");

app.use("/admin", adminRoutes);
app.use(shopRoutes);

app.use(pageNotFound);

app.listen(3000);
```
