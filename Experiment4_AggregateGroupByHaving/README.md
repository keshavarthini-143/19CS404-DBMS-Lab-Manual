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
What is the total number of appointments scheduled by each doctor?
Sample table:Appointments Table

```sql
select DoctorID , count(*) AS TotalAppointments
from Appointments
group by DoctorID
```

**Output:**

<img width="603" height="507" alt="image" src="https://github.com/user-attachments/assets/8d9961a7-dd14-489f-8df9-11b4fa2f265b" />


**Question 2**
---
How many doctors specialize in each medical specialty?
Sample table:Doctors Table

```sql
select specialty, count(*) AS TotalDocto
from Doctors 
group by specialty
```

**Output:**

<img width="638" height="582" alt="image" src="https://github.com/user-attachments/assets/aabd1086-d925-48a6-8f71-dde7a2db3dbb" />

**Question 3**
---
How many medical records are there for each patient?

```sql
select patientID, count(*) AS TotalRecords
from MedicalRecords
group by patientID
```

**Output:**

<img width="534" height="534" alt="image" src="https://github.com/user-attachments/assets/6188d4a9-183a-4871-802e-66488c39d6d0" />


**Question 4**
---
```
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city
Table: customer
name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
```

```sql
select avg(length(email)) as avg_email_length_below_30
from customer
where city = 'Mumbai'
```

**Output:**

<img width="587" height="307" alt="image" src="https://github.com/user-attachments/assets/97564ecc-3cc7-438e-98a7-6e95754e33a7" />


**Question 5**
---
```
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.
Note: Inventory attribute contains amount of fruits
Table: fruits
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 
```

```sql
select sum(inventory) as total
from fruits
where unit = 'LB'

```

**Output:**

<img width="430" height="316" alt="image" src="https://github.com/user-attachments/assets/12f229ee-2b6c-4363-998f-6ceec9190487" />


**Question 6**
---
```
Write a SQL query to find the minimum purchase amount.
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```

```sql
select min(purch_amt) as MINIMUM
from orders
```

**Output:**

<img width="375" height="311" alt="image" src="https://github.com/user-attachments/assets/f077f043-dd65-4c66-a7d5-49d8d15ae5a1" />

**Question 7**
---
```
Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.
Sample table: orders
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```

```sql
select sum(purch_amt) as TOTAL
from orders

```

**Output:**

<img width="293" height="318" alt="image" src="https://github.com/user-attachments/assets/3c499b99-a421-470e-a204-226cf130f5d7" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 400,000.
Sample table: employee

```sql
select age, min(income) AS 'MIN(income)'
from employee
group by age
having min(income) < 400000
```

**Output:**

<img width="691" height="424" alt="image" src="https://github.com/user-attachments/assets/bc6e9298-461f-4365-9c7a-689d5cbd3c6d" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.
Sample table: employee1

```sql
select jdate,avg(workhour) as 'AVG(workhour)'
from employee1
group by jdate
having avg(workhour) < 10
```

**Output:**

<img width="534" height="338" alt="image" src="https://github.com/user-attachments/assets/0c627839-a819-42c2-8e65-406e086ae1bf" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by city, calculates the total income for each city, and includes only those cities where the total income sum is greater than 200,000.
Sample table: employee

```sql
select city, sum(income) as Income
from employee
group by city
having sum(income) > 200000
```

**Output:**

<img width="479" height="469" alt="image" src="https://github.com/user-attachments/assets/889dc298-07c7-4cb7-9c3f-55346f1d986c" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
