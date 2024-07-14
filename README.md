# Database Schema: Movie Database

## Table: Movies
- `movieId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `title` (VARCHAR(100))
- `releaseYear` (YEAR)
- `duration` (INT) - duration in minutes
- `rating` (DECIMAL(3,1)) - for example, 7.8

## Table: Actors
- `actorId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `firstName` (VARCHAR(50))
- `lastName` (VARCHAR(50))
- `birthdate` (DATE)

## Table: Directors
- `directorId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `firstName` (VARCHAR(50))
- `lastName` (VARCHAR(50))
- `birthdate` (DATE)

## Table: Genres
- `genreId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `genreName` (VARCHAR(50))

## Table: MovieActors
- `movieActorId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `movieId` (INT, FOREIGN KEY REFERENCES Movies(movieId))
- `actorId` (INT, FOREIGN KEY REFERENCES Actors(actorId))

## Table: MovieDirectors
- `movieDirectorId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `movieId` (INT, FOREIGN KEY REFERENCES Movies(movieId))
- `directorId` (INT, FOREIGN KEY REFERENCES Directors(directorId))

## Table: MovieGenres
- `movieGenreId` (INT, AUTO_INCREMENT, PRIMARY KEY)
- `movieId` (INT, FOREIGN KEY REFERENCES Movies(movieId))
- `genreId` (INT, FOREIGN KEY REFERENCES Genres(genreId))

## Relationships
- One-to-Many: Each movie can have multiple actors, directors, and genres.
- Many-to-Many: Each actor can act in multiple movies, and each movie can have multiple actors. Each director can direct multiple movies, and each movie can have multiple directors. Each movie can belong to multiple genres, and each genre can apply to multiple movies.

# MySQL Data Types

MySQL supports a variety of data types in several categories: numeric types, date and time types, string (character and byte) types, spatial types, and JSON type. Below is a brief overview of each category and its data types:

## Numeric Types
- `INT`: A normal-size integer that can be signed or unsigned.
- `BIGINT`: A large integer that can be signed or unsigned.
- `TINYINT`: A very small integer that can be signed or unsigned.
- `DECIMAL(M, D)`: A fixed-point number where M is the total number of digits (the precision) and D is the number of digits after the decimal point (the scale).

## Date and Time Types
- `DATE`: A date in the format YYYY-MM-DD.
- `TIME`: A time in the format HH:MM:SS.
- `YEAR`: A year in two-digit or four-digit format.
- `TIMESTAMP`: A timestamp, combining date and time, in the format YYYY-MM-DD HH:MM:SS.

## String Types
- `CHAR(M)`: A fixed-length string that is always right-padded with spaces to the specified length when stored.
- `VARCHAR(M)`: A variable-length string with a maximum length specified in parentheses.
- `SET`: A string object that can have zero or more values, each of which must be chosen from a list of permitted values specified when the table is created.
- `BLOB`: A binary large object that can hold a variable amount of data.
- `ENUM`: An enumeration, a string object that can have only one value, chosen from a list of possible values.

## JSON Type
- `JSON`: An efficient and flexible format to store and exchange data, allowing for a hierarchical, nested arrangement of data objects and arrays.

# Creating Tables

```sql
CREATE DATABASE IF NOT EXISTS moviedb;

USE moviedb;

CREATE TABLE actors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    firstName VARCHAR(20),
    lastName VARCHAR(20),
    birthDate DATE
);

CREATE TABLE directors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    firstName VARCHAR(20),
    lastName VARCHAR(20),
    birthDate DATE
);

CREATE TABLE genres (
    id INT AUTO_INCREMENT PRIMARY KEY,
    genreName VARCHAR(20)
);

CREATE TABLE movies (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(20),
    releaseYear YEAR,
    duration INT,
    rating DECIMAL(3, 1)
);

CREATE TABLE movieactors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    movieId INT,
    actorId INT,
    FOREIGN KEY (movieId) REFERENCES movies(id),
    FOREIGN KEY (actorId) REFERENCES actors(id)
);

CREATE TABLE moviedirectors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    movieId INT,
    directorId INT,
    FOREIGN KEY (movieId) REFERENCES movies(id),
    FOREIGN KEY (directorId) REFERENCES directors(id)
);

CREATE TABLE moviegenres (
    id INT AUTO_INCREMENT PRIMARY KEY,
    movieId INT,
    genreId INT,
    FOREIGN KEY (movieId) REFERENCES movies(id),
    FOREIGN KEY (genreId) REFERENCES genres(id)
);
```

