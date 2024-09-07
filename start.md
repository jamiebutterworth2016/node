### Create project with Node + TS
`mkdir project && cd project && code -r .`\
`npm init` - generates package.json\
Add type module to package.json\
`npm i typescript @types/node --save-dev`\
`npx tsc --init` - generates tsconfig.json\
Set module to ESNext tsconfig.json 

### Server root - vanilla Node
`echo > app.ts`
```
import http from 'http'

const server = http.createServer((req, res) => {
  console.log(req);
});

server.listen(3000, "localhost");
```

### Build and run
`npm i nodemon --save-dev`\
Add start script to package.json `npx tsc && nodemon app.js` - generates js files (build) && runs app\
`npm run start` 

### Install Express.js
`npm i express --save`\
`npm i @types/express --save-dev`

app.ts
```
import http from "http";
import express from "express";

const app = express();
const server = http.createServer(app);
server.listen(3000);
```

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

### Split app and routes into two separate files
app.ts
```
import http from "http";
import requestHandler from "./routes.js";

const server = http.createServer(requestHandler);
server.listen(3000, "localhost");
```

routes.ts
```
import http from "http";
import fs from "fs";

const requestHandler = (
  req: http.IncomingMessage,
  res: http.ServerResponse<http.IncomingMessage>
) => {
  const { url, method } = req;

  if (url === "/") {
    res.setHeader("Content-Type", "text/html");
    res.write("<html>");
    res.write("<head><title>Enter message</title></head>");
    res.write("<body>");
    res.write(
      `<form action="/message" method="POST"><input type="text" name="message"/><button type="submit">Send</button></form>`
    );
    res.write("</body>");
    res.write("</html>");
    return res.end();
  }

  if (url === "/message" && method === "POST") {
    const body: Uint8Array[] = [];

    req.on("data", (chunk) => {
      body.push(chunk);
    });

    let message = "";

    return req.on("end", () => {
      const parsedBody = Buffer.concat(body).toString();
      message = parsedBody.split("=")[1];
      fs.writeFile("message.txt", message, (err) => {
        res.writeHead(302, { location: "/" });
        return res.end();
      });
    });
  }

  res.setHeader("Content-Type", "text/html");
  res.write("<html>");
  res.write("<head><title>My First Page</title></head>");
  res.write("<body>");
  res.write("<h1>Hello from my Node.js Server!</h1>");
  res.write("</body>");
  res.write("</html>");
  return res.end();
};

export default requestHandler;
```
