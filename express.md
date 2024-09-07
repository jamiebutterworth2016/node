# Getting started with Express.js
Requires 4 files: app.ts, package.json, tsconfig.json, nodemon.json.

`mkdir project && cd project && code -r .`\
`npm init` - generates package.json\
`npm i typescript @types/node @types/express nodemon ts-node --save-dev`\
`npm i express --save`\
`npx tsc --init` - generates tsconfig.json\
package.json - set start script to `nodemon`

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
  },
  "exclude": ["node_modules"]
}
```

nodemon.json
```
{
    "watch": ["."],
    "ext": "ts",
    "exec": "ts-node ./app.ts"
}
```

app.ts
```
import http from "http";
import express from "express";

const app = express();
const server = http.createServer(app);
server.listen(3000);
```