# Inserting Data into Database

## Actors
```sql
INSERT INTO actors (firstName, lastName, birthDate) VALUES
('Robert', 'Downey Jr.', '1965-04-04'),
('Chris', 'Evans', '1981-06-13'),
('Scarlett', 'Johansson', '1984-11-22'),
('Mark', 'Ruffalo', '1967-11-22'),
('Chris', 'Hemsworth', '1983-08-11'),
('Tom', 'Holland', '1996-06-01'),
('Zendaya', 'Coleman', '1996-09-01'),
('Samuel', 'Jackson', '1948-12-21'),
('Emma', 'Stone', '1988-11-06'),
('Ryan', 'Reynolds', '1976-10-23');
```
## Directors
```sql
INSERT INTO directors (firstName, lastName, birthDate) VALUES
('Anthony', 'Russo', '1970-02-03'),
('Joe', 'Russo', '1971-07-18'),
('Christopher', 'Nolan', '1970-07-30'),
('James', 'Cameron', '1954-08-16'),
('Quentin', 'Tarantino', '1963-03-27'),
('Martin', 'Scorsese', '1942-11-17'),
('Jon', 'Watts', '1981-06-28'),
('Damien', 'Chazelle', '1985-01-19'),
('Taika', 'Waititi', '1975-08-16'),
('Patty', 'Jenkins', '1971-07-24');
```
## Genres
```sql
INSERT INTO genres (genreName) VALUES
('Action'),
('Drama'),
('Adventure'),
('Sci-Fi'),
('Romance'),
('Comedy'),
('Thriller');
```
## Movies
```sql
INSERT INTO movies (title, releaseYear, duration, rating) VALUES
('Avengers: Endgame', 2019, 181, 8.4),
('Inception', 2010, 148, 8.8),
('Titanic', 1997, 195, 7.8),
('Pulp Fiction', 1994, 154, 8.9),
('The Wolf of Wall Street', 2013, 180, 8.2),
('Spider-Man: Homecoming', 2017, 133, 7.4),
('La La Land', 2016, 128, 8.0),
('Deadpool', 2016, 108, 8.0),
('Thor: Ragnarok', 2017, 130, 7.9),
('Wonder Woman', 2017, 141, 7.4);
```
## MovieActors
```sql
INSERT INTO movieactors (movieId, actorId) VALUES
(1, 1), -- Avengers: Endgame, Robert Downey Jr.
(1, 2), -- Avengers: Endgame, Chris Evans
(1, 3), -- Avengers: Endgame, Scarlett Johansson
(1, 4), -- Avengers: Endgame, Mark Ruffalo
(1, 5), -- Avengers: Endgame, Chris Hemsworth
(2, 1), -- Inception, Robert Downey Jr.
(2, 3), -- Inception, Scarlett Johansson
(3, 2), -- Titanic, Chris Evans
(3, 4), -- Titanic, Mark Ruffalo
(4, 5), -- Pulp Fiction, Chris Hemsworth
(5, 1), -- The Wolf of Wall Street, Robert Downey Jr.
(6, 6), -- Spider-Man: Homecoming, Tom Holland
(6, 7), -- Spider-Man: Homecoming, Zendaya
(7, 9), -- La La Land, Emma Stone
(7, 10), -- La La Land, Ryan Reynolds
(8, 10), -- Deadpool, Ryan Reynolds
(9, 5), -- Thor: Ragnarok, Chris Hemsworth
(9, 8), -- Thor: Ragnarok, Samuel Jackson
(10, 2), -- Wonder Woman, Chris Evans
(10, 6); -- Wonder Woman, Tom Holland
```
## MovieDirectors
```sql
INSERT INTO moviedirectors (movieId, directorId) VALUES
(1, 1), -- Avengers: Endgame, Anthony Russo
(1, 2), -- Avengers: Endgame, Joe Russo
(2, 3), -- Inception, Christopher Nolan
(3, 4), -- Titanic, James Cameron
(4, 5), -- Pulp Fiction, Quentin Tarantino
(5, 6), -- The Wolf of Wall Street, Martin Scorsese
(6, 7), -- Spider-Man: Homecoming, Jon Watts
(7, 8), -- La La Land, Damien Chazelle
(8, 9), -- Deadpool, Taika Waititi
(9, 9), -- Thor: Ragnarok, Taika Waititi
(10, 10); -- Wonder Woman, Patty Jenkins
```
## MovieGenres
```sql
INSERT INTO moviegenres (movieId, genreId) VALUES
(1, 1), -- Avengers: Endgame, Action
(1, 3), -- Avengers: Endgame, Adventure
(2, 1), -- Inception, Action
(2, 4), -- Inception, Sci-Fi
(3, 2), -- Titanic, Drama
(3, 5), -- Titanic, Romance
(4, 2), -- Pulp Fiction, Drama
(4, 6), -- Pulp Fiction, Comedy
(5, 2), -- The Wolf of Wall Street, Drama
(6, 1), -- Spider-Man: Homecoming, Action
(6, 3), -- Spider-Man: Homecoming, Adventure
(7, 2), -- La La Land, Drama
(7, 5), -- La La Land, Romance
(8, 1), -- Deadpool, Action
(8, 6), -- Deadpool, Comedy
(9, 1), -- Thor: Ragnarok, Action
(9, 3), -- Thor: Ragnarok, Adventure
(10, 1), -- Wonder Woman, Action
(10, 3); -- Wonder Woman, Adventure
```

