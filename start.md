### Create project
mkdir project
cd project

### Node + TS
npm init - generates package.json\
npm i typescript @types/node --save-dev\
npx tsc --init - generates tsconfig.json\
tsconfig.json - change module to ESNEXT

### Server root
echo > app.ts\
```
import http from 'http'

http.createServer((req, res) => {
  console.log(req);
})  
```

### Build
npx tsc - generates js files (build)


