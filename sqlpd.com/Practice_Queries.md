# This file includes my queries from https://www.sqlpd.com/


```sql
/* An illegal site's servers were siezed in a recent operation. Please submit all subscribers details. */

SELECT *
FROM subscribers;
```

```sql
/* An illegal site's servers were siezed in a recent operation. Please submit all users last access times and emails details. */

SELECT lastaccess, email
FROM users;
```

```sql
/* Whitehat hacker has sent SQL PD exposed subscribers' details of shady site connected to various persons of interest. 
Please submit all subscribers' password hashes, usernames and names details. */

SELECT passwordhash, name, username
FROM subscribers;
```

```sql
/* A mailing list of an illegal online service was sent to the SQL PD hotline. Please submit all records number of promotions sent details. 
Please make sure there are no duplicates. */

SELECT DISTINCT promotionssent
FROM mailing_list;
```

```sql
/* A hacked site's subscribers details have surfaced on a darknet forum. 
Please submit all subscribers' details sorted by hashed password in ascending order. */

SELECT *
FROM subscribers
ORDER BY HashedPasswords;
```

```sql
/* An illegal site's servers were siezed in a recent operation. Please submit all users details sorted by first names in descending order. */
SELECT *
FROM subscribers;
ORDER BY FirstName DESC;
```

```sql
/* Whitehat hacker has sent SQL PD exposed subscribers' details of shady site connected to various persons of interest. 
Please submit all members' mailing address and member since dates sorted by mailing addresses in desc order.Please make sure there are no duplicates.*/

SELECT DISTINCT mailingaddress,membersince
FROM members 
ORDER BY mailingaddress DESC;
```

```sql
/* A mailing list of an illegal online service was sent to the SQL PD hotline. 
Please submit all records emails and join dates details sorted by join dates in ascending order and then by emails in ascending order.
Please make sure there are no duplicates. */

SELECT email, joined
FROM mailing_list
ORDER BY joined, email ASC;
```

```sql
/* A hacked site's subscribers details have surfaced on a darknet forum. 
Please submit top 3 members' details when sorted by full names in ascending order and then by password hashes in ascending order. */

SELECT *
FROM members
ORDER BY fullname, passwordhash ASC
LIMIT 3;
```

```sql
/* An illegal site's servers were siezed in a recent operation. 
Please submit top 20 users emails and family names' details when sorted by family names in descending order and then by emails in desc order.
Please make sure there are no duplicates. */

SELECT DISTINCT email, familyname
FROM members
ORDER BY name, comments DESC
LIMIT 20;
```

```sql
/* An illegal site's servers were siezed in a recent operation. 
Please submit all users details that have 39 downloads */

SELECT *
FROM users 
WHERE downloads = 39;
```

```sql
/* A hacked site's subscribers details have surfaced on a darknet forum. 
Please submit all members with a member since dates of May 31st 2022.*/

SELECT *
FROM members
WHERE membersince = '2022-05-31';
```

```sql
/* A hacked site's subscribers details have surfaced on a darknet forum. 
Please submit all subscribers with a subscribed since dates on or after March 16th 2021 but not after Jan 3rd 2022.*/
SELECT *
FROM subscribers
WHERE subscribedsince > '2021-03-16' AND subscribedsince < '2022-01-03';
```
