My hackerrank solutions for MySQL
-----------------------------------------

**Revising the Select Query I**

*Query all columns for all American cities in CITY with populations larger than 100000. The CountryCode for America is USA.*

~~~
SELECT * FROM CITY WHERE COUNTRYCODE = 'USA' AND POPULATION > 100000;
~~~

***

**Revising the Select Query II**

*Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA.* 

~~~
SELECT NAME FROM CITY WHERE POPULATION > 120000 AND COUNTRYCODE = 'USA';
~~~

***

**Select All**

*Query all columns (attributes) for every row in the CITY table.*

~~~
SELECT * FROM CITY;
~~~

***

**Select By ID**

*Query all columns for a city in CITY with the ID 1661.*

~~~
SELECT * FROM CITY WHERE ID=1661;
~~~

***

**Japanese Cities' Attributes**

*Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.*

~~~
SELECT * FROM CITY WHERE COUNTRYCODE='JPN';
~~~

***

**Weather Observation Station 1**

*Query a list of CITY and STATE from the STATION table.*

~~~
SELECT CITY, STATE FROM STATION;
~~~

***

**Weather Observation Station 3**

*Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE ID%2=0;
~~~

***

**Weather Observation Station 5** (INCORRECT!!)

*Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.*

~~~
SELECT TOP 1 CITY, LEN(CITY) FROM STATION ORDER BY LEN(CITY) ASC;
SELECT TOP 1 CITY, LEN(CITY) FROM STATION ORDER BY LEN(CITY) DESC;
~~~

***

**Weather Observation Station 6**

*Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from **STATION**. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY LIKE 'a%' OR CITY LIKE 'e%' OR CITY LIKE 'i%' OR CITY LIKE 'o%' OR CITY LIKE 'u%';
~~~

***

**Weather Observation Station 7**

*Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY LIKE '%a' OR CITY LIKE '%e' OR CITY LIKE '%i' OR CITY LIKE '%o' OR CITY LIKE '%u';
~~~

***

**Weather Observation Station 8**

*Query the list of CITY names from **STATION** which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY RLIKE '^[aeiouAEIOU].*[aeiouAEIOU]$';
~~~

***

**Weather Observation Station 9**

*Query the list of CITY names from **STATION** that do not start with vowels. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY NOT RLIKE '^[aeiouAEIOU].*';
~~~

***

**Weather Observation Station 10**

*Query the list of CITY names from **STATION** that do not end with vowels. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY NOT RLIKE '.*[aeiouAEIOU]$';
~~~

***

**Weather Observation Station 11**

*Query the list of CITY names from **STATION** that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY NOT RLIKE '^[aeiouAEIOU].*[aeiouAEIOU]$';
~~~

***

**Weather Observation Station 12**

*Query the list of CITY names from **STATION** that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.*

~~~
SELECT DISTINCT(CITY) FROM STATION WHERE CITY NOT RLIKE '^[aeiouAEIOU].*' AND CITY NOT RLIKE '.*[aeiouAEIOU]$';
~~~


***

**Higher Than 75 Marks**

*Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.*

~~~
SELECT Name FROM Students WHERE Marks > 75 ORDER BY RIGHT(Name, 3), ID;
~~~

***

**Employee Names**

*Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.*

~~~
SELECT name FROM Employee ORDER BY name;
~~~

***

**Employee Salaries**

*Write a query that prints a list of employee names (i.e.: the name attribute) for employees in **Employee** having a salary greater than $2000  per month who have been employees for less than 10 months. Sort your result by ascending employee_id.*

~~~
SELECT name FROM Employee WHERE salary > 2000 AND months < 10 ORDER BY employee_id;
~~~

***
