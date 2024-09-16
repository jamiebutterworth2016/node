`npm i --save sql2 sequelize`  
`npm i --save-dev @types/sequelize`

util/database.ts
```
import { Sequelize } from "sequelize";

const sequelize = new Sequelize("node-complete", "root", "pass");

```
