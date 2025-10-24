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
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
select cast(ValidityPeriod as integer) as ValidityYear, count(*) as TotalPatients from Insurance group by ValidityYear 
```

**Output:**

<img width="1236" height="478" alt="image" src="https://github.com/user-attachments/assets/241316f0-9a27-47f4-b134-21d1a8cffe42" />


**Question 2**
---
How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT

```sql
select strftime('%H',AppointmentDateTime) as HourOfDay, count (*) as TotalAppointments from Appointments group by HourOfDay
```

**Output:**

<img width="1238" height="616" alt="image" src="https://github.com/user-attachments/assets/d78e5d5a-2d51-4e64-9c99-c48a9469f4d1" />

**Question 3**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT

```sql
select patientID,count (*) as TotalAppointments from Appointments group by patientID
```

**Output:**

<img width="1235" height="717" alt="image" src="https://github.com/user-attachments/assets/084258e9-c569-457d-ba63-e3557809ed57" />


**Question 4**
---
Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```sql
select name, length(name) as length from customer order by length(name) DESC LIMIT 1
```

**Output:**

<img width="1232" height="404" alt="image" src="https://github.com/user-attachments/assets/00a451c6-715e-4f48-8c4d-eb6499cccc3a" />


**Question 5**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select avg(purch_amt) as AVERAGE from orders
```

**Output:**

<img width="1234" height="397" alt="image" src="https://github.com/user-attachments/assets/2e07a0ad-7099-426d-872e-ca61cfe45e18" />


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

```sql
select count(*) as employees_count from employee where income > 50000
```

**Output:**

<img width="1237" height="396" alt="image" src="https://github.com/user-attachments/assets/15c8476a-1a84-44bb-871e-75e5d7fe99a5" />


**Question 7**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000



```sql
select count(*) as COUNT from employee where age > 32
```

**Output:**

<img width="1228" height="399" alt="image" src="https://github.com/user-attachments/assets/7a8ff7cb-1526-4cd4-b5fa-f8ab577438ed" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.

Sample table: employee



```sql
select age, AVG(income) from employee group by age having AVG(income) between 300000 and 500000
```

**Output:**

<img width="1238" height="420" alt="image" src="https://github.com/user-attachments/assets/55eaf74d-654b-4a08-80ac-e7a35433f47b" />


**Question 9**
---
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products



```sql
select category_id, sum(price) as Total_Cost from products group by category_id having Total_Cost > 50
```

**Output:**

<img width="1232" height="426" alt="image" src="https://github.com/user-attachments/assets/e4a076ac-4316-4b9d-a31e-a89e8e353083" />


**Question 10**
---
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

Sample table: products



```sql
select category_id,count(*) as COUNT from products group by category_id having category_id > 2
```

**Output:**

<img width="1227" height="420" alt="image" src="https://github.com/user-attachments/assets/e0e4a7f0-98f6-47ab-95e0-2b67e26e6e96" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
