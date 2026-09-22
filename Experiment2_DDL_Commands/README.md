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
```
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE
For example:

Test
pragma table_info('Events');
Result
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EventID     INTEGER     0                       0
1           EventName   TEXT        0                       0
2           EventDate   DATE        0                       0

```

```
CREATE TABLE Events(
    EventID INTEGER,
    EventName TEXT,
    EventDate DATE
);
```

**Output:**

<img width="1332" height="300" alt="image" src="https://github.com/user-attachments/assets/f4e4ad04-f37f-4b09-9cbc-ca2fc856d9de" />


**Question 2**
```
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Result
Error: FOREIGN KEY constraint failed

```
```
CREATE TABLE ProjectAssignments(
    AssignmentID INTEGER,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1706" height="264" alt="image" src="https://github.com/user-attachments/assets/c9289a89-7e60-40ec-a0bc-9e33a7007392" />


**Question 3**
```
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	
pragma table_info('Student_details');
Result
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0
```

```
ALTER TABLE student_details
ADD MobileNumber NUMBER;
ALTER TABLE student_details
ADD Address VARCHAR(100);
```

**Output:**

<img width="1275" height="293" alt="image" src="https://github.com/user-attachments/assets/cfd12868-34d4-4ed7-ade0-010e46cf2471" />

**Question 4**
```
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
Result
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000

```
```
CREATE TABLE jobs(
    job_id INTEGER PRIMARY KEY,
    job_title TEXT UNIQUE DEFAULT '',
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER NULL
);
```
**Output:**

<img width="1635" height="305" alt="image" src="https://github.com/user-attachments/assets/46f1346a-c069-4a50-9974-a7149c8985c0" />

**Question 5**
```
In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

For example:

Test	
SELECT * FROM Employee;
Result
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT

```
```
INSERT INTO Employee(EmployeeID,Name,Position)
VALUES
(5,'George Clark','Consultant');
INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES
(7,'Noah Davis','Manager','HR',60000);
INSERT INTO Employee(EmployeeID,Name,Position,Department)
VALUES
(8,'Ava Miller','Consultant','IT');

```
**Output:**

<img width="1221" height="270" alt="image" src="https://github.com/user-attachments/assets/b80e0294-ba4a-47f7-bef7-0e82462b8ba5" />

**Question 6**
```
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	
select * from Products;
Result
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5

```
```
INSERT INTO Products
SELECT *FROM Discontinued_products;
```
**Output:**

<img width="1252" height="272" alt="image" src="https://github.com/user-attachments/assets/4743e739-67d9-4747-81dc-809485bc7f9b" />

**Question 7**
```
Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.
For example:

Test	
INSERT INTO Bonuses (BonusID, EmployeeID, BonusAmount, BonusDate, Reason) VALUES (1, 6, 1000.0, '2024-08-01', 'Outstanding performance');
SELECT * FROM Bonuses;
Result
BonusID     EmployeeID  BonusAmount  BonusDate   Reason
----------  ----------  -----------  ----------  -----------------------
1           6           1000.0       2024-08-01  Outstanding performance

```
```
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK(BonusAmount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
); 
```
**Output:**

<img width="1847" height="234" alt="image" src="https://github.com/user-attachments/assets/172a8690-f34e-47f4-8779-c28be565157b" />

**Question 8**
```
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Result
Error: FOREIGN KEY constraint failed

```
```
CREATE TABLE Shipments(
    ShipmentID INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID INTEGER,
    OrderId INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```
**Output:**

<img width="1234" height="202" alt="image" src="https://github.com/user-attachments/assets/a799acc2-0899-4390-a18d-a007124005b2" />

**Question 9**
```
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

For example:

Test	
pragma table_info('Companies');
Result
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           first_name  varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           mobilenumb  number      0                       0
6           DOB         Date        0                       0
```
```
ALTER TABLE Companies
RENAME name TO first_name;
ALTER TABLE Companies
ADD mobilenumber number;
ALTER TABLE Companies
ADD DOB Date;

```
**Output:**

<img width="1274" height="302" alt="image" src="https://github.com/user-attachments/assets/87851ed9-e011-4d83-b110-1f2b60e71106" />

**Question 10**
```
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values.    
For example:

Test	
SELECT EmployeeID, Name, Position 
FROM Employee;
Result
EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

```
```
INSERT INTO Employee(EmployeeID,Name,Position)
VALUES
(4,'Emily White','Analyst');
```
**Output:**

<img width="893" height="268" alt="image" src="https://github.com/user-attachments/assets/88a2c574-f9fc-4810-8490-7bb7d3ac1045" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
