# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition; 
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
```
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
```
**Code**
```
UPDATE employees
SET email='Unavailable'
```

**Output:**

<img width="1259" height="394" alt="image" src="https://github.com/user-attachments/assets/60393f77-df55-4413-b3a5-b0fc647cb8a5" />

**Question 2**
```
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
```
**Code**
```
UPDATE Employees
SET salary=ROUND(salary*1.25)
WHERE department_id=40;

UPDATE Employees
SET salary=ROUND(salary*1.15)
WHERE department_id=90;

UPDATE Employees
SET salary=ROUND(salary*1.10)
WHERE department_id=110;


```

**Output:**

<img width="1819" height="342" alt="image" src="https://github.com/user-attachments/assets/c4a9f21d-7db3-4a86-9b11-0fe09fdd86ad" />

**Question 3**
```
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
```
**Code**
```
UPDATE PRODUCTS
SET reorder_lvl=40
WHERE category='Grocery'
```

**Output:**

<img width="1839" height="265" alt="image" src="https://github.com/user-attachments/assets/0e761b81-c86e-44fd-b718-e0ae96a8d632" />

**Question 4**
```
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
```
**Code**
```
UPDATE Suppliers
SET address='58 Lakeview, Magnolia'
WHERE supplier_id=5
```

**Output:**

<img width="1894" height="269" alt="image" src="https://github.com/user-attachments/assets/1b4aff5e-78b0-460f-b69a-c158bfe5829b" />

**Question 5**
```
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

```
**Code**
```
UPDATE PRODUCTS
SET sell_price = CAST(cost_price*1.35 AS INT)
WHERE ((sell_price-cost_price)/sell_price)*100<30;

```

**Output:**

<img width="1736" height="342" alt="image" src="https://github.com/user-attachments/assets/cd6ce2a9-7466-4003-b22f-9a7c35f936b2" />

**Question 6**
```
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
**Code**
```
DELETE FROM Customer
WHERE cust_country='India'
AND cust_city!='Chennai';
```

**Output:**

<img width="1896" height="476" alt="image" src="https://github.com/user-attachments/assets/34289f01-3053-4bbe-80ea-1a3cbf7a1d1a" />

**Question 7**
```
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
**Code**
```
DELETE FROM Doctors
WHERE specialization='Cardiology'
```

**Output:**

<img width="1175" height="333" alt="image" src="https://github.com/user-attachments/assets/be23feb6-5b7b-40a2-ab48-f78ac9011246" />

**Question 8**
```
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```
**Code**
```
DELETE FROM Doctors
WHERE last_name IS NULL;
```

**Output:**

<img width="1189" height="636" alt="image" src="https://github.com/user-attachments/assets/2d4710a5-47bc-427c-9c50-937bb8141792" />

**Question 9**
```
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
**Code**
```
DELETE FROM Customer
WHERE GRADE=2
AND CUST_NAME LIKE 'M%'
AND PAYMENT_AMT<3000;
```

**Output:**

<img width="1895" height="237" alt="image" src="https://github.com/user-attachments/assets/ea4392ad-671c-46f7-b735-a8b4d05f0f47" />

**Question 10**
```
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
```
**Code**
```
DELETE FROM Surgeries
WHERE surgery_date = '2024-02-28'
```

**Output:**

<img width="1268" height="354" alt="image" src="https://github.com/user-attachments/assets/978220e6-da96-4d70-9759-7c40c2f4c647" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
