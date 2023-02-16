## This file contains all the queries practiced through https://www.w3schools.com/sql/

```sql
-- Insert the missing statement to get all the columns from the Customers table.

SELECT * FROM Customers;
```
```sql
 -- Write a statement that will select the City column from the Customers table.

SELECT city FROM Customers;
```
```sql
-- Select all the different values from the Country column in the Customers table.

SELECT DISTINCT Country FROM Customers;
```
```sql
-- Select all records where the City column has the value "Berlin".
SELECT * FROM Customers
WHERE city = "Berlin";
```
```sql
-- Use the NOT keyword to select all records where City is NOT "Berlin".
SELECT * FROM Customers
WHERE NOT city= 'Berlin';
```
```sql
-- Select all records where the CustomerID column has the value 32.
SELECT * FROM Customers
WHERE CustomerID = 32;
```
```sql
-- Select all records where the City column has the value 'Berlin' and the PostalCode column has the value 12209.
SELECT
 * FROM Customers
WHERE
 City = 'Berlin'
AND
PostalCode
 = 12209;
```
```sql
 -- Select all records where the City column has the value 'Berlin' or 'London'.
SELECT
 * FROM Customers
WHERE
 City = 'Berlin'
OR
City= 'London';
```
```sql
-- Select all records from the Customers table, sort the result alphabetically by the column City.
SELECT * FROM Customers
ORDER BY City
;
```
```sql
-- Select all records from the Customers table, sort the result reversed alphabetically by the column City.
SELECT * FROM Customers
ORDER BY City DESC
;
```
```sql
-- Select all records from the Customers table, sort the result alphabetically, first by the column Country, then, by the column City.
SELECT * FROM Customers
ORDER BY Country,City;
```
```sql
-- Insert a new record in the Customers table.

INSERT INTO
 Customers 
(
CustomerName, 
Address, 
City, 
PostalCode,
Country
)
VALUES
 
(
'Hekkan Burger',
'Gateveien 15',
'Sandnes',
'4306',
'Norway'
);
```
```sql
-- Select all records from the Customers where the PostalCode column is empty.
SELECT * FROM Customers
WHERE 
PostalCode IS NULL;
```
```sql
-- Select all records from the Customers where the PostalCode column is NOT empty.
SELECT * FROM Customers
WHERE 
PostalCode IS NOT NULL;
```
```sql
-- Update the City column of all records in the Customers table.
UPDATE Customers 
SET City = 'Oslo';
```
```sql
-- Set the value of the City columns to 'Oslo', but only the ones where the Country column has the value "Norway".
UPDATE Customers 
SET City = 'Oslo'
WHERE Country = 'Norway';
```
