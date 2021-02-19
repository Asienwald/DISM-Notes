

06 Preventing XSS
===




## Table of Contents

- [06 Preventing XSS](#06-preventing-xss)
  * [Table of Contents](#table-of-contents)
  * [Middleware](#middleware)
  * [Securing Against XSS](#securing-against-xss)
    + [Validation-Regular Expressions](#validation-regular-expressions)
    + [Regex](#regex)
      - [Wildcard Characters](#wildcard-characters)
      - [Pre-defined Classes](#pre-defined-classes)
      - [Logical Operators](#logical-operators)
      - [Using Regular Expressions](#using-regular-expressions)
    + [External Libraries](#external-libraries)
  * [Validator](#validator)
    + [Sanitisation](#sanitisation)
    + [Escaping Data](#escaping-data)
    + [Remove Line Breaks, Tabs and Extra White Space](#remove-line-breaks--tabs-and-extra-white-space)
    + [Securing Input and Output](#securing-input-and-output)
  * [Parameters in SQL Statements](#parameters-in-sql-statements)

Middleware
---
![](https://i.imgur.com/ndVleVx.png)
- middleware
    - func that receive req and res with 3rd arg of another func that will call the next middleware func if any
- usually has middleware chain
    - chain of funcs called in sequence
    - last sends res back to browser
    - must called `next()` unless is last func in chain
        - else req will hang and timeout
    - changes made to req or res avail in next middleware func

![](https://i.imgur.com/Nvq6LZx.png)


Securing Against XSS
---
- input validation and output sanitisation in form of middlewares
- 2 standard controls against XSS
    - validate all user input form fields, GET and POST params, headers and cookies
        - only whitelisted chars shld be allowed
        - disallow special html chars
    - escape all string output
        - html special chars shld be html encoded and interpreted by browser literally

### Validation-Regular Expressions
- apps frequently need txt processing for features like word searches, email validation or XML doc integrity
    - needs pattern matching
- `RegExp` builtin in js

### Regex
#### Wildcard Characters
- `*` - match 0 or more occurrence
- `?` - match 0 or 1 occurrence
- `+` - match 1 or more occurrence
- `{x}` - match exactly x times
- `{x, y}` - match between x (inclusive) to y (inclusive) occur.
- `[123x]` - match single instance of any char in brackets
- `[0-9]` - range from 0-9
- `[^0-9]` - match single char except those specified in brackets

#### Pre-defined Classes
- `.` any chars
- `\d` - digit
- `\D` non digit
- `\s` whitespace
- `\S` non whitespace
- `\w` word char
    - `[a-zA-Z_0-9]`
- `\W` non word char
    - `[^\w]`

#### Logical Operators
- `XY` X followed by Y
- `X|Y` either x or y
- `(x)` x as capturing grp
- eg. `([13]x)|([ab]3)` will match `lx,3x,a3,b3`

#### Using Regular Expressions
- steps
    - define regexp to search
    - check input against regexp
    - blk or allow op to continue depending on regexp check

**Example Email Validation**
```javascript
var userinput=“abc@gmail.com”;
pattern=new RegExp(‘^.+@.+\.[a-z]+$’);//create regex with a pattern
 
if(pattern.test(userinput)){
    console.log(“Input is correct!”);
}else{
    console.log(“Input does not match pattern!”);
}
```

**Example Password Regex**
```javascript
// at least one upper case alphabet, at least one lower case alphabet, at least 1 number and 8 or more alphanumeric characters
passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{8,}$/;

if(!req.body.password.match(passwordRegex)){
   res.status(500).send("Password invalid.")
}
```

![](https://i.imgur.com/5TcBST7.png)

### External Libraries
- nodejs validator lib
    - https://www.npmjs.com/package/validator
    - `npm i validator --save`
    - lib helps sanitise & validate strings in app
        - common funcs to validate emails, credit cards, urls etc. alr defined



Validator
---
- can use `isAlphanumeric()` and `isEmail()` methods to replace some regex statements


```javascript
var validator=require('validator');
function validateRegistration(req,res,next){
    var username=req.body.username;
    var email=req.body.email;
    var role=req.body.role;
    var password=req.body.password;
    if (validator.isAlphanumeric(username) && validator.isEmail(email) && (role=='user' || role=='admin') && validator.isAlphanumeric(password) && password.length>7){
        next();
    }
    else{
        res.send(`{"Message":"Validation Failed"}`);
    }
}
module.exports.validateRegistration=validateRegistration;
```

```javascript
// apply middleware func
var validate=require('../validate/validate.js');

app.post('/api/user',…,validate.validateRegistration, function(req,res){
  …
}
```

### Sanitisation
- process of removing/replacing submitted data
- ensure outputted data is safe
- use validator to sanitise

### Escaping Data
- chars like `<>&'"/"'` shld be converted to corr html entities so wont be interpreted as code like js

```javascript
var validator=require('validator');
var input=“<script>alert(‘JS XSS!’);</script>”;
var sanitizedOutput=validator.escape(input);
```

### Remove Line Breaks, Tabs and Extra White Space
- validtor has `stripLow()` func that removes ascii control chars which are normally invisible in html

```javascript
var validator=require('validator');
var input=“Hi there!\r\n Welcome to Secure Coding   ”;
var sanitizedOutput=validator.stripLow(input);
```
### Securing Input and Output
- perform validation on input data
    - sanitisation on output
- apply middleware to api routes


Parameters in SQL Statements
---
```javascript
var sql=`insert into user(username,email,role,password) Values(?, ?, ?, ?)`;

dbConn.query(sql,[username, email, role, password],function(err,result){

    dbConn.end();
    if(err){
        console.log(err);
    }else{

        console.log(result);
    }
    return callback(err,result);
});
```


###### tags: `SC` `DISM` `School` `Notes`