# Constraints
In SQL, constraints are like rules for your data. They make sure the data in your database is accurate and follows certain rules. Here's a quick look at some common ones:

### 1. NOT NULL
Ensures that a column cannot have a NULL value.

**Example:**
```sql
CREATE TABLE Students (
    student_id INT NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);
```

### 2. UNIQUE
Ensures that all values in a column are unique.

**Example:**
```sql
CREATE TABLE Employees (
    employee_id INT NOT NULL UNIQUE,
    email VARCHAR(100) UNIQUE
);
```

### 3. PRIMARY KEY
A combination of NOT NULL and UNIQUE. Uniquely identifies each row in a table. A table can have only one PRIMARY KEY, which can be a single column or a combination of columns.

**Example:**
```sql
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    order_date DATE NOT NULL
);
```

### 4. FOREIGN KEY
Enforces a link between the data in two tables. It ensures that the value in one table matches a value in another table.

**Example:**
```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100)
);

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    order_date DATE NOT NULL,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);
```

### 5. CHECK
Ensures that all values in a column satisfy a specific condition.

**Example:**
```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    price DECIMAL(10, 2) CHECK (price > 0)
);
```

### 6. DEFAULT
Sets a default value for a column if no value is specified when a record is inserted.

**Example:**
```sql
CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    hire_date DATE DEFAULT CURRENT_DATE
);
```

### 7. INDEX
While not exactly a constraint, indexes are used to create and retrieve data from the database very quickly. UNIQUE constraints automatically create an index on the specified column.

**Example:**
```sql
CREATE INDEX idx_employee_name ON Employees(employee_name);
```

### 8. AUTO_INCREMENT
Automatically generates a unique number for the column, often used with the PRIMARY KEY constraint.

**Example:**
```sql
CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL
);
```

# SQL Operators

SQL operators are used to perform operations on data stored in a database. They are categorized into different types based on the operations they perform. Here's an overview of the types of operators in SQL:

## Assignment Operator
- `=`: Used to assign values.

**Example:**
```sql
SET @myVar = 100;
```

## Arithmetic Operators
- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division
- `%`: Modulus

**Example:**
```sql
SELECT price * quantity AS total_cost FROM Sales;
```

## Relational Operators
- `=`: Equal to
- `<>` or `!=`: Not equal to
- `<`: Less than
- `>`: Greater than
- `<=`: Less than or equal to
- `>=`: Greater than or equal to

**Example:**
```sql
SELECT * FROM Employees WHERE salary >= 50000;
```

## Logical Operators
- `AND`: Returns true if both conditions are true.
- `OR`: Returns true if at least one condition is true.
- `NOT`: Reverses the result of a condition.

**Example:**
```sql
SELECT * FROM Orders WHERE order_date >= '2020-01-01' AND total_amount > 500;
```

