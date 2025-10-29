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


# CONCAT

# CAST

# POSITION

# STRPOS

# COALESCE

# NORMALIZATION
Relevant Definitions:
`Normalization`: Standardizing or “cleaning up a column” by transforming it in some way to make it ready for analysis. A few normalization techniques are below:
- Adjusting a column that includes multiple currencies to one common currency
- Adjusting the varied distribution of a column value by transforming it into a z-score
- Converting all price into a common metric (e.g., price per ounce)
