
07 Basic Authentication and Authorisation with JSON Web Tokens
===




## Table of Contents
- [07 Basic Authentication and Authorisation with JSON Web Tokens](#07-basic-authentication-and-authorisation-with-json-web-tokens)
  * [Table of Contents](#table-of-contents)
  * [Authentication and Authorisation](#authentication-and-authorisation)
    + [JWT](#jwt)
  * [Implementing JWT in NodeJS](#implementing-jwt-in-nodejs)
    + [app.js](#appjs)
    + [config.js](#configjs)
    + [user.js](#userjs)
    + [Verifying the Token - verifyToken.js](#verifying-the-token---verifytokenjs)
  * [Practical Example](#practical-example)
    + [Adding Authorisation](#adding-authorisation)


Authentication and Authorisation
---
- HTTP and HTTPS are stateless
    - strict auth would require users to reauth everytime they access a protected res
    - hence rely on token-based auth which is performed at the start
        - auth system issues signed auth token to end-user app
        - token appended to every req of client when protected res required
        - unique token verifies your identity and authorise you
    - __JSON Web Tokens (JWT)__ is a means of performing auth and authorisation

### JWT
- jwt - JSON based open standard for creating access tokens that assert some number of claims
- composed of
    - header
    - payload
    - signature that proves integrity of msg of receiving server
- content inside jwt is digitally signed either using a secret with HMAC algo OR leveraging the public key infrastructure (PKI) model with priv/pub RSA config

![](https://i.imgur.com/LGBkRdn.png)

- 3 parts envoded using base64 __separately__

```javascript=
const token = base64urlEncoding(header) + '.' + base64urlEncoding(payload) + '.' + base64urlEncoding(signature)

// example output
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJsb2dnZWRJbkFzIjoiYWRtaW4iLCJpYXQiOjE0MjI3Nzk2Mzh9.gzSraSYS8EXBxLN_oWnFSRgCzcmJmMjLiuyu5CSpyHI
```

Implementing JWT in NodeJS
---
- install jsonwebtoken lib
    - `npm install jsonwebtoken --save`


### app.js
```javascript=
// post endpt for above function
app.post('/api/login',function(req,res){

    var email=req.body.email;
    var password=req.body.password;

    user.loginUser(email,password,function(err,result){
        if(!err){
            res.send("{\"result\":\""+result +"\"}");
        }else{
            res.status(500);
            res.send(err.statusCode);
        }
    });
});
```

### config.js
- to hold the secret key for our jwt

```javascript=
var secret='s12xyz00'; //your own secret key
module.exports.key=secret;
```

### user.js
```javascript=
// use jwt.sign func to generate json web token and return to caller upon successful verification of login credentials
// user's role and id is also encoded into the jwt
// if fails, return null val for token

var config=require('../config.js'); 
var jwt=require('jsonwebtoken');

loginUser: function (email,password, callback) {   
    var conn = db.getConnection();
    conn.connect(function (err) {
        if (err) {
            console.log(err);
            return callback(err,null);
        }
        else {
            console.log("Connected!");
            var sql = 'select * from user where email=? and password=?';

            conn.query(sql, [email,password], function (err, result) {
                conn.end();

                if (err) {
                    console.log(err);
                    return callback(err,null);
                } else {
                    //console.log(config.key);
                    var token="";
                    if(result.length==1){
                        token = jwt.sign({
                            id: result[0].userid,
                            role: result[0].role
                        }, config.key, {
                            expiresIn: 86400    //expires in 24 hrs
                        });
                    }
                    return callback(null,token);
                }
            });
        }
    });
}
```

### Verifying the Token - verifyToken.js
- need to authorise verified user through token when protected service called
    - jwt shld be sent in the authorisation header using the bearer schema
        - `Authorization: Bearer <token>`
- create new folder `auth/` to hold middleware funcs to chekc for presence of token and verify its validity

```javascript=
// verifyToken.js
var jwt=require('jsonwebtoken');
var config=require('../config');

function verifyToken(req,res,next){
    console.log(req.headers);

    var token=req.headers['authorization']; //retrieve authorization header’s content
    console.log(token);

    if(!token || !token.includes('Bearer')){ //process the token
        res.status(403);
        return res.send({auth:'false',message:'Not authorized!'});
    }else{
        token=token.split('Bearer ')[1]; //obtain the token’s value
        console.log(token);
        jwt.verify(token,config.key,function(err,decoded){//verify token
            if (err){
                res.status(403);
                return res.end({auth:false,message:'Not authorized!'});
            }else{
                req.userid=decoded.userid; //decode the userid and store in req for use
                req.role=decoded.role; //decode the role and store in req for use
                next();
            }
        });
    }
}

module.exports=verifyToken;
```

- rmb to apply middleware in app.js!

```javascript=
var verifyToken=require('../auth/verifyToken.js');
…
app.post('/api/user',verifyToken,function(req,res){
……
});
```

Practical Example
---
```javascript=
// user.verify() add to user model
verify: function(username, password, callback) {
        const query = "SELECT * FROM user WHERE username=? and password=?";

        db.query(query, [username,password], (error, results) => {
            if (error) {
                callback(error, null);
                return;
            }
            if (results.length === 0) {
                callback(null, null);
                return;
            }else{
              const user = results[0];
              callback(null, user);
            }       
        });
    },

```

```javascript=
// /login end pt in controller
const jwt = require("jsonwebtoken");
const JWT_SECRET = require("../config.js"); 

app.post("/login/", (req, res) => {
  User.verify(
    req.body.username,
    req.body.password,
    (error, user) => {
      if (error) {
        next(error);
        return;
      }
      if (user === null) {
        res.status(401).send();
        return;
      }
      const payload = { user_id: user.id };
      jwt.sign(payload, JWT_SECRET, { algorithm: "HS256" }, (error, token) => {
        if (error) {
          console.log(error);
          res.status(401).send();
          return;
        } 
        res.status(200).send({
          token: token,
          user_id: user.id
        });
      })
  });
});
...
```

```javascript=
// isLoggedInMiddleware.js
// in callback if verification successful, we store decoded token in req.decodedToken and invoke next() to pass the req and res to the next middleware
// else return 401 unauthorised

const jwt = require("jsonwebtoken");
const JWT_SECRET = require("../config.js");

var check = (req, res, next) => {
  const authHeader = req.headers.authorization;
  if (authHeader === null || authHeader === undefined || !authHeader.startsWith("Bearer ")) {
    res.status(401).send();
    return;
  }
  const token = authHeader.replace("Bearer ", "");
  jwt.verify(token, JWT_SECRET, { algorithms: ["HS256"] }, (error, decodedToken) => {
    if (error) {
      res.status(401).send();
      return;
    }
    req.decodedToken = decodedToken;
    next();
  });
};
module.exports=check;
```
```javascript=
// mount middlewares in controller
const isLoggedInMiddleware = require("./isLoggedInMiddleware");
...
app.put("/users/:userID/", isLoggedInMiddleware, (req, res, next) => {
...
app.post("/users/:userID/friends/:friendID", isLoggedInMiddleware, (req, res) => {
...
app.delete("/users/:userID/friends/:friendID/", isLoggedInMiddleware, (req, res) => {
```

### Adding Authorisation
- we have authenticated, but anyone who is loggedin can freely update/delete users
    - only want logged in user to update/delete their own

```javascript=
// add check after userID parsed to see if userid in decoded token matches the one in req params
// app.js

app.put("/users/:userID/", isLoggedInMiddleware, (req, res, next) => {
  const userID = parseInt(req.params.userID);
  if (isNaN(userID)) {
    res.status(400).send();
    return;
  }

  // user ID in the request params should be the same as the logged in user ID
  if (userID !== req.decodedToken.user_id) {
    res.status(403).send();
    return;
  }
  ...
app.post("/users/:userID/friends/:friendID", isLoggedInMiddleware, (req, res) => {
    const userID = parseInt(req.params.userID);
    const friendID = parseInt(req.params.friendID);
    if (isNaN(userID) || isNaN(friendID)) {
      res.status(400).send();
      return;
    }
  
    if (userID === friendID) {
      res.status(400).send();
      return;
    }

    // user ID in the request params should be the same as the logged in user ID
    if (userID !== req.decodedToken.user_id) {
      res.status(403).send();
      return;
    }
    ...
app.delete("/users/:userID/friends/:friendID/", isLoggedInMiddleware, (req, res) => {
    const userID = parseInt(req.params.userID);
    const friendID = parseInt(req.params.friendID);

    if (isNaN(userID) || isNaN(friendID)) {
      res.status(400).send();
      return;
    }

    // user ID in the request params should be the same as the logged in user ID
    if (userID !== req.decodedToken.user_id) {
      res.status(403).send();
      return;
    }
    ...

```


###### tags: `BED` `DISM` `School` `Notes`