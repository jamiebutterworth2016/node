# Controllers
`mkdir controllers`
`echo > controllers/products.ts`

admin.ts
```
import express from "express";
import { getAddProduct, addNewProduct } from "../controllers/products";

const adminRoutes = express.Router();

adminRoutes.get("/add-product", getAddProduct);
adminRoutes.post("/add-product", addNewProduct);

export default adminRoutes;
```

products.ts
```
import { Request, Response } from "express";

type Product = {
  title: string;
};

const products: Product[] = [];

const getAddProduct = (req: Request, res: Response) => {
  res.render("add-product", {
    title: "Add Product",
    path: "/admin/add-product",
  });
};

const addNewProduct = (req: Request, res: Response) => {
  products.push({ title: req.body.title });
  res.redirect("/");
};

const getProducts = (req: Request, res: Response) => {
  res.render("shop", {
    title: "Shop",
    prods: products,
    hasProducts: products.length > 0,
    path: "/",
    activeShop: true,
  });
};

export { getAddProduct, addNewProduct, getProducts };
```

# Models
`mkdir models`  
`echo > models/product.ts`
```
import { promises as fs } from "fs";
import path from "path";

const p = path.join(__dirname, "..", "data", "products.json");

class Product {
  title: string;

  constructor(title: string) {
    this.title = title;
  }

  async save(): Promise<void> {
    const file = await fs.readFile(p);

    let products: Product[] = [];

    products = JSON.parse(file.toString());
    products.push(this);

    await fs.writeFile(p, JSON.stringify(products));
  }

  static async fetchAll(): Promise<Product[]> {
    const file = await fs.readFile(p);
    return JSON.parse(file.toString());
  }
}

export { Product };
```
