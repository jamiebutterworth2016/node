`npm i --save sql2 sequelize`  
`npm i --save-dev @types/sequelize`

util/database.ts
```
import { DataTypes, Sequelize } from "sequelize";
import Product from "../models/product";

const sequelize = new Sequelize("node-complete", "root", "pass", {
  dialect: "mysql",
});

Product.init(
    {
      id: {
        type: DataTypes.INTEGER.UNSIGNED,
        autoIncrement: true,
        allowNull: false,
        primaryKey: true,
      },
      title: DataTypes.STRING(255),
      price: {
        type: DataTypes.DOUBLE,
        allowNull: false,
      },
      imageUrl: {
        type: DataTypes.STRING(255),
        allowNull: false,
      },
      description: {
        type: DataTypes.STRING(255),
        allowNull: false,
      },
    },
    { tableName: "products", sequelize }
  );

export default sequelize;
```

models/product.ts
```
import { Model } from "sequelize";

export default class Product extends Model {
  declare id: number;
  declare title: string;
  declare price: number;
  declare imageUrl: string;
  declare description: string;
}
```

app.ts
```
import express from "express";
import path from "path";
import adminRoutes from "./routes/admin";
import shopRoutes from "./routes/shop";
import pageNotFound from "./controllers/error";
import sequelize from "./util/database";

const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static(path.join(__dirname, "public")));

app.set("view engine", "ejs");

app.use("/admin", adminRoutes);
app.use(shopRoutes);

app.use(pageNotFound);

sequelize
  .sync()
  .then(() => app.listen(3000))
  .catch((err) => console.log(err));
```
