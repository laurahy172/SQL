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
```
Use Case
Typically when a single column holds too much info from a raw data dump and needs to be parsed to make the data usable

LEFT(string, number_of_chars)

string: The string you are parsing

number_of_chars: How many characters you'd like to extract

# STRING_SPLIT

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
