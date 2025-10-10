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
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.


```sql
insert into Employee(EmployeeID,Name,Position,Department,Salary)values(001,"Sarah Parker","Manager","HR",60000)
```

**Output:**

<img width="1221" height="313" alt="image" src="https://github.com/user-attachments/assets/6bd31510-8321-4c95-9727-9d1a8ec3757f" />


**Question 2**
---
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE

```sql
Create table Employees
(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE
);
```

**Output:**

<img width="1218" height="383" alt="image" src="https://github.com/user-attachments/assets/dac1dccd-28b3-4d22-a580-70b58fd8c358" />


**Question 3**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
Create table Invoices
(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
Amount REAL check(Amount > 0),
DueDate DATE check(DueDate > InvoiceDate),
OrderID INTEGER,
foreign key(OrderID) references Orders(OrderID));
```

**Output:**

<img width="1223" height="356" alt="image" src="https://github.com/user-attachments/assets/d608b770-a347-4ba6-a123-d88db4bd7e60" />


**Question 4**
---
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375

```sql
insert into Customers(CustomerID,Name,Address,City,ZipCode)values(306,"Diana Prince","Themyscira",NULL,NULL),(307,"Bruce Wayne","Wayne Mano","Gotham",10007),(308,"Peter Parker","Queens",NULL,11375)

```

**Output:**

<img width="1219" height="342" alt="image" src="https://github.com/user-attachments/assets/2439e5fa-6ef9-4379-b05b-6041a04f550a" />


**Question 5**
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
Create table item
(
item_id TEXT primary key,
item_desc TEXT not NULL,
rate INTEGER not NULL,
icom_id TEXT check(length(icom_id = 4)),
foreign key(icom_id) references company(com_id)ON UPDATE SET NULL ON DELETE SET NULL);
```

**Output:**

<img width="1222" height="427" alt="image" src="https://github.com/user-attachments/assets/b99c40d5-071e-41b0-9858-e45d61f606a9" />


**Question 6**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
Create table Shipments
(
ShipmentID INTEGER primary key,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key(SupplierID) references Suppliers(SupplierID),
foreign key(OrderID) references Orders(OrderID));
```

**Output:**

<img width="1222" height="309" alt="image" src="https://github.com/user-attachments/assets/85c9618c-40a5-4301-acc1-3e931ad53cf4" />



**Question 7**
---
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.

```sql
Create table Bonuses
(
BonusID INTEGER primary key,
EmployeeID INTEGER,
BonusAmount REAL check(BonusAmount > 0),
BonusDate Date,
Reason TEXT not NULL,
foreign key(EmployeeID) references Employees(EmployeeID));
```

**Output:**

<img width="1217" height="354" alt="image" src="https://github.com/user-attachments/assets/67ed1765-6bb5-4c04-998e-d7dafb3f223e" />


**Question 8**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary



```sql
insert into Employee(EmployeeID,Name,Department,Salary) select EmployeeID,Name,Department,Salary from Former_employees
```

**Output:**

<img width="1226" height="338" alt="image" src="https://github.com/user-attachments/assets/3e4bdb69-50f4-4bf2-abb0-8c95b23f76cc" />


**Question 9**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
Create table Invoices
(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
DueDate DATE check(DueDate > InvoiceDate),
Amount REAL check(Amount > 0));
```

**Output:**

<img width="1210" height="345" alt="image" src="https://github.com/user-attachments/assets/872d1d0e-0775-411a-afc3-94a77a75fe92" />


**Question 10**
---
Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```sql
ALTER TABLE Student_details
add column Date_of_birth Date
```

**Output:**

<img width="1217" height="426" alt="image" src="https://github.com/user-attachments/assets/f0ab3968-70f8-4c69-b6d1-a3ad14b8d4e2" />
**Output:**
<img width="1902" height="1073" alt="Screenshot 2025-10-10 111804" src="https://github.com/user-attachments/assets/2e994fa4-84d6-46e2-9904-1913610f7274" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
