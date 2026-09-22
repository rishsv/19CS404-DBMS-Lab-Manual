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
```
How many medical records does each doctor have?

Sample table:MedicalRecords Table

<img width="1089" height="164" alt="image" src="https://github.com/user-attachments/assets/8dff1eef-e045-4380-b1b9-c71a91376aa2" />

```
**Code**
```
SELECT DoctorID,COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY DoctorID;
```
**Output:**

<img width="570" height="559" alt="image" src="https://github.com/user-attachments/assets/272a92a4-4a01-4410-8aae-69a09f5a0b6e" />

**Question 2**
```
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table

<img width="1082" height="154" alt="image" src="https://github.com/user-attachments/assets/47af0123-f601-4d55-b9be-b659cd54f422" />

```
**Code**
```
SELECT Frequency,COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY Frequency;
```
**Output:**

<img width="709" height="477" alt="image" src="https://github.com/user-attachments/assets/ac8ca2ae-a369-4916-936e-0ce031685f7d" />

**Question 3**
```
What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

<img width="998" height="163" alt="image" src="https://github.com/user-attachments/assets/60ba2c23-7273-4b32-be35-7d7ea0b7d066" />

```
**Code**
```
SELECT DoctorID,COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DoctorID;
```
**Output:**

<img width="651" height="562" alt="image" src="https://github.com/user-attachments/assets/f74947bc-ab50-436b-a7a5-d7ea71c36869" />

**Question 4**
```
Write a SQL query to count the number of customers. Return number of customers.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002
```
**Code**
```
SELECT COUNT(cust_name) AS COUNT
FROM customer;
```
**Output:**

<img width="337" height="286" alt="image" src="https://github.com/user-attachments/assets/d0b7937d-6caa-4eaf-865a-f01554b947d2" />

**Question 5**
```
Write a SQL query to find the minimum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```
**Code**
```
SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```
**Output:**

<img width="369" height="279" alt="image" src="https://github.com/user-attachments/assets/df6a5804-0c08-4885-bd90-58321df5f174" />

**Question 6**
```
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```
**Code**
```
SELECT name AS Employee_Name,age AS Age
FROM employee
ORDER BY age ASC
LIMIT 1;
```
**Output:**

<img width="672" height="287" alt="image" src="https://github.com/user-attachments/assets/beba32c1-ea85-4b09-967a-e487a815df94" />

**Question 7**
```
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
```
**Code**
```
SELECT AVG(LENGTH(name)) AS avg_name_length
FROM customer
WHERE city='Chennai';
```
**Output:**

<img width="437" height="280" alt="image" src="https://github.com/user-attachments/assets/b05b5542-8e3e-4d5e-ae5c-ceef7f35270d" />

**Question 8**
```
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.

Sample table: employee1

<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/bf199a83-feb3-40cf-863f-263b641445a2" />

```
**Code**
```
SELECT jdate,AVG(workhour)
FROM employee1
GROUP BY jdate
HAVING AVG(workhour)<10;
```
**Output:**

<img width="590" height="305" alt="image" src="https://github.com/user-attachments/assets/0dc5314f-4639-4355-ba2f-6071497e9e87" />

**Question 9**
```
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1

<img width="1031" height="203" alt="image" src="https://github.com/user-attachments/assets/6c8b066d-6c05-4a62-a324-585d562394b0" />

```
**Code**
```
SELECT occupation,SUM(workhour)
FROM employee1
GROUP BY occupation
HAVING SUM(workhour)>20;
```
**Output:**

<img width="573" height="417" alt="image" src="https://github.com/user-attachments/assets/3c56f97e-0d3f-4b84-9878-199cb2f328bb" />

**Question 10**
```
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1

<img width="992" height="173" alt="image" src="https://github.com/user-attachments/assets/dc79fda8-5891-4782-8c15-a83661ecdf67" />

```
**Code**
```
SELECT (age/5)*5 AS age_group,AVG(age)
FROM customer1
GROUP BY (age/5)*5
HAVING AVG(age)<24;
```
**Output:**

<img width="542" height="280" alt="image" src="https://github.com/user-attachments/assets/9efd4cfc-0811-4f83-a741-c217c4b0ce50" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
