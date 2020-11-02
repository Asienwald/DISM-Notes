

06 RESTful Web Services with Express & MySQL
===



## Table of Contents

- [06 RESTful Web Services with Express & MySQL](#06-restful-web-services-with-express---mysql)
  * [Table of Contents](#table-of-contents)
  * [RESTful API](#restful-api)
    + [API](#api)
    + [HTTP Response COde](#http-response-code)
    + [Example](#example)
    + [Model View Controll (MVC)](#model-view-controll--mvc-)
      - [Scenario](#scenario)
  * [Express](#express)
    + [Setting Up](#setting-up)
    + [Creating Connection to DB](#creating-connection-to-db)
      - [Sync](#sync)
      - [Async](#async)
    + [Querying Database](#querying-database)
      - [Sync](#sync-1)
      - [Async](#async-1)
    + [Define Routing in Controller](#define-routing-in-controller)
      - [Sync](#sync-2)
      - [Async](#async-2)
    + [Defining Main Server in Root](#defining-main-server-in-root)
  * [Nodemon](#nodemon)
  * [Postman](#postman)


RESTful API
---
### API
- application programming interface (api) defines set of operations that allow apps to communicate with it
    - Eg. web api or software libs
- REST APIs
    - REST - architectural style used to design API
    - data (res) in db is exposed through endpoints (url) of our api
        - res can be crated, updated and deleted (CRUD) through endpts
    - [Read more](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- CRUD operations correspond to http methods
    - get to retrieve res
    - post to create res
    - put to update res
    - delete to delete res

### HTTP Response COde
- important ones to rmb
- 2xx success
    - 200 ok - when get succeeds
    - 201 created - when post succeeds
    - 204 no content - when put or delete succeeds and there's nothing to send back
- 4xx client errs
    - 400 bad request - cannor process req due to invalid syntax
        - client shld not repeat same req
    - 404 not found - cannot find request res. res doesnt exist
- 5xx server errors
    - 500 internal server error - server encountered situation it doesnt know how to handle
        - use generic err msg for handling unexpected errors
- [Full list of status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)



### Example
![](https://i.imgur.com/Y1Comho.png)
- web services will be designed based on the __Model-View-Controller (MVC)__ design
    - web services will function in the __controller__ dir
    - data extraction/modification of database in __model__ dir

### Model View Controll (MVC)
- is simple architecture whr all components are separated into 3 classes
    - model
        - files that contain code to interact with db
    - view
        - components that display model to user
    - controller
        - components that handle any interaction with user

![](https://i.imgur.com/yGbtY3H.png)

#### Scenario
![](https://i.imgur.com/7lCuWm5.png)


Express
---
### Setting Up
- install necessary packages
```bash=
npm init
npm install mysql --save
npm install body-parser –save
npm install express --save
```

### Creating Connection to DB
#### Sync
```javascript=
// databaseConfig.js
var mysql = require('mysql');

var dbconnect = {
    getConnection: function () {
        var conn = mysql.createConnection({
            host: "localhost",
            user: "root",
            password: "root",
            database: "furniture”
        });     
        return conn;
    }
};
module.exports = dbconnect
```

#### Async
```javascript=
// db.js
const mysql = require("mysql2");

const dbconnect = {
    getConnection: ()=>{
        const conn = mysql.createPool({
            host:"localhost",
            port: 3306,
            user: "root",
            password: "password",
            database: "bruh"
        }).promise();
        return conn;
    }
}
module.exports = dbconnect;
```

### Querying Database
#### Sync
```javascript=
// example user.js in models/
var db = require('./databaseConfig.js');
var userDB = {
    getUser: function (userid, callback) {
        var conn = db.getConnection();
        conn.connect(function (err) {
            if (err) {
                console.log(err);
                return callback(err,null);
            }
            else {
                console.log("Connected!");
                var sql = 'SELECT * FROM user WHERE userid = ?';
                conn.query(sql, [userid], function (err, result) {
                    conn.end();
                    if (err) {
                        console.log(err);
                        return callback(err,null);
                    } else {
                        return callback(null, result);
                    }
                });
            }
              });
       }
}

module.exports = userDB
```

#### Async
```javascript=
// example async (functions used is not same but format is there)
// error handling of these statements is dont through a try catch in the controller file instead
const db = require("../database/db");
const dbConn = db.getConnection()

const get_users = async () => {
    const sql = "SELECT userid, username, profile_pic_url, created_at FROM users";
    [results, fields] = await dbConn.query(sql);
    return results
}

module.exports = {
    get_users: get_users
}
```

### Define Routing in Controller
#### Sync
```javascript=
// app.js in controllers/
var express = require('express');
var app = express();
var user = require('../models/user.js'); 

app.get('/api/user/:userid', function (req, res) {
    var id = req.params.userid;

    user.getUser(id, function (err, result) {
        if (!err) {
            res.send(result);
        }else{
            res.status(500).send(“Some error”);
        }
    });

});

module.exports = app
```

#### Async
```javascript=
// example of a separate async app.js
// products obj is basically the model code
const products = require('../model/products');
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
// parse app/x-www-form-urlencoded
app.use(bodyParser.urlencoded({extended: false}));


const ERROR_MSG = "Internal Server Error."

app.get('/api/retrieveProduct', async(req, res) => {
    try{
        let queryStr = req.body.query;
        const results = await products.retrieveProduct(queryStr);
        res.status(200).send(results);
    }catch(err){
        console.log(err);
        res.status(500).send(ERROR_MSG);
    }
})

module.exports = app;
```

### Defining Main Server in Root
```javascript=
// server.js at root of folder
var app = require('./controller/app.js');
var port=8081
var server = app.listen(port, function () {
    console.log('Web App Hosted at http://localhost:%s',port);
});

// Alternate
const app = require("./controllers/app");

app.listen(3000, () => {
    console.log(`Hosted at http://localhost:3000`);
});
```

Nodemon
---
- nodemon is cli that automatically detects changes to the codebase and restarts server for us
    - use npm have to manually restart everytime
- `npm install -g nodemon`
- to save as npm script, make changes to scripts section of package.json
    - run `npm run start-dev`

```json=
{
  ...
  "scripts": {
    "start-dev": "nodemon server.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  ...
}
```

Postman
---
- program for testing http endpoints





###### tags: `BED` `DISM` `School` `Notes`