```sql
CREATE DATABASE IF NOT EXISTS bookdb;

USE bookdb;

CREATE TABLE authors (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL
);

CREATE TABLE books (
    id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    pages INT NOT NULL,
    author_id INT,
    FOREIGN KEY (author_id) REFERENCES authors(id)
);

INSERT INTO authors (id, name, age) VALUES
(1, 'James Patterson', 72),
(2, 'Dan Brown', 55),
(3, 'JK Rowling', 54),
(4, 'David Baldacci', 59),
(5, 'Agatha Christie', 85),
(6, 'Stephen King', 73),
(7, 'George Orwell', 46),
(8, 'Isaac Asimov', 72);


INSERT INTO books (id, title, pages, author_id) VALUES
(1, 'Along Came a Spider', 435, 1),
(2, 'The Da Vinci Code', 454, 2),
(3, 'The Lost Symbol', 528, 2),
(4, 'HP & Sorcerer''s Stone', 309, 3),
(5, 'HP & Chamber of Secrets', 341, 3);
```
# JOIN
SQL joins are used to combine rows from two or more tables, based on a related column between them. Here are simple examples of each type of join:

- firstly see what exactly join return...
```sql
SELECT * FROM books JOIN authors;
```
| id | title                   | pages | author_id | id | name            | age |
|----|-------------------------|-------|-----------|----|-----------------|-----|
|  5 | HP & Chamber of Secrets |   341 |         3 |  1 | James Patterson |  72 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  1 | James Patterson |  72 |
|  3 | The Lost Symbol         |   528 |         2 |  1 | James Patterson |  72 |
|  2 | The Da Vinci Code       |   454 |         2 |  1 | James Patterson |  72 |
|  1 | Along Came a Spider     |   435 |         1 |  1 | James Patterson |  72 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  2 | Dan Brown       |  55 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  2 | Dan Brown       |  55 |
|  3 | The Lost Symbol         |   528 |         2 |  2 | Dan Brown       |  55 |
|  2 | The Da Vinci Code       |   454 |         2 |  2 | Dan Brown       |  55 |
|  1 | Along Came a Spider     |   435 |         1 |  2 | Dan Brown       |  55 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  3 | JK Rowling      |  54 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  3 | JK Rowling      |  54 |
|  3 | The Lost Symbol         |   528 |         2 |  3 | JK Rowling      |  54 |
|  2 | The Da Vinci Code       |   454 |         2 |  3 | JK Rowling      |  54 |
|  1 | Along Came a Spider     |   435 |         1 |  3 | JK Rowling      |  54 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  4 | David Baldacci  |  59 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  4 | David Baldacci  |  59 |
|  3 | The Lost Symbol         |   528 |         2 |  4 | David Baldacci  |  59 |
|  2 | The Da Vinci Code       |   454 |         2 |  4 | David Baldacci  |  59 |
|  1 | Along Came a Spider     |   435 |         1 |  4 | David Baldacci  |  59 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  5 | Agatha Christie |  85 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  5 | Agatha Christie |  85 |
|  3 | The Lost Symbol         |   528 |         2 |  5 | Agatha Christie |  85 |
|  2 | The Da Vinci Code       |   454 |         2 |  5 | Agatha Christie |  85 |
|  1 | Along Came a Spider     |   435 |         1 |  5 | Agatha Christie |  85 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  6 | Stephen King    |  73 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  6 | Stephen King    |  73 |
|  3 | The Lost Symbol         |   528 |         2 |  6 | Stephen King    |  73 |
|  2 | The Da Vinci Code       |   454 |         2 |  6 | Stephen King    |  73 |
|  1 | Along Came a Spider     |   435 |         1 |  6 | Stephen King    |  73 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  7 | George Orwell   |  46 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  7 | George Orwell   |  46 |
|  3 | The Lost Symbol         |   528 |         2 |  7 | George Orwell   |  46 |
|  2 | The Da Vinci Code       |   454 |         2 |  7 | George Orwell   |  46 |
|  1 | Along Came a Spider     |   435 |         1 |  7 | George Orwell   |  46 |
|  5 | HP & Chamber of Secrets |   341 |         3 |  8 | Isaac Asimov    |  72 |
|  4 | HP & Sorcerer's Stone   |   309 |         3 |  8 | Isaac Asimov    |  72 |
|  3 | The Lost Symbol         |   528 |         2 |  8 | Isaac Asimov    |  72 |
|  2 | The Da Vinci Code       |   454 |         2 |  8 | Isaac Asimov    |  72 |
|  1 | Along Came a Spider     |   435 |         1 |  8 | Isaac Asimov    |  72 |

