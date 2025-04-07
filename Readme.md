# Mysql


- MySQL is a popular open-source Relational Database Management System (RDBMS).
- It's used to store, organize, and retrieve data in a structured way using tables.
- Key features include its `reliability`,   `scalability`, and `wide community support` 
- The default port for MySQL is `3306`. 


## Commands
 
### Show/Listing Existing Databases
```
show databases;
```

### Use/Switch Existing Databases  eg."database1"
```
use database1;
```

### Create Databases
```
create database myfirststore;
```

### Deleting a Databases eg."database1"
```
drop database database1;
```
### Create A New Table
```
CREATE TABLE students(
    id INT,
    name VARCHAR(40),
    class INT,
);
```

### See the Table Structure
```
DESC students;
```
### Adding/Inserting Data into Table "students"
```
INSERT INTO students(id,name,class)
values(101,"Suman",5);
```
### Adding/Inserting Data into Table "students" without Defining Order

- It will follow the default table order
- eg.(1st -> id)
- (2nd -> name)
- (3rd -> class)

```
INSERT INTO students
values(103,"Samay",10);
```

### Adding/Inserting Multiple Data into Table "students" 
```
INSERT INTO students
VALUES (102,"Sam",10), (104,"Saksham",8) , (105,"Simran",4);
```

### Reading Data from the Table

- To See Specific One Column
```
SELECT <column_name> FROM students;
```
- To See All Column
```
SELECT * FROM students;
```

### Reading Data for a specific Id

```
SELECT * FROM students
WHERE id = 105;
```
### Modify / Updating Data for a specific Id

```
UPDATE students
SET name = "Manav"
WHERE id = 103 ;
```
### Deleting Data for a specific Id

```
DELETE FROM students
WHERE id = 103 ;
```

### Delete Entire Table  eg."students"
```
DROP TABLE students;
```

- By default If we didn't add any column it will be added as `NULL`

eg. 
```
INSERT INTO students
VALUES (102,"Sam",10), (104,"Saksham") , (105,"Simran");
```
Output 
| id  | name    | class |
|-----|---------|-------|
| 102 | Sam     | 10    |
| 104 | Saksham | NULL  |
| 105 | Simran  | NULL  |

- We have to manually set the Column to   `NOT NULL` to avoid this

```
CREATE TABLE customers(
    id INT NOT NULL,
    name VARCHAR(40) NOT NULL
);
```

Now for an insert like 
```
INSERT INTO customers
VALUES (101);
```
Output : 
```
Field 'name' doesn't have a default value
```
Note : * **Same will happen for providing NULL as input** *

- ## For Changing the `DEFAULT` we need to provide it manually when creating the table like:

```
CREATE TABLE customers(
    id INT NOT NULL,
    name VARCHAR(40) NOT NULL,
    acc_type VARCHAR(40) NOT NULL DEFAULT 'savings'
);
```

- Now after adding only few columns like:
```
INSERT INTO customers
VALUES (101,"Raju"), (102,"Sham"), (103,"Paul");
```
Output :

| id  | name  | acc_type |
|-----|-------|----------|
| 101 | Raju  | savings  |
| 102 | Sham  | savings  |
| 103 | Paul  | savings  |

## Primary Key
* A **primary key** is a column (or set of columns) in a table that **uniquely identifies each row**.
* It ensures **data integrity** by preventing duplicate records.
* Primary key columns **cannot contain NULL values**.
* Each table can have **only one primary key**.
* Used for **referencing rows** in other tables (as a foreign key).
* It typically creates an **indexed structure**, which can improve query performance for lookups based on the primary key.

### Creating table with Primary Key
```
CREATE TABLE customers(
    acc_no INT PRIMARY KEY,
    name VARCHAR(40) NOT NULL,
    acc_type VARCHAR(40) NOT NULL DEFAULT 'savings'
);
```

- Now we cannot make duplicate `acc_no` eg.
```
INSERT INTO customers(acc_no , name)
VALUES (1102, "Fan"), (1102, "Sam");
```

output :

**Error Code:** 1062. Duplicate entry '1102' for key 'customers.PRIMARY'

## Auto Increment
- It will automatically increase the value
```
CREATE TABLE customers(
    acc_no INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(40) NOT NULL,
    acc_type VARCHAR(40) NOT NULL DEFAULT 'savings'
);
```
- Now no need to add manually `acc_no` Although we can
- The increment will start from the largest value provided like:
```
INSERT INTO customers (name)
VALUES ("RAT"), ("BAT"), ("CAT");
```
| acc_no | name | acc_type |
|--------|------|----------|
| 1      | RAT  | savings  |
| 2      | BAT  | savings  |
| 3      | CAT  | savings  |

## Alias  "AS"
* An **alias** is a temporary, alternative name given to a table or a column in a MySQL query.
* It's used to make the query **more readable and understandable**, especially for complex queries involving multiple tables or calculated columns.
* Aliases are only valid for the **duration of the query execution**.
For eg.
```
SELECT acc_no AS "Account No." FROM customers;
```
Output
| Account No. |
|-------------|
| 1           |
| 2           |
| 3           |

OR
```
SELECT acc_no AS "Account No.", name AS "CUSTOMER NAME" FROM customers;
```
Output

| Account No. | CUSTOMER NAME |
|-------------|---------------|
| 1           | RAT           |
| 2           | BAT           |
| 3           | CAT           |

