# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
<img width="1294" height="631" alt="image" src="https://github.com/user-attachments/assets/493cd13c-7cb8-4604-ace8-6012db719abb" />

```sql
SELECT p.*
FROM patients p, test_results t
WHERE p.patient_id = t.patient_id
  AND t.test_name IN ('Blood Test','Blood Pressure')
  AND t.result NOT LIKE '%Normal%';
```

**Output:**
<img width="1352" height="261" alt="image" src="https://github.com/user-attachments/assets/efbc8320-2432-4c69-8149-790d99577a64" />


**Question 2**
---
<img width="1349" height="465" alt="image" src="https://github.com/user-attachments/assets/46ec0e90-74c9-43cd-861c-091bb2f7316d" />


```sql
SELECT p.first_name AS patient_name, d.first_name AS doctor_name
FROM patients p
JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;

```

**Output:**

<img width="1362" height="251" alt="image" src="https://github.com/user-attachments/assets/84015a68-fb03-4e2c-8636-e8370ceb3099" />

**Question 3**
---
<img width="1353" height="546" alt="image" src="https://github.com/user-attachments/assets/462444e7-f3f6-4622-a81f-ce6c5544a609" />


```sql
SELECT c.cust_name AS "Customer Name", c.city AS "city",
       s.name AS "Salesman", s.city AS "city", s.commission AS "commission"
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city AND s.commission > 0.12;

```

**Output:**

<img width="1360" height="383" alt="image" src="https://github.com/user-attachments/assets/641adbd8-4981-4b8e-b303-02268ef4b2d9" />


**Question 4**
---
<img width="1353" height="192" alt="image" src="https://github.com/user-attachments/assets/b98e17ba-55b7-4c36-b4d4-b779508f6573" />


```sql
SELECT s.name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.city = 'New York';

```

**Output:**

<img width="1366" height="251" alt="image" src="https://github.com/user-attachments/assets/f38f2e43-dc3f-4278-83f0-bf0acb74c969" />

**Question 5**
---
<img width="1350" height="554" alt="image" src="https://github.com/user-attachments/assets/ef3ad1b2-6dcf-4321-bcb1-569648896f7d" />


```sql
SELECT c.cust_name AS "Customer Name", c.city AS "city",
       s.name AS "Salesman", s.commission AS "commission"
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

```

**Output:**

<img width="1361" height="474" alt="image" src="https://github.com/user-attachments/assets/252b4ddb-c4db-4181-b33a-6c5d380bdc8d" />


**Question 6**
---
<img width="1358" height="289" alt="image" src="https://github.com/user-attachments/assets/32d9cc7c-14d8-4c30-93c2-3c66535ac0f0" />

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';
```

**Output:**
<img width="1359" height="518" alt="image" src="https://github.com/user-attachments/assets/edbf2a76-2039-4fbe-ae9b-dd9dc18bfdbe" />




**Question 7**
---
<img width="1372" height="594" alt="image" src="https://github.com/user-attachments/assets/90ee3d60-d79b-4fd7-8a29-fd76dfa497e5" />


```sql
SELECT a.cust_name, a.city, b.ord_no,
       b.ord_date, b.purch_amt AS "Order Amount", 
       c.name, c.commission 
-- Specifying the tables to retrieve data from ('customer' as 'a', 'orders' as 'b', and 'salesman' as 'c')
FROM customer a 
-- Performing a left outer join based on the customer_id, including unmatched rows from 'customer'
LEFT OUTER JOIN orders b 
ON a.customer_id = b.customer_id 
-- Performing another left outer join with the result of the previous join and the 'salesman' table based on salesman_id
LEFT OUTER JOIN salesman c 
ON c.salesman_id = b.salesman_id;
```

**Output:**

<img width="1366" height="740" alt="image" src="https://github.com/user-attachments/assets/0ab675f4-eb68-41cf-b2b5-6096c9f5426e" />

**Question 8**
---
<img width="1337" height="598" alt="image" src="https://github.com/user-attachments/assets/2616465e-d9f5-4ed6-8000-e86b346caba8" />


```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1408" height="496" alt="image" src="https://github.com/user-attachments/assets/57bee1b2-4fc6-449a-82e4-2236051bc7bf" />

**Question 9**
---
<img width="1328" height="586" alt="image" src="https://github.com/user-attachments/assets/c6774075-45a3-4b05-b8da-241927faf332" />


```sql
SELECT a.cust_name, a.city, a.grade, 
       b.name AS "Salesman", b.city 
FROM customer a 
LEFT JOIN salesman b 
ON a.salesman_id = b.salesman_id 
ORDER BY a.customer_id;
```

**Output:**

<img width="1368" height="561" alt="image" src="https://github.com/user-attachments/assets/d0481b4b-1399-4515-be00-4f3a58530634" />


**Question 10**
---
<img width="1358" height="434" alt="image" src="https://github.com/user-attachments/assets/69916690-9fd3-4c36-90a1-84b6eac4bffe" />


```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM patients p
INNER JOIN test_results t 
    ON p.patient_id = t.patient_id;

```

**Output:**

<img width="1369" height="341" alt="image" src="https://github.com/user-attachments/assets/167ab83f-f348-45e6-97db-cb2ee621dd19" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
