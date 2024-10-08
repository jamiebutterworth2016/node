# Getting started with Express.js
Requires 4 files: app.ts, package.json, tsconfig.json, nodemon.json.

`mkdir project && cd project && code -r .`\
`npm init` - generates package.json\
`npm i express --save`\
`npm i typescript --save-dev nodemon ts-node @types/node @types/express`\
`npx tsc --init` - generates tsconfig.json

package.json
```
{
  "name": "nodejs-complete-guide",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon"
  },
  "author": "",
  "license": "ISC",
  "description": "",
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/node": "^22.5.4",
    "nodemon": "^3.1.4",
    "ts-node": "^10.9.2",
    "typescript": "^5.5.4"
  },
  "dependencies": {
    "express": "^4.19.2"
  }
}
```

tsconfig.json
```
{
  "compilerOptions": {
    "target": "ES2016",                                 
    "module": "CommonJS",
    "esModuleInterop": true,                             
  }
}
```

nodemon.json
```
{
  "watch": ["."],
  "ext": "ts",
  "exec": "ts-node app.ts"
}
```

app.ts
```
import express from "express";

const app = express();

app.use((req, res, next) => {
  console.log("middleware");
  next();
});

app.use((req, res, next) => {
  console.log("middleware 2");
  res.send("<h1>Hello from express!</h1>");
});

app.listen(3000);
```
