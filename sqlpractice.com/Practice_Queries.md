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
```sql
-- Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'
select (MAX(weight) - MIN(weight)) AS diff
FROM patients
where last_name = 'Maroni'
;
```
```sql
-- Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.
select DAY(admission_date) AS day_of_month, COUNT(*) AS number_of_admissions
FROM admissions
group by day_of_month
order by number_of_admissions DESC;
```
```sql
-- Show all columns for patient_id 542's most recent admission_date.
select *
from admissions
WHERE patient_id = 542 
group by patient_id
HAVING admission_date = MAX(admission_date)
;
```
```sql
-- Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:
-- 1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
-- 2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.
select patient_id, attending_doctor_id, diagnosis
from admissions
WHERE (patient_id % 2 != 0 AND attending_doctor_id IN (1,5,19)) OR 
(attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3);
```
```sql
-- Show first_name, last_name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.
select first_name, last_name, count(a.patient_id) AS number_of_admissions
from doctors AS d 
JOIN admissions AS a ON d.doctor_id = a.attending_doctor_id
group by first_name, last_name;
```
```sql
-- For each doctor, display their id, full name, and the first and last admission date they attended.
select d.doctor_id, concat(first_name, " ", last_name) AS full_name, MIN(admission_date) AS earliest_admission, MAX(admission_date) AS latest_admission
FROM doctors AS d 
JOIN admissions AS a on a.attending_doctor_id = d.doctor_id
group by d.doctor_id, full_name;
```
```sql
-- Display the total amount of patients for each province. Order by descending.
select pn.province_name, COUNT(p.patient_id) AS total_patients
from province_names AS pn
JOIN patients AS p USING(province_id)
group by pn.province_name
order by total_patients DESC;
```
```sql
-- For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.
select concat(p.first_name, ' ', p.last_name) AS patient_full_name, a.diagnosis,
	concat(d.first_name, ' ', d.last_name) AS doctor_full_name
from patients AS p 
JOIN admissions AS a ON a.patient_id = p.patient_id
JOIN doctors AS d ON a.attending_doctor_id = d.doctor_id;
```
```sql
-- Display the number of duplicate patients based on their first_name and last_name.
select first_name, last_name, count(*) AS number_of_duplicates
from patients
GROUP BY first_name, last_name
having COUNT(*) > 1;
```
```sql
-- Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated.
-- Convert CM to feet by dividing by 30.48. Convert KG to pounds by multiplying by 2.205.
select concat(first_name, " ", last_name) AS full_name, ROUND(height/30.48,1) as heights_ft,
ROUND(weight*2.205,0) as weight_pounds, birth_date,
(case WHEN gender = 'M' then "Male" ELSE "Female" END) AS gender_nonabv
FROM patients;
```
```sql
-- Show all of the patients grouped into weight groups. Show the total amount of patients in each weight group. Order the list by the weight group decending.
-- For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.
select FLOOR(weight/10)*10 AS weight_group, count(*) AS number_of_patients
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC
;
```
```sql
-- Show patient_id, weight, height, isObese from the patients table. Display isObese as a boolean 0 or 1. 
-- Obese is defined as weight(kg)/(height(m)2) >= 30. weight is in units kg. height is in units cm.

SELECT patient_id, weight, height,
(CASE WHEN (weight/ POWER(height*0.01,2)) >= 30 THEN 1 ELSE 0 END) AS isObese
FROM patients
;
```
```sql
-- Show patient_id, first_name, last_name, and attending doctor's specialty. 
-- Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'
-- Check patients, admissions, and doctors tables for required information.

SELECT p.patient_id, p.first_name, p.last_name, d.specialty
FROM patients AS p 
JOIN admissions AS a ON p.patient_id = a.patient_id
JOIN doctors AS d ON a.attending_doctor_id = d.doctor_id
WHERE a.diagnosis = 'Epilepsy' AND d.first_name = 'Lisa'
;
```
```sql
/* All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.

The password must be the following, in order:
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date */

select DISTINCT p.patient_id, concat(p.patient_id, LEN(p.last_name),YEAR(p.birth_date)) AS password
FROM patients AS p
JOIN admissions AS a USING(patient_id)
;
```
```sql
-- Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance.
-- Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. 
-- Add up the admission_total cost for each has_insurance group.

select has_insurance, SUM(admission_cost) AS admission_total_cost 
FROM(select
(CASE WHEN patient_id%2 = 0 THEN "Yes" ELSE "No" END) AS has_insurance,
(CASE WHEN 
 (CASE WHEN patient_id%2 = 0 THEN "Yes" ELSE "No" END) = "Yes" THEN 10 ELSE 50 END) AS admission_cost
FROM admissions)
GROUP BY has_insurance
;
```
```sql
-- Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name
select pn.province_name 
FROM province_names AS pn
JOIN patients AS p USING(province_id)
GROUP BY pn.province_name
HAVING COUNT(CASE WHEN p.gender = 'M' THEN 1 END) > COUNT(CASE WHEN p.gender = 'F' THEN 1 END)
;
```
```sql
/* We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston' */
select *
FROM patients
WHERE first_name LIKE '%__r%' AND gender = 'F' AND MONTH(birth_date) IN (2,5,12) AND
(weight between 60 AND 80) AND patient_id % 2 != 0 AND city = 'Kingston'
;
```
```sql
-- Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.
SELECT CONCAT(
  ROUND(
    (
      select COUNT(*) 
      FROM patients 
      WHERE gender = 'M'
    )/ CAST(COUNT(*) AS float),
    4
  )* 100,
  '%'
) AS percentage
FROM patients
;
```
```sql
-- For each day display the total amount of admissions on that day. Display the amount changed from the previous date.
SELECT admission_date, count(admission_date) AS total_admissions, 
COUNT(admission_date)- LAG(COUNT(admission_date)) 
OVER(order by admission_date) AS change
FROM admissions
GROUP BY admission_date;
```
```sql
-- Sort the province names in ascending order in such a way that the province 'Ontario' is always on top.
select province_name
FROM province_names
ORDER BY (CASE WHEN province_name = 'Ontario' THEN 0 ELSE 1 END), province_name;
```
