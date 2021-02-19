

07 Preventing SQL Injection
===



## Table of Contents

- [07 Preventing SQL Injection](#07-preventing-sql-injection)
  * [Table of Contents](#table-of-contents)
  * [SQL Injection Prevention](#sql-injection-prevention)
    + [Placeholders](#placeholders)
    + [Stored Procedures](#stored-procedures)
    + [Best Practice](#best-practice)

SQL Injection Prevention
---
### Placeholders
- mysql `query()`
    - uto escape user inputs with placeholders ?
    - ? replaced in sequential order with values represented in arr of same order

```javascript
var sql = `SELECT userid,email,username FROM user WHERE userid=? and role=?`;

conn.query(sql, [userid,role], function(err, result){
….
}

// or can be key value pair
var sql = `SELECT userid,email,username FROM user WHERE  ? and ?`;

conn.query(sql, [userid:`${userid}`,role:`${role}`], function(err, result){
….
}
```
![](https://i.imgur.com/AF5pOJc.png)


### Stored Procedures
- dev can create stored procedures to create specific views with restricted access instead of using normal queries
- stored procedure is func/method that works like an interface to specific restricted parts of db
    - can also declare vars in db
    - can embed multiple sql statements and implement if/else or looping logic
- right click stored procedure > created stored procedure

![](https://i.imgur.com/WnX0j8y.png)
- procedure will retun arr of results so query row data extracted as `result[0]`

```javascript
var sql=`call finduser(?,?)`; 
conn.query(sql, [userid,role], function(err, result){
    ...
});
```

### Best Practice
- use placeholders in mysql node lib to escape inputs
- use stored procedures
- if not possible
    - input validation and whitelisting with regex
    - datatype checks
    - escape input
- for db config
    - strong pwd
    - acc with least priv on db for client apps
        - allow access to required data for perf of required tasks only
    - ensure conns to db from client app is encrypted






###### tags: `SC` `DISM` `School` `Notes`