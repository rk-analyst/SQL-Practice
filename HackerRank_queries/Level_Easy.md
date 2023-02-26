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
