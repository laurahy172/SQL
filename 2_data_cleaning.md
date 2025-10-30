The following set of methods cover three types of data cleaning techniques: parsing information, returning where information lives, and changing the data type of the information.

- Left: Extracts a number of characters from a string starting from the left
- Right: Extracts a number of characters from a string starting from the right
- Substr: Extracts a substring from a string (starting at any position)
- Position: Returns the position of the first occurrence of a substring in a string
- Strpos: Returns the position of a substring within a string
- Concat: Adds two or more expressions together
- Cast: Converts a value of any type into a specific, different data type
- Coalesce: Returns the first non-null value in a list

# LEFT, RIGHT, SUBSTR
<img width="665" height="260" alt="image" src="https://github.com/user-attachments/assets/992cbd27-30d0-4ff0-9e38-3094d9568c4b" />
<img width="674" height="257" alt="image" src="https://github.com/user-attachments/assets/8308213a-6b36-41ba-9691-1732c937d109" />
<img width="674" height="257" alt="image" src="https://github.com/user-attachments/assets/37cee23b-2b09-4a5a-9327-4c1cde7582cf" />
<img width="674" height="259" alt="image" src="https://github.com/user-attachments/assets/549b654c-4e5b-4742-b8f9-4376b7009060" />

Syntax
- Left: Extracts a # of characters from a string starting from the left
- Right: Extracts a # of characters from a string starting from the right

```sql 
LEFT(student_information, 8) AS student_id
RIGHT(student_information, 6) AS salary

select count(*), right(website,3) as type_of_website from accounts group by right(website,3) 
select count(*), left(name,1) as company_initial from accounts group by left(name,1)


SELECT RIGHT(website, 3) AS domain, COUNT(*) num_companies
FROM accounts
GROUP BY 1
ORDER BY 2 DESC;

SELECT LEFT(UPPER(name), 1) AS first_letter, COUNT(*) num_companies
FROM accounts
GROUP BY 1
ORDER BY 2 DESC;

SELECT SUM(num) nums, SUM(letter) letters
FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9') 
                          THEN 1 ELSE 0 END AS num, 
            CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9') 
                          THEN 0 ELSE 1 END AS letter
         FROM accounts) t1;


SELECT SUM(vowels) vowels, SUM(other) other
FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U') 
                           THEN 1 ELSE 0 END AS vowels, 
             CASE WHEN LEFT(UPPER(name), 1) IN ('A','E','I','O','U') 
                          THEN 0 ELSE 1 END AS other
            FROM accounts) t1;

```
Use Case
Typically when a single column holds too much info from a raw data dump and needs to be parsed to make the data usable

LEFT(string, number_of_chars)

string: The string you are parsing

number_of_chars: How many characters you'd like to extract


----
## Q1
SELECT SUM(num) nums, SUM(letter) letters
FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9')
THEN 1 ELSE 0 END AS num,
CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9')
THEN 0 ELSE 1 END AS letter
FROM accounts) t1; 如果写 in (1,2,3,4,5...) 不是 ('1','2','3','4',...) 可以吗

A:
1. In SQL, when you are using the IN clause to check for values, the data types of the values you are comparing must match the data type of the column you are checking against.
2. In your query, you are using LEFT(UPPER(name), 1), which extracts the first character of the name column and converts it to uppercase. If the name column contains string values, you should compare against string representations of the numbers, like this:
3. CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9') 

