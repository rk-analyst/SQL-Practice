# This file includes my queries from https://www.sql-practice.com/
```sql
-- Show first name, last name, and gender of patients who's gender is 'M'
SELECT first_name, last_name, gender
FROM patients
WHERE gender = "M";
```
```sql
-- Show first name and last name of patients who does not have allergies. (null)
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;
```
```sql
--Show first name of patients that start with the letter 'C'
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';
```
```sql
-- Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
SELECT first_name, last_name
FROM patients
WHERE weight between 100 AND 120;
```
```sql
-- Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
UPDATE patients
SET allergies = 'NKA' 
WHERE allergies IS null;
```
```sql
-- Show first name and last name concatinated into one column to show their full name.
SELECT concat(first_name,' ', last_name) AS full_name
FROM patients;
```
```sql
-- Show first name, last name, and the full province name of each patient. Example: 'Ontario' instead of 'ON'
select first_name, last_name, pn.province_name
FROM patients as p
INNER JOIN province_names AS pn USING(province_id);
```
```sql
-- Show how many patients have a birth_date with 2010 as the birth year.
select COUNT(*)
FROM patients
WHERE YEAR(birth_date) 	= 2010;
```
```sql
-- Show the first_name, last_name, and height of the patient with the greatest height.
select first_name, last_name, MAX(height) AS max_ht
from patients
group by first_name, last_name
ORDER BY max_ht DESC
LIMIT 1;
```
```sql
-- Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000
select *
FROM patients
WHERE patient_id IN (1,45,534,879,1000);
```
```sql
-- Show the total number of admissions
select COUNT(*)
FROM admissions
;
```
```sql
-- Show all the columns from admissions where the patient was admitted and discharged on the same day.
select *
FROM admissions
WHERE admission_date = discharge_date
;
```
```sql
-- Show the patient id and the total number of admissions for patient_id 579.
select patient_id, COUNT(*)
FROM admissions
WHERE patient_id = 579
group by patient_id
;
```
```sql
-- Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?
select distinct city
FROM patients
where province_id = 'NS'
;
```
```sql
-- Write a query to find the first_name, last name and birth date of patients who have height more than 160 and weight more than 70
select first_name, last_name, birth_date
from patients
where height > 160 AND weight > 70
;
```
```sql
-- Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null
select first_name, last_name, allergies
FROM patients
WHERE city = 'Hamilton' AND allergies IS NOT null
;
```
```sql
-- Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). 
-- Show the result order in ascending by city.
SELECT DISTINCT city
FROM patients
WHERE (city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%')
ORDER BY city
;
```
```sql
-- Show unique birth years from patients and order them by ascending.
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year
;
```
```sql
-- Show unique first names from the patients table which only occurs once in the list.
-- For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. 
-- If only 1 person is named 'Leo' then include them in the output.
SELECT DISTINCT first_name
FROM patients
group by first_name
HAVING COUNT(first_name) = 1
;
```
```sql
-- Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
SELECT patient_id, first_name
FROM patients
WHERE (first_name LIKE 'S%' AND first_name LIKE '%s') AND len(first_name) >= 6
;
```
```sql
-- Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.
SELECT patient_id, first_name, last_name
FROM patients AS p
INNER JOIN admissions AS a USING(patient_id)
WHERE diagnosis = 'Dementia'
;
```
```sql
-- Display every patient's first_name. Order the list by the length of each name and then by alphbetically
SELECT  first_name
FROM patients 
ORDER BY LEN(first_name), first_name
;
```
```sql
-- Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.
SELECT
  (select COUNT(*) from patients WHERE gender = 'M') AS male_count,
    (select COUNT(*) from patients WHERE gender = 'F') AS female_count;
```
```sql
-- Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. 
-- Show results ordered ascending by allergies then by first_name then by last_name.
select first_name, last_name, allergies
from patients
WHERE allergies = 'Penicillin' OR allergies = 'Morphine'
ORDER BY allergies,first_name, last_name
```
```sql
-- Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.
select patient_id, diagnosis
from admissions
group by patient_id, diagnosis
having count(diagnosis) > 1;
```
```sql
-- Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.
select city, COUNT(*) AS total_patients
FROM patients
group by city
order by total_patients DESC, city;
```
```sql
-- Show first name, last name and role of every person that is either patient or doctor. The roles are either "Patient" or "Doctor"
select first_name, last_name, 'Patient' AS role
FROM patients
UNION ALL
select first_name, last_name, 'Doctor' AS role
FROM doctors;
```
```sql
-- Show all allergies ordered by popularity. Remove NULL values from query.
select allergies, COUNT(*) AS popularity
FROM patients
WHERE allergies IS NOT NULL
group by allergies
order by popularity desc
;
```
```sql
-- Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.
select first_name, last_name, birth_date
from patients
WHERE YEAR(birth_date) between 1970 AND 1979
order by birth_date
;
```
```sql
-- We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. 
-- Separate the last_name and first_name with a comma. Order the list by the first_name in decending order. EX: SMITH,jane

select concat(UPPER(last_name), ',', lower(first_name)) AS full_name
FROM patients
order by first_name desc
;
```
```sql
-- Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.
select province_id, SUM(height)
FROM patients
group by province_id
having SUM(height) >= 7000
;
```
