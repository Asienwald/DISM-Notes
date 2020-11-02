

04 RESTful Web Services with Express
===




## Table of Contents

- [04 RESTful Web Services with Express](#04-restful-web-services-with-express)
  * [Table of Contents](#table-of-contents)
  * [Express](#express)
    + [Serving Static Web Pages](#serving-static-web-pages)
  * [RESTful Web Services](#restful-web-services)
    + [Principles](#principles)
    + [HTTP Methods](#http-methods)
      - [Diff between PUT and POST](#diff-between-put-and-post)
    + [Express App Routes](#express-app-routes)
      - [Example](#example)

Express
---
- express is minimal and flexible nodejs web app framework that provides a robust set of features for web and mobile apps
    - expressjs is prebuilt nodejs framework that can help in creating server-side web apps faster and smarter
- key features
    - simplicity
    - minimalism
    - flexibility
    - scalability
- supports various middleware modules u can easily apply and use
    - middleware funcs allow you to modify req and res objs with relevant info
    - basically gives access to req and res in apps request to resp cycle
    - https://medium.com/@jamischarles/what-is-middleware-a-simple-explanation-bb22d6b41d01

![](https://i.imgur.com/oQf8R4O.png)


### Serving Static Web Pages
- create file `server.js` in root dir

```javascript=
var express = require('express');
var serveStatic = require('serve-static');
var app = express();
var port=3000;
var hostname="localhost";

app.use(serveStatic(__dirname + '/public')); //apply middleware with app.use

// custom middleware to see req obj
app.use(function(req, res, next) {//create our custom middleware
    console.log(req.url);
    console.log(req.method)
    console.log(req.path);    
    console.log(req.query.id);
    next();
});

// custom middleware to see res obj
app.use(function(req, res, next) {
    console.log(req.url);
    console.log(req.method)
    console.log(req.path);    
    console.log(req.query.id);
    res.status(200);
    res.type(".html");
    res.end("<html><body>Using response object!!</body></html>");
    // res.redirect("https://www.sp.edu.sg");//comment out if we just want to redirect

    // next(); // since we are setting the whole response data, do not pass to the next middleware
});



app.listen(port, hostname, () => {
    console.log(`Server started and accessible via http://${hostname}:${port}/`);
});

```

RESTful Web Services
---
- REST is term invented by Roy Fielding in his doctoral dissertation “Architectural Styles and the Design of Network-based Software Architecture” in 2000
- __representational state transfer (REST)__ is architectural style that specifies constraints (Eg. uniform interface) that if applied to web service induce desirable properties like perf, scalability and modificability that enable services to work best on the web
- in REST style, data and functionality are considered res and accessed using __uniform resource identifiers (URIs)__ (AKA web url links)
    - res acted upon by using set of simple, well-defined operations
- REST style constraints an architecture to client/server arch and designed to use stateless comm protocol, typically http
    - clients and servers exchange representatives of res by using standardised interface and protocol

### Principles
- resource identification through URI
    - restful web service exposes set of res that identify targets of interaction with its clients
    - identified by URIs, which provides global addressing space for res and service discovery
- uniform interface
    - res manipulated using fixed set of 4 create, read, update and delete operations
        - PUT, GET, POST & DELETE
- self-descriptive msgs
    - res decoupled from respresentation so content can be accessed in variety of formats
    - Eg. HTML, XML, plaintext, pdf, jpeg, json
        - json most popular
- stateless interactions
    - every interaction with res is stateless
        - req msg is self-contained
    - stateful interactions are based on concept of explicit state transfer
        - several techniques to exchange state
            - URI rewriting, cookies, hidden form fields
    - state can be embedded in resp msgs to point to valid future states of interaction

![](https://i.imgur.com/66zkL16.png)


### HTTP Methods
![](https://i.imgur.com/m5FBWbm.png)
- safe op - op that dont have any effect on orig val of res
    - read op only fetches data so doesnt modify data
- idempotent op - op that gives same result no matter how many times its performed
    - eg. delete user - result will always be same no matter how many times performed

#### Diff between PUT and POST
- PUT is idempotent while POST is not
    - POST multiple times may result in multiple res created on server
- PUT must also specify complete URI of the res
    - implies that client shld be able to construct the URI of a res even if it doesnt yet exist on the server
        - this is possible if its client's job to choose unique name/ID for res
    - if client cannot guess complete URI of res, no option but to use POST

![](https://i.imgur.com/H4SRybP.png)


### Express App Routes
- express provides http verb + URL based routing support
- with express simply code app.VERB(path, callback) to register middleware chain
    - can call `app.all` to register middleware called whenever path matches
        - irrespective of http verb


#### Example
![](https://i.imgur.com/QQgFG25.png)

```javascript=
// server.js
var express = require('express');
var bodyParser = require('body-parser');
var port=8081;//use another port 8081 for this exercise
var hostname="localhost";

var app = express();

var urlencodedParser = bodyParser.urlencoded({ extended: false });
app.use(urlencodedParser);//attach body-parser middleware
app.use(bodyParser.json());//parse json data

//VERB+URL 
app.get('/api/user', function (req, res) {

   res.status(200);
   res.type(".html");
   res.end("Data of all users sent!");
});

app.listen(port, hostname, () => {
    console.log(`Server started and accessible via http://${hostname}:${port}/`);
});

```

- use postman to test our routes

![](https://i.imgur.com/ySHPPyN.png)




###### tags: `BED` `DISM` `School` `Notes`