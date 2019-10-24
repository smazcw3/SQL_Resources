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

**Weather Observation Station 4**

*Let N be the number of CITY entries in STATION, and let N' be the number of distinct **CITY** names in **STATION**; query the value of N - N' from **STATION**. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.*

~~~
SELECT COUNT(CITY) - COUNT(DISTINCT(CITY)) FROM STATION;
~~~

***

**Weather Observation Station 5**

*Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.*

~~~
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY), CITY LIMIT 1)
UNION
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY LIMIT 1);
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

**Type of Triangle**

*Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:*

- Equilateral: It's a triangle with  sides of equal length.
- Isosceles: It's a triangle with  sides of equal length.
- Scalene: It's a triangle with  sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

~~~
SELECT
CASE WHEN A + B <= C OR B + C <= A OR A + C <= B THEN "Not A Triangle"
WHEN A = B AND B = C AND A = C THEN "Equilateral"
WHEN A != B AND B != C AND A != C THEN "Scalene"
WHEN A = B OR B = C OR A = C THEN "Isosceles" 
END
FROM TRIANGLES;
~~~
***

**Asian Population**

*Given the **CITY** and **COUNTRY** tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.*

***Note:** CITY.CountryCode and COUNTRY.Code are matching key columns.*

~~~
SELECT SUM(CITY.POPULATION) FROM CITY LEFT JOIN COUNTRY ON CITY.CountryCode = COUNTRY.Code WHERE CONTINENT="Asia";
~~~

***

**African Cities**

*Given the **CITY** and **COUNTRY** tables, query the names of all cities where the CONTINENT is 'Africa'.*

***Note:** CITY.CountryCode and COUNTRY.Code are matching key columns.*

~~~
SELECT CITY.NAME FROM CITY LEFT JOIN COUNTRY ON CITY.CountryCode = COUNTRY.Code WHERE CONTINENT="Africa";
~~~

***

**Average Population of Each Continent**

*Given the **CITY** and **COUNTRY** tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.*

*Note: CITY.CountryCode and COUNTRY.Code are matching key columns.*

~~~
SELECT COUNTRY.Continent, FLOOR(AVG(CITY.POPULATION)) 
FROM CITY INNER JOIN COUNTRY ON CITY.CountryCode = COUNTRY.Code 
GROUP BY COUNTRY.CONTINENT;
~~~

***

**Contest Leaderboard**

*You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!*

*The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of 0 from your result.*

~~~

~~~

***

**Revising Aggregations - The Sum Function**

*Query the total population of all cities in **CITY** where District is **California**.*

~~~
SELECT SUM(POPULATION)FROM CITY WHERE DISTRICT="California";
~~~

***

**Revising Aggregations - The Count Function**

*Query a count of the number of cities in CITY having a Population larger than 100,000.*

~~~
SELECT COUNT(*) FROM CITY WHERE POPULATION > 100000;
~~~

***

**Revising Aggregations - Averages**

*Query the average population of all cities in **CITY** where District is **California**.*

~~~
SELECT AVG(POPULATION) FROM CITY WHERE DISTRICT = "California";
~~~

***

**Average Population**

*Query the average population for all cities in **CITY**, rounded down to the nearest integer.*

~~~
SELECT ROUND(AVG(POPULATION)) FROM CITY;
~~~

***

**Japan Population**

*Query the sum of the populations for all Japanese cities in **CITY**. The COUNTRYCODE for Japan is **JPN**.*

~~~
SELECT SUM(POPULATION) FROM CITY WHERE COUNTRYCODE="JPN";
~~~

***

**Population Density Difference**

*Query the difference between the maximum and minimum populations in **CITY**.*

~~~
SELECT MAX(POPULATION) - MIN(POPULATION) FROM CITY;
~~~

***

**Weather Observation Station 2**

*Query the following two values from the STATION table:*

*1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.*

*2. The sum of all values in LONG_W rounded to a scale of 2 decimal places.*

~~~
SELECT ROUND(SUM(LAT_N),2), ROUND(SUM(LONG_W),2) FROM STATION;
~~~

***

**Weather Observation Station 13**

*Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.*

~~~
SELECT ROUND(SUM(LAT_N),4) FROM STATION WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
~~~

***

**Weather Observation Station 14**

*Query the greatest value of the Northern Latitudes (LAT_N) from **STATION** that is less than 137.2345. Truncate your answer to 4 decimal places.*

~~~
SELECT ROUND(MAX(LAT_N),4) FROM STATION WHERE LAT_N < 137.2345;
~~~

***

**Weather Observation Station 15**

*Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in **STATION** that is less than 137.2345. Round your answer to 4 decimal places.*

~~~
SELECT ROUND(LONG_W, 4) FROM STATION WHERE LAT_N < 137.2345 ORDER BY LAT_N DESC LIMIT 1;
~~~

***

**Weather Observation Station 16**

*Query the smallest Northern Latitude (LAT_N) from **STATION** that is greater than 38.7780. Round your answer to 4 decimal places.*

~~~
SELECT ROUND(LAT_N, 4) FROM STATION WHERE LAT_N > 38.7780 ORDER BY LAT_N LIMIT 1;
~~~

***

**Weather Observation Station 17**

*Query the Western Longitude (LONG_W) where the smallest Northern Latitude (LAT_N) in **STATION** is greater than 38.7780. Round your answer to 4 decimal places.*

~~~
SELECT ROUND(LONG_W, 4) FROM STATION WHERE LAT_N > 38.7780 ORDER BY LAT_N LIMIT 1;
~~~

***

**Weather Observation Station 18**

*Consider P1(a,b) and P2(c,d) to be two points on a 2D plane*.

 - **a** happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 
 - **b** happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 
 - **c** happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 
 - **d** happens to equal the maximum value in Western Longitude (LONG_W in STATION).
 
*Query the Manhattan Distance between points P1 and P2 and round it to a scale of 4 decimal places.*

~~~
SELECT ROUND(ABS(MIN(LAT_N) - MAX(LAT_N)) + ABS(MIN(LONG_W) - MAX(LONG_W)), 4) FROM STATION;
~~~

***

**Weather Observation Station 19**

*Consider P1 and P2 to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.*

*Query the Euclidean Distance between points P1 and P2 and format your answer to display 4 decimal digits.*

~~~
SELECT ROUND(SQRT(POW(MIN(LAT_N) - MAX(LAT_N),2) + POW(MIN(LONG_W) - MAX(LONG_W),2)), 4) FROM STATION;
~~~

***

**Weather Observation Station 20**

*A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from **STATION** and round your answer to 4 decimal places.*

~~~

~~~

***















