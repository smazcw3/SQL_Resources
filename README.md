# SQL_Resources

This is intended to run SQL queries using sqlite. 

CREATING DATABASES
------------------
`sqlite3 testDB.db`


CREATING TABLES
---------------
~~~
 CREATE TABLE COMPANY
 (
 ID INT PRIMARY KEY NOT NULL,
 NAME TEXT NOT NULL,
 AGE INT NOT NULL,
 ADDRESS CHAR(50),
 SALARY REAL
 );
~~~

~~~
 CREATE TABLE DEPARTMENT
 (
 ID INT PRIMARY KEY NOT NULL,
 DEPT CHAR(50) NOT NULL,
 EMP_ID INT NOT NULL
 );
~~~

Listing DATABASES and TABLES
----------------------------
`.databases`  # Returns list of databases

`.tables`  # Returns list of tables


Attaching a database
--------------------
SQLite ATTACH DATABASE statement is used to select a particular database, and after this command, all SQLite statements will be executed under the attached database.

`ATTACH DATABASE 'testDB.db' as 'TEST';`


Detaching a database
--------------------
SQLite DETACH DATABASE statement is used to detach and dissociate a named database from a database connection which was previously attached using ATTACH statement

`DETACH DATABASE 'currentDB';`


DROPPING TABLES
----------------
`DROP TABLE COMPANY;`


POPULATING the TABLE
--------------------
#Populating the table `COMPANY`

`INSERT INTO COMPANY (ID, NAME, AGE, ADDRESS, SALARY)
VALUES (1, 'Paul', 32, 'California', 2000.00);`

`INSERT INTO COMPANY (ID, NAME, AGE, ADDRESS, SALARY)
VALUES (2, 'Allen', 23, 'Norway', 15000.00);`

`INSERT INTO COMPANY (ID, NAME, AGE, ADDRESS, SALARY)
VALUES (3, 'Teddy', 23, 'Norway', 20000.00);`

`INSERT INTO COMPANY (ID, NAME, AGE, ADDRESS, SALARY)
VALUES (4, 'Mark', 25, 'RichMond', 65000.00);`

`INSERT INTO COMPANY (ID, NAME, AGE, ADDRESS, SALARY)
VALUES (5, 'David', 27, 'Texas', 850000.00);`

`INSERT INTO COMPANY VALUES (6, 'Kim', 22, 'South-Hall', 45000.00);`

