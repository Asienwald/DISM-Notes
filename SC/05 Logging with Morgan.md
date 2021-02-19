

05 Logging with Morgan
===




## Table of Contents

- [05 Logging with Morgan](#05-logging-with-morgan)
  * [Table of Contents](#table-of-contents)
  * [Logging](#logging)
    + [What to Log](#what-to-log)
    + [How to Log](#how-to-log)
  * [Morgan](#morgan)
    + [Pre-defined Tokens](#pre-defined-tokens)
    + [Pre-defined Log Formats](#pre-defined-log-formats)
    + [Custom Tokens](#custom-tokens)
      - [Applying Custom Tokens](#applying-custom-tokens)
      - [Examples](#examples)
    + [Logging to File](#logging-to-file)
      - [Examples](#examples-1)
    + [Log File Rotation](#log-file-rotation)
      - [More Examples](#more-examples)

Logging
---
- collect and store data over time for analysis
    - gain insights
    - resolve bugs
    - detect probs
- simplest form is `console.log` to log data to cmd
- why log?
    - debug
        - document steps for error
    - security audits
        - detect and log suspicious activities/events
    - complexity of tracking and detecting

### What to Log
- timestamp/log entry
- timing data for req
- request endpt data
    - eg. paths /users
    - eg. verbs - GET, POST etc.
- ip of req
- exceptions

### How to Log
- libs
    - morgan
    - winson
    - log4js


Morgan
---
- http req middleware for nodejs
    - simplifies logging reqs for app
    - https://www.npmjs.com/package/morgan
- http://expressjs.com/en/resources/middleware/morgan.html


![](https://i.imgur.com/LQ6MvOf.png)

- `npm install morgan --save`
    - `var morgan = require('morgan')`
- api - `morgan(format, options)`
    - create morgan logger middleware func with given format and options
    - format str can be string of predefined name, string of format str orfunc to produce a log entry
    - format func is called with 3 args - tokens, req and res
        - token is obj will all defined tokens
        - req is http req
        - res is http resp
        - func expected to return str which is log line
            - or undefined or null to skip logging

### Pre-defined Tokens
![](https://i.imgur.com/DtlUV0z.png)

```javascript
...
app.use(morgan(':method :url :date'));
...
```

### Pre-defined Log Formats
![](https://i.imgur.com/8eYwlQO.png)

```javascript
var morgan = require('morgan')
...
app.use(morgan('combined'))
...
```

### Custom Tokens
```javascript
// function returns some val representing token output in log
morgan.token('myToken', (req, res) => {
    ...
    return ...;
})
```

#### Applying Custom Tokens
- `app.use(morgan(":myToken" :method :url :date));`

#### Examples
**custom json token**
```javascript
morgan.token("json", function(req, res) {
    return JSON.stringify({
        date: nDate,
        url: req.url,
        status: res.statusCode,
        method: req.method,
        httpVersion: req.httpVersion
    })
})

// eg. used with format :json
app.use(morgan(':remote-addr ===> :method :url => :status  header count => :req-headers-length --> :date --> :response-time :json', {stream: appLogStream}));

// sample output with :json
::1 ===> GET /profile.html => 404  header count => 14 --> Tue, 01 Dec 2020 16:44:20 GMT --> 2.661 {"date":"12/2/2020, 12:44:18 AM","url":"/profile.html","status":404,"method":"GET","httpVersion":"1.1"}
```


### Logging to File
- use fs lib to create file stream and apply to morgan


```javscript
var fs = require('fs')
...
// flag = a - append mode to file
const appLogStream = fs.createWriteStream(path.join(__dirname__, 'app.log'), {flags: "a"});
...
app.use(morgan("combined", {stream: appLogStream}));
...
```

#### Examples
**App logging stream**
```javascript
var appLogStream = rfs.createStream('access.log', {
  interval: '1d', // rotate daily
  path: path.join(__dirname, 'logs') //write to a subdir log using path module to use parent dir
})

app.use(morgan(':remote-addr ===> :method :url => :status  header count => :req-headers-length --> :date --> :response-time :json', {stream: appLogStream}));

// eg. output to access.log
::1 ===> GET /profile.html => 404  header count => 14 --> Tue, 01 Dec 2020 16:44:20 GMT --> 2.661 {"date":"12/2/2020, 12:44:18 AM","url":"/profile.html","status":404,"method":"GET","httpVersion":"1.1"}
```

**Error logging stream**
```javascript
var errorLogStream = rfs.createStream('error.log', {
  interval: '1d', // rotate daily
  path: path.join(__dirname, 'logs') //write to a subdir log
})

app.use((morgan(':remote-addr ===> :method :url => :status :exception => :date --> :response-time :exception-json', {
  skip: function (req, res) { return res.statusCode < 400 },
  stream: errorLogStream
})));

// eg. output to error.log
::1 ===> GET /profile.html => 404 Not Found => Tue, 01 Dec 2020 16:44:20 GMT --> 2.661 {"exception":"Not Found","method":"GET","url":"/profile.html","ip":"::1","date":"12/2/2020, 12:44:18 AM"}
```


### Log File Rotation
- log file can grow to large size for apps on cloud
    - need to create multiple log files
        - eg. one for ea day
- use `rotating-file-stream` module
    - `npm install rotating-file-stream --save`

```javascript
var rfs = require('rotating-file-stream');
// create rotating write stream
var appLogStream = rfs.createStream('access.log', {
    interval: '1d', // rotate daily
    path: path.join(__dirname, 'log') //write to a subdir log
})
...
app.use(morgan('combined', {stream: appLogStream}));
```


#### More Examples
```javascript
const rfs = require("rotating-file-stream");
const stream = rfs.createStream("file.log", {
  // other eg. 300B, 300K, 1G
  size: "10M", // rotate every 10 MegaBytes written
  // other eg. 5s, 5m, 2h, 1M (rotate every midmight between 2 distinct months)
  interval: "1d", // rotate daily
  compress: "gzip" // compress rotated files
});
```


###### tags: `SC` `DISM` `School` `Notes`