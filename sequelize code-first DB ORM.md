`npm i --save sql2 sequelize`  
`npm i --save-dev @types/sequelize`

util/database.ts
```
import { Sequelize } from "sequelize";

const sequelize = new Sequelize("node-complete", "root", "pass", {
  dialect: "mysql",
});

export default sequelize;
```

models/product.ts
```
import { DataTypes } from "sequelize";
import sequelize from "../util/database";

const Product = sequelize.define("product", {
  id: {
    type: DataTypes.INTEGER,
    autoIncrement: true,
    allowNull: false,
    primaryKey: true,
  },
  title: DataTypes.STRING,
  price: {
    type: DataTypes.DOUBLE,
    allowNull: false,
  },
  imageUrl: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  description: {
    type: DataTypes.STRING,
    allowNull: false,
  },
});

export default Product;
```
