# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Departments with the following columns:DepartmentID as INTEGER,DepartmentName as TEXT

```sql
  CREATE TABLE Departments(
   DepartmentID INTEGER,
   DepartmentName TEXT);
```

**Output:**

<img width="871" height="258" alt="image" src="https://github.com/user-attachments/assets/966167f8-f6be-4c33-83bb-55bc634c18fc" />


**Question 2**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
   CREATE TABLE item(
   item_id TEXT PRIMARY KEY,
   item_desc TEXT NOT NULL,
   rate INTEGER NOT NULL,
   icom_id TEXT CHECK(LENGTH(icom_id)=4),
    FOREIGN KEY(icom_id) REFERENCES company(com_id)
    ON UPDATE SET NULL
    ON DELETE SET NULL
);
```

**Output:**

<img width="902" height="273" alt="image" src="https://github.com/user-attachments/assets/3bea9042-feb5-49b5-8369-8386b86acda1" />



**Question 3**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
ALTER TABLE customers
ADD column email TEXT
```

**Output:**

<img width="897" height="227" alt="image" src="https://github.com/user-attachments/assets/65106054-40ef-4f76-9572-05db0462aeca" />


**Question 4**
---
Insert all employees from Former_employees into Employee
Table attributes are EmployeeID, Name, Department, Salary

```sql
INSERT INTO Employee(EmployeeID ,Name ,Department ,Salary)
SELECT * FROM Former_employees
```

**Output:**

<img width="906" height="212" alt="image" src="https://github.com/user-attachments/assets/6048f28a-e71c-49ad-9758-faced8f2df20" />


**Question 5**
---
Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'

```sql
ALTER TABLE Employees 
ADD column Date_of_joining Date;
ALTER TABLE Employees
RENAME job_title to Designation;
```

**Output:**

<img width="905" height="270" alt="image" src="https://github.com/user-attachments/assets/99569cac-50db-49d4-8da6-76cd660142a4" />


**Question 6**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE CHECK (DueDate>InvoiceDate),
Amount REAL  CHECK(Amount>0)
);
```

**Output:**

<img width="915" height="220" alt="image" src="https://github.com/user-attachments/assets/026b6881-db74-4ab7-9f46-821445373eb6" />


**Question 7**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```sql
INSERT INTO student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES(205,"Olivia Green",'F',NULL,NULL);
INSERT INTO student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES(207,"Liam Smith","M","Mathematics",85);
INSERT INTO student_details(RollNo,Name,Gender,Subject,MARKS)
VALUES(208,"Sophia Johnson","F","Science",NULL);
```

**Output:**

<img width="928" height="233" alt="image" src="https://github.com/user-attachments/assets/6aae8954-9a82-4682-af65-be4148418781" />


**Question 8**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE CHECK (DueDate>InvoiceDate),
OrderID INTEGER,
FOREIGN KEY(OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="900" height="227" alt="image" src="https://github.com/user-attachments/assets/f4a4603b-b6d7-426d-842b-f58a43fa49de" />

**Question 9**
---
Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.


```sql
INSERT INTO  Products(ProductID,Name,Category,Price,Stock)
VALUES(101,"Laptop","Electronics",1500,50);
```

**Output:**

<img width="910" height="205" alt="image" src="https://github.com/user-attachments/assets/fa782c91-afa3-4e31-aae3-12bb7bcdb2f2" />

**Question 10**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT NOT NULL UNIQUE,
Location TEXT 
)
```

**Output:**

<img width="917" height="235" alt="image" src="https://github.com/user-attachments/assets/ee8f3abf-4ed2-4ff1-ba48-2064beb221e9" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
