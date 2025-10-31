# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)



```sql
SELECT department_id,
       department_name
FROM Departments
WHERE LENGTH(department_name) >
      (SELECT AVG(LENGTH(department_name))
       FROM Departments);

```

**Output:**

<img width="1285" height="493" alt="image" src="https://github.com/user-attachments/assets/03c304a2-0fe8-4845-97c3-ca0afade8218" />


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
select * from CUSTOMERS where salary = '1500'
```

**Output:**

<img width="1276" height="423" alt="image" src="https://github.com/user-attachments/assets/419993cb-98da-4575-9952-0ba34e8ff04f" />


**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
select * from CUSTOMERS where salary < '2500'
```

**Output:**

<img width="1280" height="548" alt="image" src="https://github.com/user-attachments/assets/8ca6e3d2-a099-408c-b186-03a83f0fc771" />


**Question 4**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
SELECT ord_no,
       purch_amt,
       ord_date,
       salesman_id
FROM orders
WHERE salesman_id IN (
      SELECT salesman_id
      FROM salesman
      WHERE commission = (
            SELECT MAX(commission)
            FROM salesman
      )
)

```

**Output:**

<img width="1284" height="560" alt="image" src="https://github.com/user-attachments/assets/29f032bf-0adc-47dc-8619-895be5fb7c53" />


**Question 5**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name   city
-----  ---------------
Neha   Bangalore
Rohit  Bangalore
Manoj  Bangalore
Vivek  Chandigarh


```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
)

```

**Output:**

<img width="1290" height="547" alt="image" src="https://github.com/user-attachments/assets/2a137276-3da9-4ec9-82c4-bd05899ffb1a" />


**Question 6**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

```sql
select id,name,age,city,income 
from Employee 
where age <
(select avg(age)
from Employee
where income > '250000')
```

**Output:**

<img width="1288" height="617" alt="image" src="https://github.com/user-attachments/assets/44eec51b-ff7d-4e4a-8386-67d9c660d5ea" />


**Question 7**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



```sql
SELECT student_id,
       student_name,
       subject,
       grade
FROM Grades
WHERE (subject, grade) IN (
      SELECT subject,
             MIN(grade)
      FROM Grades
      GROUP BY subject
)

```

**Output:**

<img width="1290" height="542" alt="image" src="https://github.com/user-attachments/assets/d4b77d8b-1fec-49c7-88e0-73ba212ea9fd" />


**Question 8**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT id,
       name,
       city,
       email,
       phone
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
)

```

**Output:**

<img width="1292" height="591" alt="image" src="https://github.com/user-attachments/assets/038ce19f-a87a-40c3-b1ee-f83b7939f1c5" />


**Question 9**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int

```sql
SELECT customer_id,
       cust_name,
       city,
       grade,
       salesman_id
FROM customer
WHERE customer_id = (
      SELECT salesman_id
      FROM salesman
      WHERE name = 'Mc Lyon'
) - 2001
```

**Output:**

<img width="1287" height="392" alt="image" src="https://github.com/user-attachments/assets/959ed95b-4b25-4eb7-9abe-1be8b6be50b5" />


**Question 10**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER


```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
)

```

**Output:**

<img width="1291" height="537" alt="image" src="https://github.com/user-attachments/assets/8abf3144-7ead-4186-b5b6-1ec6fea0acde" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
