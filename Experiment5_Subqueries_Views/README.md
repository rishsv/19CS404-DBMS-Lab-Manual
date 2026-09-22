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
```
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

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
```
**Code**
```
SELECT DISTINCT commission
FROM salesman
WHERE salesman_id IN (
    SELECT salesman_id
    FROM customer
    WHERE city = 'Paris'
);
```

**Output:**

<img width="387" height="311" alt="image" src="https://github.com/user-attachments/assets/66add570-6d90-4e02-9521-6af01c2a21e6" />

**Question 2**
```
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
```
**Code**
```
SELECT *
FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**

<img width="1149" height="295" alt="image" src="https://github.com/user-attachments/assets/0ae9cb66-620c-47c6-bb38-f625ca8e49de" />

**Question 3**
```
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```
**Code**
```
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);
```

**Output:**

<img width="425" height="418" alt="image" src="https://github.com/user-attachments/assets/df48e089-fc7c-4a9c-9c95-94102ca009b2" />

**Question 4**
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

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
```
**Code**
```
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="1120" height="296" alt="image" src="https://github.com/user-attachments/assets/7e3064ab-ec91-439d-86b5-673f845e7d1d" />

**Question 5**
```
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
```
**Code**
```
SELECT *
FROM customer
WHERE customer_id = (
    (SELECT salesman_id 
     FROM salesman 
     WHERE name = 'Mc Lyon') - 2001
);
```

**Output:**

<img width="1164" height="272" alt="image" src="https://github.com/user-attachments/assets/99752fef-d555-4002-ada3-a57cd4c267f8" />

**Question 6**
```
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

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
```
**Code**
```
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="1121" height="385" alt="image" src="https://github.com/user-attachments/assets/cfbb09b8-b1eb-4065-86b2-f0c0487586bf" />

**Question 7**
```
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="602" height="233" alt="image" src="https://github.com/user-attachments/assets/ef880aac-3ef2-4587-bd93-73b319b9c2b7" />

```
**Code**
```
SELECT student_name, grade
FROM GRADES g1
WHERE grade = (
    SELECT MIN(grade)
    FROM GRADES g2
    WHERE g2.subject = g1.subject
);
```

**Output:**

<img width="704" height="392" alt="image" src="https://github.com/user-attachments/assets/31ef3b4d-a607-4696-9480-65d7d9638cd7" />

**Question 8**
```
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
```
**Code**
```
SELECT o.ord_no, o.purch_amt, o.ord_date, o.salesman_id
FROM orders o
WHERE o.salesman_id IN (
    SELECT salesman_id
    FROM salesman
    WHERE commission = (SELECT MAX(commission) FROM salesman)
);
```

**Output:**

<img width="942" height="418" alt="image" src="https://github.com/user-attachments/assets/79522bcb-ec70-4365-b316-69b2d8238e4a" />

**Question 9**
```
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
```
**Code**
```
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1282" height="431" alt="image" src="https://github.com/user-attachments/assets/c62600e8-4716-46e4-a513-5774cab99692" />

**Question 10**
```
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER
```
**Code**
```
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);
```

**Output:**

<img width="1282" height="455" alt="image" src="https://github.com/user-attachments/assets/8b730166-98c8-4666-bb2a-403f3db3fb7d" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
