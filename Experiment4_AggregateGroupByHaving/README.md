# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
What is the most common time slot for appointments for each doctor?

```
with SlotCounts as (select DoctorID,strftime('%H:%M', AppointmentDateTime) as TimeSlot,count(*) as TotalAppointments,
ROW_NUMBER() OVER (partition by DoctorID order by count(*) desc) as rnk
from Appointments group by DoctorID,strftime('%H:%M',AppointmentDateTime))
select DoctorID,TimeSlot,TotalAppointments from SlotCounts where rnk=1 order by TotalAppointments desc;
```

**Output:**

<img width="1630" height="1245" alt="image" src="https://github.com/user-attachments/assets/6d2bba83-656f-4723-8120-e58955fc30be" />

**Question 2**
---
How many patients are there in each city?


```
select Address,count(PatientID) as TotalPatients from Patients group by Address;
```

**Output:**

<img width="1801" height="1079" alt="image" src="https://github.com/user-attachments/assets/315a68a8-0667-4f27-853f-9b1c80c27be5" />

**Question 3**
---
How many male and female doctors are there in each medical specialty?

```
select Specialty,Gender,count(DoctorID) as TotalDoctors from Doctors group by Specialty,Gender;
```

**Output:**

<img width="1788" height="1252" alt="image" src="https://github.com/user-attachments/assets/166a2d55-40b4-498c-b4bb-9a12e769abbc" />

**Question 4**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

 
```
select (max(price)-min(price)) as price_diff from fruits;
```

**Output:**

<img width="1820" height="969" alt="image" src="https://github.com/user-attachments/assets/e05a4303-0320-4234-bf1f-fd87cf826281" />

**Question 5**
---
Write a SQL query to calculate the total number of working hours of all employees

```
select sum(workhour) as 'Total working hours' from employee1;
```

**Output:**

<img width="1814" height="1004" alt="image" src="https://github.com/user-attachments/assets/c71e500a-550d-4ee5-85fa-4d8ffdecd8e3" />

**Question 6**
---
Write a SQL query to find how many employees have an income greater than 50K?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```
select count(id) as employees_count from employee where income>50000;
```

**Output:**

<img width="1672" height="1000" alt="image" src="https://github.com/user-attachments/assets/e4d3d5a2-2ced-424f-966b-81453b606d53" />

**Question 7**
---
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
        
```
select count(customer_id) as COUNT from customer;
```

**Output:**

<img width="1679" height="983" alt="image" src="https://github.com/user-attachments/assets/ff810c14-99d9-4121-b058-b4294ab0b1c6" />

**Question 8**
---
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

```
select category_id,count(*) as COUNT from products where category_id>2 group by category_id;
```

**Output:**

<img width="1748" height="990" alt="image" src="https://github.com/user-attachments/assets/b38bd04e-2ec5-4942-a2a1-26e1d6d5ae6c" />

**Question 9**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

```
select category_id,count(product_name) from products where category_id<3 group by category_id;
```

**Output:**

<img width="1898" height="1047" alt="image" src="https://github.com/user-attachments/assets/71dedce2-8cfd-42ee-9903-bbc40f4b4d26" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.


```
select address,SUM(salary) from customer1 group by address having sum(salary)>2000;
```

**Output:**

<img width="1742" height="1146" alt="image" src="https://github.com/user-attachments/assets/8e3c60bc-8d86-4050-8ef2-2be2ff932d79" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
