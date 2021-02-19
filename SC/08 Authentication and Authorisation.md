

08 Authentication and Authorisation
===




## Table of Contents

- [08 Authentication and Authorisation](#08-authentication-and-authorisation)
  * [Table of Contents](#table-of-contents)
  * [Authentication vs Authorisation](#authentication-vs-authorisation)
  * [JSON Web Tokens](#json-web-tokens)
    + [JWT Structure](#jwt-structure)
    + [Using JWT](#using-jwt)
  * [Middlewares](#middlewares)
    + [Login Controller](#login-controller)
    + [Auth Middleware](#auth-middleware)
  * [Authorisation Middleware](#authorisation-middleware)
    + [Restricted API Controller](#restricted-api-controller)
  * [Frontend Javascript](#frontend-javascript)
  * [Sessions](#sessions)
    + [Cookies](#cookies)
    + [CSRF Attacks](#csrf-attacks)
  * [Hijacking](#hijacking)
    + [Data Storage](#data-storage)
    + [Hashing vs Encryption](#hashing-vs-encryption)
    + [Encryption](#encryption)
    + [Crypto Library](#crypto-library)


Authentication vs Authorisation
---
- auth
    - process/action of proving/showing sth to be genuine, true or valid
- authorisation
    - grant official perms/privs to res
    - verify whether access allowed through policies and rules
        - aka role based access control

![](https://i.imgur.com/1QXZZYx.png)


JSON Web Tokens
---
- jwt
    - open standard rfc
    - defines compact and self-contained way for securely transmitting info between parties as json obj
    - provide token based auth

### JWT Structure
- 3 segments separated by period
    - JWT header
        - algo used
        - token type
        - eg. `{ “alg”: “HS256”, “typ”: "JWT” }`
    - JWT payload/body
        - user defined info
    - JWT signature
        - crypto hash of earlier segments
        - `HMACSHA256( base64UrlEncode(header) + base64UrlEncode(payload) , ‘s3cr3t’ )`
            - pseudo code to create the hash
- all segments base64 encoded

### Using JWT
- `npm install --save jsonwebtoken`


Middlewares
---
### Login Controller
```javascript
app.post('/', (req, res) => {
    let { username, password } = req.body;

    user.verifyLogin(username, password, (err, user) => {
        if (err) return res.status(500).send({ message: 'an error occurred' }); 
        if (!user) return res.status(401).send({ message: 'user not authenticated' });

        jwt.sign(user, config.jwt.secret, { algorithm: 'HS256' }, (err, token) => {
            if (err) return res.status(500).send({ message: 'an error occurred' });
            res.status(200).send({ token });
        });
    });
});
```

### Auth Middleware
```javascript
function verifyToken(req, res, next) {
    let auth = req.headers.authorization;

    const authHeader = req.headers.authorization;
    if (!authHeader || !authHeader.startsWith('Bearer '))
        return res.status(401).send({ message: 'not authenticated' });

    const token = authHeader.replace('Bearer ', '');
    jwt.verify(token, config.jwt.secret, { algorithms: ['HS256'] }, (err, decoded) => {
        if (err) return res.status(401).send({ message: 'not authenticated' });
        req.decodedToken = decoded;
        next();
    });
}
```

Authorisation Middleware
---
### Restricted API Controller
```javascript
app.get('/users', verifyToken, (req, res) => {
    if (!req.decodedToken.role !== 'admin')
        return res.status(403)
            .send({ message: 'you dont have sufficient permissions' });

    // handle processing

    res.status(200).send({ users });
});

```


Frontend Javascript
---
- login html
```html
var xhr = new XMLHttpRequest();
xhr.open('POST', '/login', true);
xhr.setRequestHeader('Content-Type’, ‘application/x-www-form-urlencoded’);

xhr.onload = function () {
    if (this.readyState === XMLHttpRequest.DONE) {
        let response = JSON.parse(this.response);
        let msg = document.getElementById('msg');

        if (this.status === 200) {
            localStorage.setItem('jwt_token', response.token);
            msg.innerHTML = `You have logged in!`;
        } else {
            msg.innerHTML = `Error: ${response.message}`;
        }
    }
};

xhr.send(`username=${username}&password=${password}`);

```

- for restricted content

```html
let token = localStorage.getItem('jwt_token');var xhr = new XMLHttpRequest();
xhr.open(‘GET', '/api/users', true);
xhr.setRequestHeader(‘Authorization’, `Bearer ${jwt_token}`);

xhr.onload = function () {
    if (this.readyState === XMLHttpRequest.DONE) {
        let response = JSON.parse(this.response);
        // handle response
    }
};

xhr.send();

```

- logout
    - `localStorage.removeItem('jwt_token');`


Sessions
---
### Cookies
- purpose of cookies is to help webapp trace visits and activity

![](https://i.imgur.com/G2rpevD.png)

### CSRF Attacks
- CSRF is vulb that allows atker to induce users to perform actions not intended on a web service they're alr authenticated to
    - use automated sending of session cookies by browsers to bypass same origin policy
        - designed to prevent web servers from interfering with one another

![](https://i.imgur.com/64ux4jG.png)


Hijacking
---
- http send info in plaintext
- https use tls or ssl to crypto secure traffic

### Data Storage
- sensitive data
    - pwd
    - credit card num
    - NRIC
    - etc.

### Hashing vs Encryption
- hashing
    - 1 way func whr data mapped to fixed length val
    - used for auth
    - salting is extra step that adds extra val to end of pwd to change hash value produced
- encryption
    - 2 way func 
    - info scrambled so can be unscrambled ltr
- pwd hashing
    - gen random long string called salt
    - append salt to pwd
    - hash string using bcrypt
    - save salt and hash in user's db record

```javascript
bcrypt.hash(password, saltRounds, function(err, hash) {
  …
 }

bcrypt.compare(password,hashPwd,function(err,success){
 …
}

```

### Encryption
- asymmetric encryption
    - 1 key encrypt 1 key decrypt
    - foundation of PKI
        - trust model that undergirds SSL/TLS
- symmetric encryption
    - priv key encryption
    - after asymmetric encryption in SSL handshake, browser and server comm using symmetric session key

### Crypto Library
```javascript
// encrypt
var crypto = require('crypto');
var mykey = crypto.createCipher('aes-128-cbc', 'mypassword');
var mystr = mykey.update(stringToEncrypt, 'utf8', 'hex')
mystr += mykey.final('hex');

// decrypt
var crypto = require('crypto');
var mykey = crypto.createDecipher('aes-128-cbc', 'mypassword');
var mystr = mykey.update(EncryptedString, 'hex', 'utf8')
mystr += mykey.final('utf8');
```




###### tags: `SC` `DISM` `School` `Notes`