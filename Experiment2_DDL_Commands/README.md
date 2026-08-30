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
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
```
create table Department(DepartmentID INTEGER PRIMARY KEY,DepartmentName text UNIQUE NOT NULL,Location text);
```

**Output:**

<img width="1739" height="771" alt="image" src="https://github.com/user-attachments/assets/a5a651cd-ef00-4448-bcad-3eaad949d39f" />

**Question 2**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
```
create table Customers(CustomerID INTEGER,Name TEXT,Email TEXT,JoinDate DATETIME);
```

**Output:**

<img width="1811" height="1032" alt="image" src="https://github.com/user-attachments/assets/abc3f1dc-5cf3-4a63-9346-0c8a46520086" />

**Question 3**
---
Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.


```
insert into Student_details (RollNo,Name,Gender,Subject,MARKS) values (201,"David Lee","M","Physics",92);
```

**Output:**

<img width="1854" height="913" alt="image" src="https://github.com/user-attachments/assets/7d960a29-bc48-4a57-b3ae-bfb4fd965631" />

**Question 4**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```
create table Shipments (ShipmentID INTEGER PRIMARY KEY,ShipmentDate DATE,SupplierID INTEGER,OrderID INTEGER,FOREIGN KEY(SupplierID) REFERENCES Suppliers(SupplierID),FOREIGN KEY(OrderID) REFERENCES Orders(OrderID));
```

**Output:**

<img width="1807" height="919" alt="image" src="https://github.com/user-attachments/assets/ffec72e1-3283-4182-8dfb-fb47958909b7" />

**Question 5**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```
insert into Employee(EmployeeID,Name,Department,Salary) select EmployeeID,Name,Department,Salary from Former_employees;
```

**Output:**

<img width="1722" height="945" alt="image" src="https://github.com/user-attachments/assets/16eed565-1261-4763-97e2-39c7505128dd" />

**Question 6**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```
create table Employees(EmployeeID int PRIMARY KEY,FirstName NOT NULL,LastName not null,Email unique,Salary check(Salary>0),DepartmentID,FOREIGN KEY(DepartmentID) REFERENCES Departments(DepartmentID));
```

**Output:**

<img width="1880" height="1016" alt="image" src="https://github.com/user-attachments/assets/384addf6-c177-47fa-8d80-a9bc1c22f393" />

**Question 7**
---
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

```
alter table Companies rename column name to first_name;
alter table Companies add column mobilenumb number;
alter table Companies add column DOB Date;
alter table Companies add column State varchar(30);
```

**Output:**

<img width="1832" height="1027" alt="image" src="https://github.com/user-attachments/assets/add64a6d-8fba-43f6-b245-af927f9ba1f3" />

**Question 8**
---
Write a SQL query to modify the Student_details table by adding a new column Email of type VARCHAR(50) and updating the column MARKS to have a default value of 0.

```
alter table Student_details add column Email VARCHAR(50);
alter table Student_details add column MARKS INT DEFAULT 0;
```

**Output:**

<img width="1918" height="900" alt="image" src="https://github.com/user-attachments/assets/e57238a4-c751-4136-bca3-f2f69efa3410" />

**Question 9**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```
CREATe table jobs (job_id,job_title DEFAULT ' ',min_salary DEFAULT 8000,max_salary DEFAULT NULL);
```

**Output:**

<img width="1866" height="999" alt="image" src="https://github.com/user-attachments/assets/d20dd8a0-d0f3-41be-b19e-1513e7d2110f" />

**Question 10**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021
```
insert into Books(ISBN,Title,Author) values ('978-1234567890','Introduction to AI','John Doe');
insert into Books(ISBN,Title,Author,Publisher,Year) values('978-9876543210','Deep Learning','Jane Doe','TechPress',2022);
insert into Books(ISBN,Title,Author,Year) values('978-1122334455','Cybersecurity Essentials','Alice Smith',2021);
```

**Output:**

<img width="1833" height="953" alt="image" src="https://github.com/user-attachments/assets/da96fe96-b490-488e-ad7c-cb20db48175c" />


**Screenshot of Module 1 SEB Completion Grades:**

<img width="1983" height="820" alt="image" src="https://github.com/user-attachments/assets/ef387896-121a-4976-9e6a-23447744e748" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
