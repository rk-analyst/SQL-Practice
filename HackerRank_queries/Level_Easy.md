# This file depicts the solutions of the EASY level queries on Hacker Rank: https://www.hackerrank.com/domains/sql

```sql
-- Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.
SELECT *
FROM city
WHERE countrycode = 'USA' AND population > 100000;
```
```sql
-- Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.
SELECT Name 
FROM City
WHERE CountryCode = 'USA' AND population > 120000;
```
```sql
-- Query all columns (attributes) for every row in the CITY table.
SELECT *
FROM City;
```
```sql
-- Query all columns for a city in CITY with the ID 1661.
SELECT*
FROM city
WHERE ID = 1661;
```
```sql
-- Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.
SELECT *
FROM City
WHERE CountryCode = 'JPN';
```
```sql
-- Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.
SELECT name
FROM city
WHERE CountryCode = 'JPN';
```
```sql
-- Query a list of CITY and STATE from the STATION table.
SELECT City, State
FROM Station;
```
```sql
-- Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.
SELECT DISTINCT city
FROM Station
WHERE ID % 2 = 0;
```
```sql
-- Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.
SELECT COUNT(*) - COUNT(DISTINCT City) AS difference
FROM Station;
```
```sql
/* Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). 
If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
Note: You can write two separate queries to get the desired output. It need not be a single query. */
SELECT city, LENGTH(city) AS name_length
FROM station
ORDER BY name_length, city
LIMIT 1;

SELECT city, LENGTH(city) AS name_length
FROM station
ORDER BY name_length DESC, city
LIMIT 1;
```
```sql
/* Query the following two values from the STATION table:
1. The sum of all values in LAT_N rounded to a scale of 2 decimal places.
2. The sum of all values in LONG_W rounded to a scale of 2 decimal places. */
SELECT ROUND(SUM(LAT_N),2), ROUND(SUM(LONG_W),2)
FROM Station;
```
```sql
-- Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.
SELECT DISTINCT City
FROM Station 
WHERE LEFT(city,1) IN ('A','E','I','O','U');
```
```sql
--  Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
SELECT DISTINCT City
FROM Station 
WHERE RIGHT(city,1) IN ('A','E','I','O','U');
```
```sql
-- Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.
SELECT DISTINCT City
FROM Station 
WHERE RIGHT(city,1) IN ('A','E','I','O','U') AND LEFT(city,1) IN ('A','E','I','O','U') ;
```
```sql
-- Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.
SELECT DISTINCT City
FROM Station 
WHERE LEFT(city,1) NOT IN ('A','E','I','O','U');
```
```sql
-- Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.
SELECT DISTINCT City
FROM Station 
WHERE RIGHT(city,1) NOT IN ('A','E','I','O','U');
```
```sql
-- Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.
SELECT DISTINCT CITY 
FROM station 
WHERE LEFT(CITY,1) NOT IN ('A','E','I','O','U') or RIGHT(CITY,1) NOT IN ('a','e','i','o','u');
```
```sql
-- Query the list of CITY names from STATION that either do not start with vowels and do not end with vowels. Your result cannot contain duplicates.
SELECT DISTINCT CITY 
FROM station 
WHERE LEFT(CITY,1) NOT IN ('A','E','I','O','U') AND RIGHT(CITY,1) NOT IN ('a','e','i','o','u');
```
```sql
-- Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. 
-- If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
SELECT name
FROM students
WHERE marks > 75
ORDER BY RIGHT(name,3), ID;
```
```sql
-- Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880  and less than 137.2345. Truncate your answer to 4 decimal places.

SELECT ROUND(SUM(LAT_N),4)
FROM station
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
```
```sql
-- Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.
SELECT ROUND(MAX(LAT_N),4)
FROM station
WHERE LAT_N < 137.2345;
```
```sql
-- Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Truncate your answer to 4 decimal places.
SELECT ROUND(LONG_W,4)
FROM Station
WHERE LAT_N = (SELECT MAX(LAT_N)
                FROM station
                WHERE LAT_N < 137.2345);
```
```sql
-- Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780. Round your answer to 4 decimal places.
SELECT ROUND(MIN(LAT_N),4)
FROM Station
WHERE LAT_N > 38.7780;
```
```sql
-- Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780 . Round your answer to 4 decimal places.
SELECT ROUND(LONG_W,4)
FROM Station
WHERE LAT_N = (SELECT MIN(LAT_N)
                FROM station
                WHERE LAT_N > 38.7780);

```
```sql
-- Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.
SELECT name
FROM employee
ORDER BY name;
```
```sql
/* Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month 
who have been employees for less than  months.  Sort your result by ascending employee_id. */
SELECT name
FROM employee
WHERE salary > 2000 AND months < 10;
```
```sql
-- Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.
-- Note: CITY.CountryCode and COUNTRY.Code are matching key columns.
SELECT city.name
FROM city
JOIN country ON CITY.CountryCode = COUNTRY.Code
WHERE country.Continent = 'Africa';
```
```sql
/* Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective 
average city populations (CITY.Population) rounded down to the nearest integer. */
SELECT country.continent, FLOOR(AVG(city.population)) AS avg_population
FROM country 
JOIN city ON city.countrycode = country.code
GROUP BY country.continent;
```
```sql

-- Query a count of the number of cities in CITY having a Population larger than 100000
SELECT COUNT(name)
FROM city
WHERE population > 100000;
```
```sql
-- Query the total population of all cities in CITY where District is California.
SELECT SUM(population)
FROM city
WHERE District = 'California';
```
```sql
-- Query the average population of all cities in CITY where District is California.
SELECT AVG(population)
FROM city
WHERE District = 'California';
```
```sql
-- Query the average population for all cities in CITY, rounded down to the nearest integer.
SELECT FLOOR(AVG(population))
FROM city;
```
```sql
-- Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.
SELECT SUM(Population)
FROM city
WHERE countrycode = 'JPN';
```
```sql
-- Query the difference between the maximum and minimum populations in CITY.
SELECT MAX(population) - MIN(population) AS difference
FROM city;
```
```sql
/* Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0
key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with 
any zeros removed), and the actual average salary.
Write a query calculating the amount of error (i.e.:  actual - miscalculated average monthly salaries), and round it up to the next integer. */
SELECT CEILING(AVG(salary) - AVG(REPLACE(salary, 0, ""))) AS amount_of_error
FROM employees;
```
```sql
/* We define an employee's total earnings to be their monthly  worked, and the maximum total earnings to be the maximum total earnings for any 
employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have 
maximum total earnings. Then print these values as 2 space-separated integers. */
SELECT salary*months AS max_earnings, COUNT(*)
FROM employee
WHERE salary*months = (SELECT MAX(salary*months) FROM employee)
GROUP BY max_earnings;
```
```sql
-- Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.
ELECT SUM(city.population)
FROM city
JOIN country on CITY.CountryCode = COUNTRY.Code 
WHERE country.continent = 'Asia';
```
```sql
/* Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:
Equilateral: It's a triangle with 3 sides of equal length.
Isosceles: It's a triangle with 2 sides of equal length.
Scalene: It's a triangle with 3 sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle. */
SELECT 
(CASE
    WHEN (A+B)<=C OR (A+C)<=B OR (B+C)<=A THEN 'Not A Triangle'
    WHEN A=B AND A=C THEN 'Equilateral'
    WHEN A=B OR A=C OR B=C THEN 'Isosceles'
    WHEN A<>B AND A<>C AND C<>B THEN 'Scalene' 
END) AS type_of_triangle
FROM triangles; 
```
```sql
/* P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

* * * * * 
* * * * 
* * * 
* * 
*
Write a query to print the pattern P(20). */
SET @var := 21;

SELECT REPEAT('* ', @var:= @var - 1)
FROM INFORMATION_SCHEMA.TABLES;
```
```sql
/* P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

* 
* * 
* * * 
* * * * 
* * * * *
Write a query to print the pattern P(20). */
SET @var := 0;

SELECT REPEAT('* ', @var:= @var + 1)
FROM INFORMATION_SCHEMA.TABLES
WHERE @var < 20;
```
```sql