- so, it's cross product each rows and sum of column



### INNER JOIN (JOIN)

**Definition**: Returns records that have matching values in both tables.

**Example**: Find the titles of books and their authors' names.

```sql
SELECT b.title AS BookTitle, a.name AS AuthorName
FROM books b
INNER JOIN authors a ON b.author_id = a.id;
```
here output from cross product where match id's
| BookTitle               | AuthorName      |
|-------------------------|-----------------|
| Along Came a Spider     | James Patterson |
| The Da Vinci Code       | Dan Brown       |
| The Lost Symbol         | Dan Brown       |
| HP & Sorcerer's Stone   | JK Rowling      |
| HP & Chamber of Secrets | JK Rowling      |


### LEFT JOIN (or LEFT OUTER JOIN)

**Definition**: Returns all records from the left table, and the matched records from the right table. If there is no match, the result is NULL on the side of the right table.

**Example**: List all books and their authors' names, including books without an author.means here a table which in left side that's rows appear completly with given condition.  
here books as left table

```sql
SELECT authors.name AS AuthorName, books.title AS BookTitle 
FROM books
LEFT JOIN authors ON books.author_id = authors.id;
```
| AuthorName      | BookTitle               |
|-----------------|-------------------------|
| James Patterson | Along Came a Spider     |
| Dan Brown       | The Da Vinci Code       |
| Dan Brown       | The Lost Symbol         |
| JK Rowling      | HP & Sorcerer's Stone   |
| JK Rowling      | HP & Chamber of Secrets |

in our side there have not any book which does not have author.

### RIGHT JOIN (or RIGHT OUTER JOIN)

**Definition**: Returns all records from the right table, and the matched records from the left table. If there is no match, the result is NULL on the side of the left table.

**Example**: List all authors and their books, including authors who haven't written any books listed.

```sql
SELECT b.title AS Book_title, a.name AS Author_Name
FROM books b
RIGHT JOIN authors a ON b.author_id=a.id;
```
| Book_title              | Author_Name     |
|-------------------------|-----------------|
| Along Came a Spider     | James Patterson |
| The Lost Symbol         | Dan Brown       |
| The Da Vinci Code       | Dan Brown       |
| HP & Chamber of Secrets | JK Rowling      |
| HP & Sorcerer's Stone   | JK Rowling      |
| NULL                    | David Baldacci  |
| NULL                    | Agatha Christie |
| NULL                    | Stephen King    |
| NULL                    | George Orwell   |
| NULL                    | Isaac Asimov    |

Here authers table is in right side so all authers includes...

### FULL JOIN (or FULL OUTER JOIN)

**Definition**: Returns all records when there is a match in either left or right table. Records that do not match are filled with NULL values.

**Note**: MySQL does not directly support `FULL JOIN`, but it can be simulated using a combination of `LEFT JOIN`, `RIGHT JOIN`, and `UNION`.

**Example**: List all books and all authors, showing the author of each book if one exists, and also showing authors that have no books listed.