If you were to use numeric values instead, like this:
CASE WHEN LEFT(UPPER(name), 1) IN (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
This would not work correctly because you are comparing a string (the first character of the name) against numeric values. The comparison would not yield the expected results, as the types do not match.
-----






# STRING_SPLIT
<img width="691" height="280" alt="image" src="https://github.com/user-attachments/assets/6fa35dc8-37a5-4b7c-923a-8485015caafb" />

```sql
SELECT STRING_TO_ARRAY('apple,banana,cherry', ',') AS fruits; -- PostgreSQL
STRING_SPLIT('apple,banana,cherry', ','); -- sql server
SELECT (STRING_TO_ARRAY('apple,banana,cherry', ','))[2] AS second_part;
```

# CONCAT
<img width="646" height="274" alt="image" src="https://github.com/user-attachments/assets/dc895c7a-b089-46b2-b97d-62a6b9549e75" />
<img width="646" height="273" alt="image" src="https://github.com/user-attachments/assets/1ae6c306-71e5-4368-a688-aaaefa13a057" />

```sql
select concat(s.id,'_',r.name) as emp_id_region from sales_reps as s join region r on s.region_id = r.id
select concat(account_id,'_',channel,'_', count(*)) from web_events group by account_id, channel order by count(*) DESC
SELECT NAME, CONCAT(LAT, ', ', LONG) COORDINATE, CONCAT(LEFT(PRIMARY_POC, 1), RIGHT(PRIMARY_POC, 1), '@', SUBSTR(WEBSITE, 5)) EMAIL FROM ACCOUNTS;

WITH T1 AS (
SELECT ACCOUNT_ID, CHANNEL, COUNT(*) 
FROM WEB_EVENTS
GROUP BY ACCOUNT_ID, CHANNEL
ORDER BY ACCOUNT_ID
)
SELECT CONCAT(T1.ACCOUNT_ID, '_', T1.CHANNEL, '_', COUNT)
FROM T1;
```


# CAST
<img width="635" height="238" alt="image" src="https://github.com/user-attachments/assets/3202f95b-a9e2-4d97-8310-c1169b451ea1" />
<img width="661" height="260" alt="image" src="https://github.com/user-attachments/assets/1e6807fd-18d5-45e2-a4ee-16684b2ffef5" />
<img width="427" height="338" alt="image" src="https://github.com/user-attachments/assets/694ae255-352d-420a-9a03-21080904381a" />
<img width="454" height="245" alt="image" src="https://github.com/user-attachments/assets/49a5a6ca-1fc0-483f-b5b0-a4fb6e2e111d" />
<img width="613" height="602" alt="image" src="https://github.com/user-attachments/assets/a5c9181b-aa50-433f-ba22-e914ab71b89c" />
<img width="710" height="515" alt="image" src="https://github.com/user-attachments/assets/ac7bd4f4-f5d5-423f-a207-deaad5fad858" />
<img width="717" height="397" alt="image" src="https://github.com/user-attachments/assets/b4e95bb9-ddc5-4099-aa1e-61e3497610ce" />
🔹所以这句话「|| 和 :: 是 CONCAT() 和 CAST() 的简写」——
在 PostgreSQL 里确实如此；但在 MySQL 或 SQL Server 里就不完全对。

```sql
select  concat(substr(date,7,4),'_',substr(date,1,2),'_',substr(date,4,2))   from sf_crime_data limit 10
SELECT date orig_date, (SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) || '-' || SUBSTR(date, 4, 2)) new_date
FROM sf_crime_data;
SELECT date AS orig_date, CAST((SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) || '-' || SUBSTR(date, 4, 2)) AS DATE) new_date
FROM sf_crime_data;
SELECT date orig_date, (SUBSTR(date, 7, 4) || '-' || LEFT(date, 2) || '-' || SUBSTR(date, 4, 2))::DATE AS new_date
FROM sf_crime_data;
```
Observe how we use || to concatenate strings and :: to cast data types in our queries. These operators serve as shorthand alternatives to CONCAT() and CAST(), simplifying syntax while performing the same functions.
Execute these solutions in the below workspace.


# POSITION
<img width="593" height="226" alt="image" src="https://github.com/user-attachments/assets/f94aeb90-79fd-4f85-991f-d3a6d3bf986d" />
must the info consistently locate in the same position
<img width="580" height="206" alt="image" src="https://github.com/user-attachments/assets/eeee1939-4055-4d63-8589-09030dfd8641" />
<img width="615" height="245" alt="image" src="https://github.com/user-attachments/assets/6bc7a53c-2375-4cfe-9046-35b00e14d52b" />
<img width="490" height="201" alt="image" src="https://github.com/user-attachments/assets/362eaa70-d2af-4037-8201-79b927aa91e2" />
<img width="557" height="221" alt="image" src="https://github.com/user-attachments/assets/c7620e9c-eb84-45c8-99a4-37682ddc04dc" />


The following advanced cleaning functions are used less often but are good to understand to complete your holistic understanding of data cleaning in SQL. For the most part, these functions are used to return the position of information and help you work with NULLs.
- Position/Strpos: Used to return the position of information to identify where relevant information is held in a string to then extract across all records
- Coalesce: Used to return the first non-null value that’s commonly used for normalizing data that’s stretched across multiple columns and includes NULLs.


# STRPOS
<img width="638" height="266" alt="image" src="https://github.com/user-attachments/assets/69eec05b-1c6f-4ad7-a241-bbc1990a36ac" />

```sql
SELECT LEFT(primary_poc, STRPOS(primary_poc, ' ') -1 ) first_name, 
RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name
FROM accounts;

with tab as (select *, POSITION(' ' in primary_poc) as surname_start_position from accounts limit 20)
select left(primary_poc,surname_start_position-1) as first_name, substr(primary_poc, surname_start_position) as last_name from tab


WITH t1 AS (
 SELECT LEFT(primary_poc,
   STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
 FROM accounts)
SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', name, '.com')
FROM t1;

WITH t1 AS (
 SELECT LEFT(primary_poc,     
   STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
 FROM accounts)
SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', REPLACE(name, ' ', ''), '.com') --- REPLACE!!!
FROM  t1;

WITH t1 AS (
 SELECT LEFT(primary_poc,     STRPOS(primary_poc, ' ') -1 ) first_name,  RIGHT(primary_poc, LENGTH(primary_poc) - STRPOS(primary_poc, ' ')) last_name, name
 FROM accounts)
SELECT first_name, last_name, CONCAT(first_name, '.', last_name, '@', name, '.com'), LEFT(LOWER(first_name), 1) || RIGHT(LOWER(first_name), 1) || LEFT(LOWER(last_name), 1) || RIGHT(LOWER(last_name), 1) || LENGTH(first_name) || LENGTH(last_name) || REPLACE(UPPER(name), ' ', '')
FROM t1;
```
We would also like to create an initial password, which they will change after their first log in. The first password will be the first letter of the primary_poc's first name (lowercase), then the last letter of their first name (lowercase), the first letter of their last name (lowercase), the last letter of their last name (lowercase), the number of letters in their first name, the number of letters in their last name, and then the name of the company they are working with, all capitalized with no spaces.


# COALESCE
<img width="615" height="245" alt="image" src="https://github.com/user-attachments/assets/4274905f-133b-4906-891c-b569de3152ae" />
<img width="485" height="225" alt="image" src="https://github.com/user-attachments/assets/3e34fee5-cda6-4adb-b330-c6a238b943a8" />
<img width="623" height="251" alt="image" src="https://github.com/user-attachments/assets/dad68064-1f9e-4866-8d25-00be5e8133ad" />
return the first non-null values as the annual income column

# NORMALIZATION
Relevant Definitions:
`Normalization`: Standardizing or “cleaning up a column” by transforming it in some way to make it ready for analysis. A few normalization techniques are below:
- Adjusting a column that includes multiple currencies to one common currency
- Adjusting the varied distribution of a column value by transforming it into a z-score
- Converting all price into a common metric (e.g., price per ounce)
