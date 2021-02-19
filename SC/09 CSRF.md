

09 CSRF
===




## Table of Contents

- [09 CSRF](#09-csrf)
  * [Table of Contents](#table-of-contents)
  * [CSRF](#csrf)
    + [Auth Protocol](#auth-protocol)
    + [Session Management](#session-management)
      - [Express-Session](#express-session)
      - [Express-Mysql-Session](#express-mysql-session)
      - [Get/Set Session Values](#get-set-session-values)
      - [Logging Out](#logging-out)
  * [CSRF Attacks](#csrf-attacks)
    + [Conducting CSRF Attacks](#conducting-csrf-attacks)
    + [Preventing CSRF Attacks](#preventing-csrf-attacks)
    + [Generating CSRF Tokens](#generating-csrf-tokens)
      - [Implementation](#implementation)
  * [Session Cookie Notes](#session-cookie-notes)


CSRF
---
- CSRF
    - malicious website cause user's browser to perform unwanted action on trusted site when user is auth
    - works as browser requests auto include all cookies including session cookies
    - if user is auth, site cannot distinguish between legit and forged reqs

### Auth Protocol
- cookies used as common auth protocol
    - stores session id to uniquely identify users

![](https://i.imgur.com/nDHEa97.png)


### Session Management
- a session
    - corresponds to 1 client
    - identify user throughout his usage of the webapp
    - store user info
        - bind data to sessions
    - shld be cleared when user logouts to prevent session fixation atks
- session management with express
    - http stateless to use sessions
    - assign client session id and make reqs using that id
        - info of user linked to this id on server
    - use `express-session` and `express-mysql-session`

#### Express-Session
- node module to manage sessions and store session data
- `npm i express-session`

```javascript=
var session = require('express-session');
app.use(session({
    secret: 'an231hjEZ10mzk$zAP', //your secret key
    store: sessionStore,  //we will use the mysql store, to be shown
    saveUninitialized: false,
    resave: false
});
```

#### Express-Mysql-Session
- store user's session vars
- `npm i express-mysql-session`

```javascript
var MySQLStore = require('express-mysql-session')(session);

var sessionStore = new MySQLStore({}/* session store options */, dbconnect.getConnection());//use the mysql db connection
```

#### Get/Set Session Values
- use `req.session.varname = value`

```javascript
// store user data after login
req.session.role = role
req.session.username = username

// retrieve role of user
var session = req.session
var role = session.role
```

**Check user roles**
```javascript
verifySession: function(req, res, next){
    var session = req.session
    if(session.role){
        next()
    }
    else{
        res.status(403)
        res.send({"Message": "Not Authorized"})
    }
}
```

#### Logging Out
- destroy saved session vals and clear session to prevent session atks
    - `req.session.destroy()` to clear session and remove session id cookie at client side


CSRF Attacks
---
- possible atk scenarios
    - modify product info in backend
    - change passwd func
    - deletion of data in backend
    - etc.

### Conducting CSRF Attacks
- needs 3 conditions
    - relevant action
        - eg. priv action like modifying perms for other users or action on user-specific data
    - cookie-based session handling
        - relies **solely** on session cookies to identify user
        - cannot use any other mechanisms for tracking sessions
    - no unpredictable req params
        - req to atk cannot have params whose values the atker cannot determine/guess
- https://portswigger.net/web-security/csrf


### Preventing CSRF Attacks
- embed csrf token in form field
    - is piece of data that is random, unique and attached to a form
    - included in hidden input tag
    - shld be unpredictable
    - tied to user session
        - strictly validated in every case before action is executed


### Generating CSRF Tokens
- can use nodejs crypto lib to generate and check csrf tokens
    - or use csurf lib
        - http://expressjs.com/en/resources/middleware/csurf.html
- token generated for get reqs
    - can check for post, put and delete
- before data change operations can be executed, must issue GET req to gen a random CSRF token
    - returned by GET method and added as hidden field to webpage
    - csrf token passed when POST/PUT/DELETE op called and checked by csurf middleware before executing


#### Implementation
- `npm install csurf --save`

```javascript
var csrf = require('csrf')
var csrfProtection = csrf()

app.get('/csrfGetToken', csrfProtection, function(req, res){
    console.log(req.csrfToken())
    res.status(200).send({'csrfToken': "${req,csrfToken()}"})
})

app.post('/csrfModifyData', csrfProtection, function(req, res){
    // write code to modify data
    res.send("success")
})
```


Session Cookie Notes
---
- cookies not send by default for js/jquery call cross origin
    - diff port/domain
- same origin policy prevents session id cookie from being sent across origins/domains when using js calls
    - server must explicitly allow domain to run js code to send cookie through CORS
        - note that using * will still be blocked
    - hence hacker cannot steal csrf token val through js code
        - though html forms/elements will send cookie by default even across origins - allows csrf atks





###### tags: `SC` `DISM` `School` `Notes`