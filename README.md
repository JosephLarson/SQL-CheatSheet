# SQL-CheatSheet  
SQL-lite CheatSheet using examples learned from CodeAcademy SQL course.  
SQL -- Structured Query Language

## Basic Vocab
Relational database -- database that organizes information into one or more tables.  
Table -- a collection of data organized into rows and columns.    
Entity -- Person, place, thing, or event. Distinguishable, unique, and distinct.  
Attribute -- A characteristic of an entity.  
Relationship -- Describes association among entities
* One-to-many -- Customer to invoices  
* Many-to-many -- Student to classes  
* One-to-one -- Manager to store

Primary Key -- A column (or set of columns) whose values uniquely identify every row in a table.   
Foreign Key -- One or more columns that can be used together to identify a single row in another table.  

## Main Commands
SELECT -- Needed to query/search for data from the database.  
FROM -- Indicates the table where the search will be made.  
WHERE -- Its used to dfine the rows, in which the search will be carried.  
ORDER BY -- This is the only way to sort the results in SQL. Otherwise retured in random order.  
  
## Statement Commands  

| Command       | Purpose                                                  | Example                                                                     |
| ------------- | -------------                                            | -----                                                                       |
| CREATE TABLE  | Statment to create a new table in database               | CREATE TABLE table_name ( column1 datatype, column2 datatype, ... );        |
| INSERT INTO   | Clause to add a new row to a table                       | INSERT INTO celebs (id, name, age)                                          |
| VALUES        | Clause that indicates the data being inserted            | VALUES (1, 'Justin Bieber', 22);                                            |
| SELECT        | Clause to query data from database                       | SELECT name FROM celebs;                                                    |
| *             | Wild card symbol to select every item in column          | SELECT * FROM celebs;                                                       |
| ALTER TABLE   | Clause that modifys a columns in the table               | ALTER TABLE celebs ADD COLUMN twitter_handle TEXT;                          |
| UPDATE        | Clause that modifys a row in the table                   | **UPDATE** celebs SET twitter_handle = '@taylorswift13' WHERE id = 4;       |
| SET           | Clause to indicate column or row to edit                 | UPDATE celebs **SET** twitter_handle = '@taylorswift13' WHERE id = 4;       |
| WHERE         | Filters the result set to include certain conditions     | UPDATE celebs SET twitter_handle = '@taylorswift13' **WHERE** id = 4;       |
| DELETE FROM   | Clause that lets you delete rows from a table            | DELETE FROM celebs WHERE twitter_handle IS NULL;                            |
| AS            | Rename a column or table with an alias.                  | SELECT name AS 'Titles' FROM movies;                                        |
| DISTINCT      | Used to return unique values in the output               | SELECT DISTINCT genre FROM movies;                                          |
| LIKE          | Used with WHERE to search for specific pattern           | SELECT * FROM movies WHERE name LIKE 'Se_en';                               |
| %             | Used to match 0 or more missing letters in a pattern     | SELECT * FROM movies WHERE name LIKE 'A%';                                  |
| 'A%'          | Find all that start with A                               | SELECT * FROM movies WHERE name LIKE 'A%';                                  |
| '%a'          | Find all that end with a                                 | SELECT * FROM movies WHERE name LIKE '%a';                                  |
| '%man%'       | Find all that contains the word 'man'                    | SELECT * FROM movies WHERE name LIKE '%man%';                               |
| IS NULL       | How to check for a value of NULL (Can't use = NULL)      | SELECT name FROM movies WHERE imdb_rating IS NULL;                          |
| IS NOT NULL   | How to check for a value of NOT NULL (Can't use != NULL) | SELECT name FROM movies WHERE imdb_rating IS NOT NULL;                      |
| BETWEEN       | Filter a result within a certain *range*                 | SELECT * FROM movies WHERE year BETWEEN 1990 AND 1999;                      |
| AND           | Used for multiple conditions for a WHERE clause (All)    | SELECT * FROM movies WHERE year BETWEEN 1990 AND 1999 AND genre = 'romance';|
| OR            | Used for multple conditions for a WHERE clause (Any)     | SELECT * FROM movies WHERE year > 2014 OR genre = 'action';                 |
| ORDER BY      | Sort the result indicated                                | SELECT * FROM movies ORDER BY name;                                         |
| DESC          | Used with ORDER BY to sort in descending order           | SELECT * FROM movies WHERE imbd_rating > 8 ORDER BY year DESC;              |
| ASC           | Used with ORDER BY to sort in descending order           | SELECT * FROM movies WHERE imbd_rating > 8 ORDER BY year ASC;               |
| LIMIT         | Used to limit the number of results returned from query  | SELECT * FROM movies LIMIT 10;                                              |

## Aggregate Functions
| Function      | Purpose                                                  | Example                                                                     |
| ------------- | -------------                                            | -----                                                                       |
| COUNT()       | Count the number of rows                                 | SELECT COUNT(*) FROM fake_apps WHERE price = 0;                             |
| SUM()         | The sum of the values in a column                        | SELECT SUM(downloads) FROM fake_apps;                                       |
| MAX()         | The largest value                                        | SELECT MAX(downloads) FROM fake_apps;                                       |
| MIN()         | The smallest value                                       | SELECT MIN(downloads) FROM fake_apps;                                       |
| AVG()         | The average of the values in a column                    | SELECT AVG(price) FROM fake_apps;                                           |
| ROUND()       | Round the values in the column                           | SELECT ROUND(price, 0) FROM fake_apps;  (rounds column to number of decimal provided) |
| GROUP BY      | Group by a certain characteristic                        | SELECT category, SUM(downloads) FROM fake_apps GROUP BY category;           |
| HAVING        | Limit results of a query based off a aggregate property  | SELECT price, ROUND(AVG(downloads)), COUNT(*) FROM fake_apps GROUP BY price HAVING COUNT(price) > 10; |

## Multiple Tables
- JOIN will combine rows from different tables if the join condition is true.  
- LEFT JOIN will return every row in the left table, and if the join condition is not met, NULL values are used to fill in the columns from the right table.  
- Primary key is a column that serves a unique identifier for the rows in the table.  
- Foreign key is a column that contains the primary key to another table.  
- CROSS JOIN lets us combine all rows of one table with all rows of another table.  
- UNION stacks one dataset on top of another.  
- WITH allows us to define one or more temporary tables that can be used in the final query.  


## Constraints  
CREATE TABLE celebs (  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   id INTEGER PRIMARY KEY,   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   name TEXT UNIQUE,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   date_of_birth TEXT NOT NULL,  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   date_of_death TEXT DEFAULT 'Not Applicable'  
);  
   
| Constraints | Purpose |
| ----------- | ------- |
| PRIMARY KEY | PRIMARY KEY columns can be used to uniquely idetify the row. Prevents the ability to add another row with a identical value.       |
| UNIQUE      | UNIQUE columns have a different value for every row. Similar to PRIMARY KEY except a table can have many different UNIQUE columns. |
| NOT NULL    | NOT NULL columns must have a value. Attempts to insert a row without a value for NOT NULL will cause a constraint violation.       |
| DEFAULT     | DEFAULT columns take an additonal argument taht will be the assumed value for an inserted row if new row does not specify a value. |  

## Case Statements  
SELECT name,  
&nbsp;&nbsp;  CASE  
&nbsp;&nbsp;&nbsp;&nbsp;   WHEN imdb_rating > 8 THEN 'Fantastic'  
&nbsp;&nbsp;&nbsp;&nbsp;   WHEN imdb_rating > 6 THEN 'Poorly Received'  
&nbsp;&nbsp;&nbsp;&nbsp;   ELSE 'Avoid at All Costs'  
&nbsp;&nbsp;  END AS 'Review'   
FROM movies;    



    
                                                                                            
