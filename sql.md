# MySQL Database
Moving away from fs and path. Executing queries - way fewer lines of code than reading from file.

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

product.ts
```
import database from "../util/database";
import { RowDataPacket } from "mysql2";

class Product {
  id: string;
  title: string;
  imageUrl: string;
  description: string;
  price: number;

  constructor(
    id: string,
    title: string,
    imageUrl: string,
    description: string,
    price: number
  ) {
    this.id = id;
    this.title = title;
    this.imageUrl = imageUrl;
    this.description = description;
    this.price = price;
  }

  async save(): Promise<void> {
    await database.execute(
      `INSERT INTO product (title, imageUrl, description, price) VALUES (?, ?, ?, ?)`,
      [this.title, this.imageUrl, this.description, this.price]
    );
  }

  static async deleteById(id: string): Promise<void> {
    await database.execute(`DELETE * FROM products WHERE id = ${id}`);
  }

  static async fetchAll(): Promise<Product[]> {
    const [rows] = await database.execute<RowDataPacket[]>(
      "SELECT * FROM products"
    );
    const products = rows.map(
      (row: any) =>
        new Product(row.id, row.title, row.imageUrl, row.description, row.price)
    );
    return products;
  }

  static async findById(productId: string): Promise<Product | undefined> {
    const [rows] = await database.execute<RowDataPacket[]>(
      `SELECT * FROM products WHERE id = ?`,
      [productId]
    );

    if (!rows.length) return undefined;

    const row = rows[0];

    return new Product(
      row.id,
      row.title,
      row.imageUrl,
      row.description,
      row.price
    );
  }
}

export { Product };
```