`INSERT INTO COMPANY VALUES (7, 'James', 24, 'Housten', 10000.00);`
`

#Populating the table `DEPARTMENT`

`INSERT INTO DEPARTMENT VALUES (1, 'IT Billing', 1);`

`INSERT INTO DEPARTMENT VALUES (2, 'Engineering', 2);`

`INSERT INTO DEPARTMENT VALUES (3, 'Finance', 7);`

`INSERT INTO DEPARTMENT VALUES (4, 'HR', 5);`


FORMATTING THE OUTPUT OF A QUERY
--------------------------------
`.header on`

`.mode column`

~~~
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
~~~

EXPRESSIONS
-----------

`SELECT * FROM COMPANY WHERE SALARY = 10000;`

`SELECT COUNT(*) AS "RECORDS" FROM COMPANY;`


`SELECT * FROM COMPANY WHERE AGE >=25 OR SALARY >= 65000;`

`SELECT * FROM COMPANY WHERE AGE IS NOT NULL;`


`SELECT * FROM COMPANY WHERE NAME LIKE 'Ki%';`  #NAME starts with Ki

`SELECT * FROM COMPANY WHER AGE LIKE '%2';` #AGE ends with 2

`SELECT * FROM COMPANY WHERE ADDRESS LIKE '%-%';` #ADDRESS has - inside the address text

Unlike LIKE operator, GLOB is case sensitive and it follows syntax of UNIX for specifying THE following wildcards.
 - The asterisk sign (*)
 - The question mark (?)

The asterisk sign (*) represents zero or multiple numbers or characters. The question mark (?) represents a single number or character.

`SELECT * FROM COMPANY WHERE NAME GLOB 'KI*';` #NAME starts with Ki

`SELECT * FROM COMPANY WHERE AGE GLOB '*2';` #AGE ends with 2

`SELECT * FROM COMPANY WHERE ADDRESS GLOB '*-*';` #ADDRESS has - inside the address text



`SELECT * FROM COMPANY WHERE AGE IN (25, 27);` #Either 25 or 27

`SELECT * FROM COMPANY WHERE AGE NOT IN (25, 27);`  #Neither 25 nor 27

`SELECT * FROM COMPANY WHERE AGE BETWEEN 25 AND 27;`  #Between 25 and 27



`SELECT AGE FROM COMPANY WEHRE EXISTS (SELECT AGE FROM COMPANY WHERE SALARY > 65000);`

`SELECT * FROM COMPANY WHERE AGE > (SELECT AGE FROM COMPANY WHERE SALARY > 65000);`



`SELECT * FROM COMPANY WHERE AGE >=25 AND SALARY >= 65000;`

`SELECT * FROM COMPANY WHERE AGE >= 25 OR SALARY >= 65000;`


UPDATING THE TABLE
------------------

`UPDATE COMPANY SET ADDRESS = 'Texas' WHERE ID = 6;`

`UPDATE COMPANY SET ADDRESS = 'Texas', SALARY = 20000.00;`


DELETING THE RECORD
-------------------
#Deleting selected record from table

`DELETE FROM COMPANY WHERE ID = 7;` 

#Deleting all the records of the table

`DELETE FROM COMPANY;` 


LIMITING the data returned by query
-----------------------------------

SELECT * FROM COMPANY LIMIT 6;

SELECT * FROM COMPANY LIMIT 3 OFFSET 2;  # picks up 3 records starting from the 3rd position.


SELECT * FROM COMPANY ORDER BY SALARY ASC;


ORDER (Sort) the data
---------------------
SELECT * FROM COMPANY WHERE SALARY >=20000 ORDER BY SALARY DESC LIMIT 2;

SELECT * FROM COMPANY WHERE AGE LIKE '2%' AND SALARY >= 10000 ORDER BY SALARY DESC LIMIT 4;


GROUP-ing the data
------------------
SELECT NAME, SUM(SALARY) FROM COMPANY GROUP BY NAME ORDER BY NAME;


HAVING clause
-------------
SELECT * FROM COMPANY GROUP BY NAME HAVING COUNT(NAME) < 2;


DISTINCT clause
---------------
SELECT DISTINCT NAME FROM COMPANY;

-----------------------------------------------------------------------------------------------------------

PRAGMA
------




CONSTRAINTS
-----------
Constraints are the rules enforced on a data columns on table.

DEFAULT CONSTRAINT
------------------
The DEFAULT constraint provides a default value to a column when the INSERT INTO statement does not provide a specific value.

CREATE TABLE COMPANY2
(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL,
ADDRESS CHAR(50),
SALARY REAL DEFAULT 50000.00
);


UNIQUE CONSTRAINT
-----------------
The UNIQUE Constraint prevents two records from having identical values in a particular column.


CREATE TABLE COMPANY3
(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL UNIQUE,
ADDRESS CHAR(50),
SALARY REAL DEFAULT 50000.00
);


PRIMARY KEY CONSTRAINT
----------------------
The PRIMARY KEY constraint uniquely identifies each record in a database table. There can be more UNIQUE columns, but only one primary key in a table.

A table can have only one primary key, which may consist of single or multiple fields. When multiple fields are used as a primary key, they are called a composite key.

CREATE TABLE COMPANY4
(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL UNIQUE,
ADDRESS CHAR(50),
SALARY REAL DEFAULT 50000.00
);


CHECK CONSTRAINT
----------------
CHECK Constraint enables a condition to check the value being entered into a record. If the condition evaluates to false, the record violates the constraint and isn't entered into the table.

~~~
CREATE TABLE COMPANY4
(
ID INT PRIMARY KEY NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL,
ADDRESS CHAR(50),
SALARY REAL CHECK(SALARY > 0)
)
~~~

DROPPING CONSTRAINT
-------------------
SQLite supports a limited subset of ALTER TABLE. The ALTER TABLE command in SQLite allows the user to rename a table or add a new column to an existing table. It is not possible to rename a column, remove a column, or add or remove constraints from a table.


JOINS
-----
Joins clause is used to combine records from two or more tables in a database. A JOIN is a means for combining fields from two tables by using values common to each.


Cross Join
----------
CROSS JOIN matches every row of the first table with every row of the second table. If the input tables have x and y row, respectively, the resulting table will have x*y row. Because CROSS JOINs have the potential to generate extremely large tables, care must be taken to only use them when appropriate.

SELECT EMP_ID, NAME, DEPT FROM COMPANY CROSS JOIN DEPARTMENT;


Inner Join
----------

INNER JOIN creates a new result table by combining column values of two tables (table1 and table2) based upon the join-predicate. The query compares each row of table1 with each row of table2 to find all pairs of rows which satisfy the join-predicate. When the join-predicate is satisfied, the column values for each matched pair of rows of A and B are combined into a result row.

The `INNER JOIN` keyword selects records that have matching values in both tables.

~~~
SELECT EMP_ID, NAME, DEPT 
FROM COMPANY INNER JOIN DEPARTMENT ON COMPANY.ID = DEPARTMENT.EMP_ID;
~~~

Outer Join
----------
OUTER JOIN is an extension of INNER JOIN. Though SQL standard defines three types of OUTER JOINs: LEFT, RIGHT, and FULL.

OUTER JOINs have a condition that is identical to INNER JOINs, expressed using an ON, USING, or NATURAL keyword. The initial results table is calculated the same way. Once the primary JOIN is calculated, an OUTER JOIN will take any unjoined rows from one or both tables, pad them out with NULLs, and append them to the resulting table.

LEFT JOIN
---------
The LEFT JOIN keyword returns all records from the left table (table1), and the matched records from the right table (table2). The result is NULL from the right side, if there is no match.
~~~
SELECT Customers.CustomerName, Orders.OrderID 
FROM Customers LEFT JOIN Orders ON Customers.CustomerID = Orders.OrderID 
ORDER BY Customers.CustomerName;
~~~

~~~
SELECT EMP_ID, NAME, DEPT
FROM COMPANY LEFT JOIN DEPARTMENT ON COMPANY.ID = DEPARTMENT.EMP_ID;
~~~

RIGHT JOIN
----------
The RIGHT JOIN keyword returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side, when there is no match.

SELECT Orders.OrderID, Employees.LastName, Employees.FirstName
FROM Orders RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;


FULL OUTER JOIN
---------------
The FULL OUTER JOIN keyword returns all records when there is a match in left (table1) or right (table2) table records.

~~~
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
~~~

~~~
SELECT EMP_ID, NAME, DEPT
FROM COMPANY FULL OUTER JOIN DEPARTMENT ON COMPANY.ID = DEPARTMENT.EMP_ID;
~~~

INDEXES
-------

Indexes are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.

~~~
CREATE INDEX salary_index ON COMPANY (salary);
~~~

TRANSACTIONS
------------
A transaction is a unit of work that is performed against a database. Transactions are units or sequences of work accomplished in a logical order, whether in a manual fashion by a user or automatically by some sort of a database program.

Following are the following commands used to control transactions:

`BEGIN TRANSACTION` − To start a transaction.

`COMMIT` − To save the changes, alternatively you can use END TRANSACTION command.

`ROLLBACK` − To rollback the changes.

Transactional control commands are only used with DML commands INSERT, UPDATE, and DELETE. They cannot be used while creating tables or dropping them because these operations are automatically committed in the database.

#Transaction that doesn't delete the records since there is rollback command in the last line
~~~
BEGIN;
DELETE FROM COMPANY WHERE AGE = 25;
ROLLBACK;
~~~

#Transaction that doesn't delete the records since there is commit command in the last line
~~~
BEGIN;
DELETE FROM COMPANY WHERE AGE = 25;
COMMIT;
~~~


AUTOINCREMENT
-------------
We can auto increment a field value by using AUTOINCREMENT keyword when creating a table with specific column name to auto increment.

~~~
CREATE TABLE COMPANY5(
ID INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
NAME TEXT NOT NULL,
AGE INT NOT NULL,
ADDRESS CHAR(50),
SALARY REAL
);
~~~

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY)
VALUES ( 'Paul', 32, 'California', 20000.00 );`

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY) 
VALUES('Allen', 25, 'Texas', 15000.00);`

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY) 
VALUES('Teddy', 23, 'Norway', 20000.00);`

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY) 
VALUES('Mark', 25, 'Rich-Mond', 20000.00);`

`INSERT INTO COMPANY5  (NAME,AGE,ADDRESS,SALARY)
VALUES ( 'David', 27, 'Texas', 85000.00 );`

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY)
VALUES ( 'Kim', 22, 'South-Hall', 45000.00 );`

