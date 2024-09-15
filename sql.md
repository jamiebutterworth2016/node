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

export default pool;
```
