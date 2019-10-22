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

**Weather Observation Station 5**

*Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.*

~~~
SELECT TOP 1 CITY, LEN(CITY) FROM STATION ORDER BY LEN(CITY) ASC;
SELECT TOP 1 CITY, LEN(CITY) FROM STATION ORDER BY LEN(CITY) DESC;
~~~
