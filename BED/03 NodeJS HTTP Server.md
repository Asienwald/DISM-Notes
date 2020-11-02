

03 NodeJS HTTP Server
===



## Table of Contents

- [03 NodeJS HTTP Server](#03-nodejs-http-server)
  * [Table of Contents](#table-of-contents)
  * [HTTP](#http)
    + [HTTP Request Format](#http-request-format)
    + [HTTP Response Format](#http-response-format)
    + [Common HTTP Response Codes](#common-http-response-codes)
  * [Javascript Object Notation (JSON)](#javascript-object-notation--json-)
    + [Features](#features)
  * [1st Node Server App](#1st-node-server-app)
    + [HTTP Modules](#http-modules)
    + [Path Module](#path-module)
    + [Creating HTTP Server](#creating-http-server)
      - [Creating Static html Files](#creating-static-html-files)

HTTP
---
- most popular app layer protocol used for communicating between client and server
- provides standardised way for comps to communicate with ea other
    - specifies how client's request data will be constructed and set to server
    - and how server responds to these reqs
- to comm with server, client must indicate HTTP action like
    - GET
    - POST
    - PUT
    - DELETE
    - TRACE
    - OPTIONS
    - CONNECT
- in http protocol, req msg typically carries info like action and target URL in req msg
- when server receives req, server will
    - retrieve data from its data storage
    - package data in appropriate format
    - send data back to client
    - data is typically in html/css/js or JSON format for resful web services

![](https://i.imgur.com/EXS3fbm.png)

### HTTP Request Format
![](https://i.imgur.com/z3uVWMq.png)

### HTTP Response Format
![](https://i.imgur.com/wtjV515.png)
- 3 parts
    - status line
        - Eg. 200
    - headers
        - Eg. data format encoding of returned msg data
    - actual body of msg
        - Eg. html code for index.html
        - OR JSON format

### Common HTTP Response Codes
![](https://i.imgur.com/hlIVJDa.png)


Javascript Object Notation (JSON)
---
### Features
- lightweight
- language independent
- easy to read and write
- text based, human readable data exchange format
- uses key pairs describing the obj

```javascript=
var student1={
   "name":"John",
   "age":"18",
   "course":"DIT"
};

// directly use json obj by calling name of var and prop
console.log(student1.name);
console.log(student1.age);
console.log(student1.course);

// convert js obj to json, use stringify
var jsonStudent=JSON.stringify(jsStudent);
```

1st Node Server App
---
- js modules built into nodejs
    - http module
        - provides high performing foundation for http stack
    - path module
        - provides resolving of full paths, check of file paths etc.
    - file module
        - provides file reading, checking purposes

### HTTP Modules
- http module supports `createServer` function which takes in callback as a param
    - callback has 2 params, request and response
        - req is req msg that comes from client to process and extract info from
        - resp is resp msg we construct with header values and body of http resp msg


### Path Module
- enables us to exmine whether file exists/more details abt file eg. file extension
- has func for us to convert relative path to absolute

### Creating HTTP Server
- create `public/` folder which will contain all static files to be served to client
- `npm init`
- create `server.js` at root

```javascript=
const http = require('http');
const fs = require('fs');
const path = require('path');

const hostname = 'localhost';
const port = 3000;
const server = http.createServer((req, res) => {
    console.log('Request for page ' + req.url + ' using ' + req.method + ‘method’);
    if (req.method == 'GET') {
      var fileUrl=req.url;

      if (req.url == '/') //default file is index.html
        fileUrl = '/index.html';
  
      var filePath = path.resolve('./public'+fileUrl);

        fs.exists(filePath, (exists) => {
            if (!exists) {
                fileUrl='/error.html';
                filePath = path.resolve('./public'+fileUrl);
            
            }else{
                res.statusCode = 200;
                res.setHeader('Content-Type', 'text/html');
            }
            fs.createReadStream(filePath).pipe(res);
        });
    }
    else {
        fileUrl='/error.html';
        filePath = path.resolve('./public'+fileUrl);
        fs.createReadStream(filePath).pipe(res);

    }
});


server.listen(port, hostname, () => {
  console.log(`Server started and accessible via http://${hostname}:${port}/`);
});
```

```bash
# to run server
node server.js
# or use nodemon
```

#### Creating Static html Files
```htmlembedded=
<!-- index.html -->
<html>
    <body>
        Welcome to Node JS!!
    </body>
</html>

<!-- error.html -->
<html>
    <body>
        File does not exist or web server does not support post method!
    </body>
</html>
```




###### tags: `BED` `DISM` `School` `Notes`