`INSERT INTO COMPANY5 (NAME,AGE,ADDRESS,SALARY)
VALUES ( 'James', 24, 'Houston', 10000.00 );`



EXPLAIN
-------

Statement can be preceded by the keyword "EXPLAIN" or by the phrase "EXPLAIN QUERY PLAN" used for describing the details of a table.


`EXPLAIN SELECT * FROM COMPANY5 WHERE Salary >= 20000;`


DATE and TIME
-------------
#Computes the current date

`SELECT date('now');`  

#last day of the current month

`SELECT date('now','start of month','+1 month','-1 day');`  

`SELECT datetime(1092941466, 'unixepoch', 'localtime');`

#computes the current UNIX timestamp

`SELECT strftime('%s','now');`  



VIEWS
-----
A view is nothing more than a SQLite statement that is stored in the database with an associated name. It is actually a composition of a table in the form of a predefined SQLite query. SQLite views are read-only and thus you may not be able to execute a DELETE, INSERT or UPDATE statement on a view.

~~~
CREATE VIEW COMPANY_VIEW AS
SELECT ID, NAME, AGE
FROM  COMPANY;
~~~

`DROP VIEW COMPANY_VIEW;`


SUBQUERIES
----------
A subquery is used to return data that will be used in the main query as a condition to further restrict the data to be retrieved. An ORDER BY cannot be used in a subquery, although the main query can use an ORDER BY. The GROUP BY can be used to perform the same function as the ORDER BY in a subquery. BETWEEN operator cannot be used with a subquery; however, BETWEEN can be used within the subquery.

`SELECT AGE FROM COMPANY WEHRE EXISTS (SELECT AGE FROM COMPANY WHERE SALARY > 65000);`

`SELECT * FROM COMPANY WHERE AGE > (SELECT AGE FROM COMPANY WHERE SALARY > 65000);`

`SELECT * FROM COMPANY WHERE ID IN (SELECT ID FROM COMPANY WHERE SALARY > 45000);`


INJECTION
---------
If you take user input through a webpage and insert it into a SQLite database there's a chance that you have left yourself wide open for a security issue known as SQL Injection. In this chapter, you will learn how to help prevent this from happening and help you secure your scripts and SQLite statements.

Injection usually occurs when you ask a user for input, like their name, and instead of a name they give you a SQLite statement that you will unknowingly run on your database.

Never trust user provided data, process this data only after validation; as a rule, this is done by pattern matching.


VACUUM
------
VACUUM command cleans the main database by copying its contents to a temporary database file and reloading the original database file from the copy. This eliminates free pages, aligns table data to be contiguous, and otherwise cleans up the database file structure.





























 