```sql
SELECT books.title AS BookTitle, authors.name AS AuthorName
FROM books
LEFT JOIN authors ON books.author_id = authors.id
UNION
SELECT books.title AS BookTitle, authors.name AS AuthorName
FROM books
RIGHT JOIN authors  ON books.author_id=authors.id;
```
| Book_title              | Author_Name     |
|-------------------------|-----------------|
| Along Came a Spider     | James Patterson |
| The Lost Symbol         | Dan Brown       |
| The Da Vinci Code       | Dan Brown       |
| HP & Chamber of Secrets | JK Rowling      |
| HP & Sorcerer's Stone   | JK Rowling      |
| NULL                    | David Baldacci  |
| NULL                    | Agatha Christie |
| NULL                    | Stephen King    |
| NULL                    | George Orwell   |
| NULL                    | Isaac Asimov    |

### CROSS JOIN

this is same as join  

**Definition**: Returns a Cartesian product of the two tables, i.e., it joins every row of the first table with every row of the second table.

**Example**: List all possible combinations of books and authors.

```sql
SELECT books.title AS BookTitle, authors.name AS AuthorName
FROM books
CROSS JOIN authors;
```
| BookTitle               | AuthorName      |
|-------------------------|-----------------|
| HP & Chamber of Secrets | James Patterson |
| HP & Sorcerer's Stone   | James Patterson |
| The Lost Symbol         | James Patterson |
| The Da Vinci Code       | James Patterson |
| Along Came a Spider     | James Patterson |
| HP & Chamber of Secrets | Dan Brown       |
| HP & Sorcerer's Stone   | Dan Brown       |
| The Lost Symbol         | Dan Brown       |
| The Da Vinci Code       | Dan Brown       |
| Along Came a Spider     | Dan Brown       |
| HP & Chamber of Secrets | JK Rowling      |
| HP & Sorcerer's Stone   | JK Rowling      |
| The Lost Symbol         | JK Rowling      |
| The Da Vinci Code       | JK Rowling      |
| Along Came a Spider     | JK Rowling      |
| HP & Chamber of Secrets | David Baldacci  |
| HP & Sorcerer's Stone   | David Baldacci  |
| The Lost Symbol         | David Baldacci  |
| The Da Vinci Code       | David Baldacci  |
| Along Came a Spider     | David Baldacci  |
| HP & Chamber of Secrets | Agatha Christie |
| HP & Sorcerer's Stone   | Agatha Christie |
| The Lost Symbol         | Agatha Christie |
| The Da Vinci Code       | Agatha Christie |
| Along Came a Spider     | Agatha Christie |
| HP & Chamber of Secrets | Stephen King    |
| HP & Sorcerer's Stone   | Stephen King    |
| The Lost Symbol         | Stephen King    |
| The Da Vinci Code       | Stephen King    |
| Along Came a Spider     | Stephen King    |
| HP & Chamber of Secrets | George Orwell   |
| HP & Sorcerer's Stone   | George Orwell   |
| The Lost Symbol         | George Orwell   |
| The Da Vinci Code       | George Orwell   |
| Along Came a Spider     | George Orwell   |
| HP & Chamber of Secrets | Isaac Asimov    |
| HP & Sorcerer's Stone   | Isaac Asimov    |
| The Lost Symbol         | Isaac Asimov    |
| The Da Vinci Code       | Isaac Asimov    |
| Along Came a Spider     | Isaac Asimov    |

### SELF JOIN

**Definition**: A self join is a regular join, but the table is joined with itself. This is not directly applicable to the `books` and `authors` example, as it typically applies to scenarios where hierarchical or self-referential data is involved.

- To find pairs of books written by the same author, you can use the following query:
```sql
SELECT b1.title AS Book1, b2.title AS Book2, a.name AS Author
FROM books b1
JOIN books b2 ON b1.author_id = b2.author_id AND b1.id < b2.id
JOIN authors a ON b1.author_id = a.id;
```
| Book1                 | Book2                   | Author     |
|-----------------------|-------------------------|------------|
| The Da Vinci Code     | The Lost Symbol         | Dan Brown  |
| HP & Sorcerer's Stone | HP & Chamber of Secrets | JK Rowling |