## Set Operators
- `UNION`: Combines the result set of two or more SELECT statements (only distinct values).
- `UNION ALL`: Similar to UNION, but includes duplicates.
- `INTERSECT`: Returns the intersection of two SELECT statements.
- `EXCEPT`: Returns distinct rows from the first SELECT statement that aren't output by the second SELECT statement.

**Example:**
```sql
SELECT customer_id FROM Orders
UNION
SELECT customer_id FROM Returns;
```

## Special Operators
- `BETWEEN`: Checks if a value is within a range.
- `IN`: Checks if a value is within a list of values.
- `LIKE`: Searches for a specified pattern in a column.
    - % represents zero or more characters. For example, '%a' finds any values that end with "a".
    - _ represents a single character. For example, 'a_' finds any values that start with "a" and are at least two characters in length.
    - LIKE is case-insensitive in some databases (like SQL Server) but case-sensitive in others (like PostgreSQL), unless specified otherwise.
- `IS NULL`: Checks for NULL values.

**Example of `BETWEEN`:**
```sql
SELECT * FROM movies WHERE release_year BETWEEN 1990 AND 2000;
```

**Example of `IN`:**
```sql
SELECT * FROM generes WHERE genreName IN ('Action', 'Comedy');
```

**Example of `LIKE`:**
```sql
SELECT * FROM movies WHERE title LIKE '%Star Wars%';
```

**Example of `IS NULL`:**
```sql
SELECT * FROM directors WHERE lastName IS NULL;
```
### SQL Functions Overview

SQL functions are essential tools for data manipulation and querying in databases. Here's a concise guide to some commonly used SQL functions, categorized by their purpose.

### Aggregate Functions

Aggregate functions perform a calculation on a set of values and return a single value. They are often used with the `GROUP BY` clause.

- **COUNT()**: Counts the number of rows.
COUNT(employee_id): This part of the query tells SQL to count the number of employee_id values in the Employees table. It's important to note that COUNT() will count only non-NULL values when a specific column is mentioned.  
  ```sql
  SELECT COUNT(employee_id) FROM Employees;
  ```
  If you want to count all rows in the table regardless of whether specific columns have NULL values, you would use COUNT(*) instead:
  ```sql
  SELECT COUNT(*) FROM Employees;
  ```
  This counts all rows in the Employees table, including rows with NULL values in any of the columns
- **SUM()**: Calculates the total sum of a numeric column.
  ```sql
  SELECT SUM(salary) FROM Employees;
  ```
- **AVG()**: Computes the average value of a numeric column.
  ```sql
  SELECT AVG(salary) FROM Employees;
  ```
- **MAX()**: Finds the maximum value in a column.
  ```sql
  SELECT MAX(salary) FROM Employees;
  ```
- **MIN()**: Finds the minimum value in a column.
  ```sql
  SELECT MIN(salary) FROM Employees;
  ```

### String Functions

String functions allow for manipulation and querying of text data.

- **CONCAT()**: Concatenates two or more strings.
  ```sql
  SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM Employees;
  ```
- **UPPER()**: Converts a string to uppercase.
  ```sql
  SELECT UPPER(first_name) FROM Employees;
  ```
- **LOWER()**: Converts a string to lowercase.
  ```sql
  SELECT LOWER(first_name) FROM Employees;
  ```
- **TRIM()**: Removes leading and trailing spaces from a string.
  ```sql
  SELECT TRIM(first_name) FROM Employees;
  ```
- **LENGTH()**: Returns the length of a string.
  ```sql
  SELECT LENGTH(first_name) FROM Employees;
  ```

### Date Functions

Date functions are used to manipulate and extract information from date values.

- **NOW()**: Returns the current date and time.
  ```sql
  SELECT NOW();
  ```
- **CURDATE()**: Returns the current date.
  ```sql
  SELECT CURDATE();
  ```
- **DATE_ADD()**: Adds a specified time interval to a date.
  ```sql
  SELECT DATE_ADD('2023-01-01', INTERVAL 1 MONTH);
  ```
- **DATEDIFF()**: Calculates the difference in days between two dates.
  ```sql
  SELECT DATEDIFF('2023-12-31', '2023-01-01');
  ```

### Numerical Functions

Numerical functions perform operations on numerical data.

