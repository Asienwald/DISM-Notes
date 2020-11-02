

05 Database Systems
===



## Table of Contents
- [05 Database Systems](#05-database-systems)
  * [Table of Contents](#table-of-contents)
  * [Database Management Systems (DBMS)](#database-management-systems--dbms-)
    + [Relational Models](#relational-models)
      - [Rules](#rules)
      - [Attributes](#attributes)
      - [NULL Attribute Values](#null-attribute-values)
    + [Candidate Keys](#candidate-keys)
    + [Primary Key](#primary-key)
    + [Foreign Key](#foreign-key)
    + [Data Types in MySQL](#data-types-in-mysql)
      - [Common Attribute Data Types](#common-attribute-data-types)
  * [SQL](#sql)
    + [Creation/Drop Commands](#creation-drop-commands)
      - [Creating Database Schema](#creating-database-schema)
      - [Create Table](#create-table)
      - [Delete Table](#delete-table)
    + [Queries](#queries)
      - [Select](#select)
      - [Insert](#insert)
    + [More Complex Queries](#more-complex-queries)


Database Management Systems (DBMS)
---
- advantages of databases
    - data integrity
        - data inserted must conform to defined db schema
        - allow to maintain sanity and certainty when dealing with large amts of data
    - querying lang (SQL)
        - db can understand special queries
- dbms - collection of programs used to 
    - manage - create, update or delete
    - protect
    - control access of data in db
- common relational DBMSs are
    - oracle
    - mssql
    - db2
- actual definition
    - computer software designed for purpose of managing dbs based on a variety of data models

### Relational Models
#### Rules
- name of relation is unique in a db
    - cannot create another r/s or table in same db with same name
- every cell must be single valued
    - cannot have multi-valued cell
- attribute name in relation must be unique
    - cannot have 2 attr with same name
- ea tuple in relation is unique
    - cannot have duplicate tuple/row
    - defining primary key will ensure every tuple is unique

#### Attributes
- attribute - column name in table that defines characteristic of the obj
- attribute value
    - col values with actual data 

#### NULL Attribute Values
- NULL is special val allowed in relational db
    - means val is unknown or not applicable


### Candidate Keys
- candidate key - key that can uniquely identify a tuple in a relation
    - Eg. email that's unique across entire table and can be used to identify a row
- there might be many suitable candidate keys for a relation
    - choose most suitable candidate key for relation
    - this is the __primary key__

### Primary Key
- col used to identify a specific row in table
    - must be unique
    - usually auto generated and incremented

### Foreign Key
- a key that references another column from another table

### Data Types in MySQL
![](https://i.imgur.com/op7xpv7.png)

#### Common Attribute Data Types
- integer
- smallint
- decimal(m, n)
- char(n)
- varchar(n)
- date/datetime
- NOTE
    - unsigned short
        - 0 to 65535
    - signed short
        - -32768 to 32767
    - unsigned long
        - 0 to 4294967295
    - signed long
        - -2147483648 to 2147483647
    - whole numbers
        - -32767 to 32767


SQL
---
- standard lang for db
    - to comm with dbms to store, manipulate and retrieve data in db
    - also create and manage db

### Creation/Drop Commands
#### Creating Database Schema
```sql=
-- ensure that schema doesnt alr exist
DROP DATABASE IF EXISTS `electronics`; 
-- create new schema
CREATE DATABASE IF NOT EXISTS `electronics`
-- use schema so following queries will work
USE `electronics`;
```

#### Create Table
```sql=
-- simple table with a few cols and one primary key
CREATE TABLE CUSTOMER 
(TITLE			CHAR(2)		NOT NULL,
FIRST_NAME		VARCHAR(20)	NOT NULL,
LAST_NAME		VARCHAR(20)	NOT NULL,
EMAIL			VARCHAR(50)	NOT NULL,
PASSWORD		CHAR(8)		NOT NULL,
DOB                    DATE		NULL,
PRIMARY KEY (EMAIL));

-- this example here shows the usage of a unique key apart from primary key
CREATE TABLE IF NOT EXISTS `category` (
  `categoryID` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `description` varchar(255) NOT NULL,
  PRIMARY KEY (`categoryID`),
  UNIQUE KEY `UNIQUE NAME` (`name`)
)

-- more complex table with a primary key, foreign key and timestamp row
-- fkCategoryID is a foreign key that references the categoryID col from the category table
-- dateInserted col automatically generates the current timestamp when a new row is inserted
DROP TABLE IF EXISTS `products`;
CREATE TABLE IF NOT EXISTS `products` (
  `productID` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `description` varchar(255) NOT NULL,
  `brand` varchar(45) NOT NULL,
  `fkCategoryID` int NOT NULL,
  `imageURL` varchar(45) NOT NULL,
  `dateInserted` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`productID`),
  FOREIGN KEY (`fkCategoryID`) REFERENCES `category` (`categoryID`) ON DELETE CASCADE ON UPDATE CASCADE)
```

#### Delete Table
```sql=
DROP TABLE CUSTOMER;
```


### Queries
#### Select
```sql=
-- select statement
SELECT * FROM tablename WHERE tablerow=criteria;

-- select distinct values
SELECT DISTINCT country from addresstable;

-- order the results in asc (but actually asc is optional)
SELECT * from country ORDER BY country ASC
```

#### Insert
```sql=
-- insert new values
INSERT INTO tablename(col1, col2, col3) VALUES(val1, val2);

-- update existing role
-- [] indicates that portion of statement is optional
-- ... indicates of the possible existance of more args
UPDATE tablename SET col1=val1, [col2=val2...] [WHERE tablerow=criteria]

-- delete rows
DELETE FROM tablename WHERE tablerow=criteria
```

### More Complex Queries
```sql=
-- select values of cols from 2 different tables based on a condition with INNER JOIN
select reviews.travel_id, reviews.content, reviews.rating, users.username, users.profile_pic_url, reviews.created_at from reviews inner join users on reviews.user_id = users.userid where reviews.travel_id = ?;

-- select all cols in product table and name col in category table with a join statement
-- on the condition that the name col in prod table has a substring containing the payload
-- OR the name col in category table is equal to the payload
select products.*, category.name as categoryName from products inner join category on products.fkCategoryID = category.categoryID where products.name like concat('%', ?, '%') or category.name = ?

-- insert new row if no duplicate else update said row's description value
-- the name col in category must be a unique key (if that's what you want to decide whether its dupe or not)
insert into category (name, description) values(?, ?) on duplicate key update description = ?
```


###### tags: `BED` `DISM` `School` `Notes`