- **ROUND()**: Rounds a number to a specified number of decimal places.
  ```sql
  SELECT ROUND(price, 2) FROM Products;
  ```
- **ABS()**: Returns the absolute value of a number.
  ```sql
  SELECT ABS(-123);
  ```

# Clauses
- SQL clauses are used to specify conditions or modify the results of a query. Here are explanations for the clauses you mentioned:
- clauses are special keywords or phrases you can add to your queries to do specific things like filtering results, grouping data together, or sorting data in a certain order. They help you narrow down what you're looking for or change how the information is presented to you.

### WHERE Clause
- Purpose: Filters records based on specified conditions, returning only those that meet the criteria.
- Imagine you want to find all movies released after the year 2000. The `WHERE` clause helps you filter out movies based on this condition.

```sql
SELECT * FROM movies WHERE release_year > 2000;
```

This query fetches all columns for movies from the `movies` table where the `release_year` is greater than 2000.

### DISTINCT Clause
- Purpose: Removes duplicate rows from the results. It's used with the SELECT statement to return only distinct (different) values.
- Suppose you want to list all unique genres in your movie database because you're curious about the variety. The `DISTINCT` clause helps you eliminate duplicates.

```sql
SELECT DISTINCT genre FROM genreName;
```

This query returns all unique genre names from the `genres` table, ensuring no genre is listed more than once.

### GROUP BY Clause
- Purpose: Groups rows that have the same values in specified columns into summary rows, like "find the number of employees in each department".
- Let's say you're interested in knowing how many movies are there in each genre. The `GROUP BY` clause groups your movies by genre and counts them.

```sql
SELECT genre, COUNT(*) AS NumberOfMovies FROM movies JOIN genres ON movies.genre_id = genres.id GROUP BY genre;
```

This query joins the `movies` table with the `genres` table to get the genre names, groups the results by `genre`, and counts the number of movies in each genre.  
  
Let's say you're interested in knowing how many movies were released in each year. The GROUP BY clause groups your movies by release year and counts them.
```sql
mysql> SELECT releaseYear, COUNT(id) AS Number_of_movies FROM movies GROUP BY(releaseYear);
+-------------+------------------+
| releaseYear | Number_of_movies |
+-------------+------------------+
|        2019 |                1 |
|        2010 |                1 |
|        1997 |                1 |
|        1994 |                1 |
|        2013 |                1 |
|        2017 |                3 |
|        2016 |                2 |
+-------------+------------------+
```
### ORDER BY Clause
- Purpose: Sorts the result set in ascending or descending order based on one or more columns.
- If you want to see all movies sorted by their release years, from the most recent to the oldest, you use the `ORDER BY` clause.

```sql
SELECT title, release_year FROM movies ORDER BY release_year DESC;
```

This query selects movie titles and their release years from the `movies` table and orders the results in descending order of `release_year`.

### HAVING Clause
- Purpose: Used to filter groups based on a specified condition. It's often used with the GROUP BY clause. While the WHERE clause filters rows, the HAVING clause filters groups.
- Imagine you want to find genres that have more than 10 movies in them. Since you need to group movies by genre and then filter these groups, you use the `HAVING` clause along with `GROUP BY`.

```sql
SELECT genre, COUNT(*) AS NumberOfMovies FROM movies JOIN genres ON movies.genre_id = genres.id GROUP BY genre HAVING COUNT(*) > 10;
```

This query joins the `movies` table with the `genres` table, groups the results by `genre`, counts the number of movies in each genre, and then filters out the genres having more than 10 movies.

# limit and offset

The `LIMIT` and `OFFSET` clauses in SQL are used to control the number of records returned by a query and to specify from which record to start returning records, respectively. They are particularly useful for implementing pagination in applications that display a large number of records.

- **`LIMIT` Clause**: This clause is used to specify the maximum number of records that the query should return. It is useful when you want to retrieve only a subset of records from your result set.
```sql
SELECT * FROM users LIMIT 5; -- will return the first 5 records from the `users` table.
```
- **`OFFSET` Clause**: This clause is used in conjunction with `LIMIT` to skip a specific number of records before starting to return records from the query. It is essential for implementing pagination where you need to skip a certain number of records from the beginning.
```sql
SELECT * FROM users LIMIT 5 OFFSET 10; --will skip the first 10 records and then return the next 5 records from the `users` table.
```




