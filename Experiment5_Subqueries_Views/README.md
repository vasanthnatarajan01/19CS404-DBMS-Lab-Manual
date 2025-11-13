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
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh      32          Ahmedabad         2000
2          Khilan      25          Delhi             1500
3          Kaushik     23          Kota              2000
4          Chaitali    25          Mumbai            6500
5          Hardik      27          Bhopal            8500
6          Komal       22          Hyderabad         4500
7           Muffy      24          Indore           10000

```sql
SELECT * 
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi' AND AGE < 30
ORDER BY ID;

```

**Output:**

![Screenshot 2025-05-05 141151](https://github.com/user-attachments/assets/69ac48d5-a35f-410d-88dd-825a18dd0055)


**Question 2**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT * 
FROM GRADES g
WHERE grade = (
    SELECT MIN(grade) 
    FROM GRADES 
    WHERE subject = g.subject
);

```

**Output:**
![Screenshot 2025-05-05 141244](https://github.com/user-attachments/assets/63b356b3-6440-4832-a259-b1b19fba7bd9)


**Question 3**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name              varchar(30)
city              varchar(15)
commission        decimal(5,2)

customer table

name              type
-----------       ----------
customer_id      int
cust_name        text
city             text
grade            int
salesman_id      int

```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;

```

**Output:**
![Screenshot 2025-05-05 141405](https://github.com/user-attachments/assets/6756877a-a2cb-4955-b766-4c2b38c8c0ae)


**Question 4**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name             varchar(30)
city             varchar(15)
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
SELECT *
FROM customer
WHERE customer_id = (
    SELECT salesman_id - 2001
    FROM salesman
    WHERE name = 'Mc Lyon'
);

```

**Output:**

![Screenshot 2025-05-05 141513](https://github.com/user-attachments/assets/156ab547-f3f1-430d-85c7-1aece8df1395)

**Question 5**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

![Screenshot 2025-05-05 141617](https://github.com/user-attachments/assets/a739fcd2-5493-4b67-91d9-9949226e3ac4)


**Question 6**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);

```

**Output:**

![Screenshot 2025-05-05 141721](https://github.com/user-attachments/assets/a67c7ffb-251b-4b6d-b93c-1b8242c3db47)


**Question 7**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name             varchar(30)
city             varchar(15)
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
SELECT
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    o.salesman_id
FROM orders o
WHERE
    o.salesman_id IN (
    SELECT salesman_id FROM salesman 
    ORDER BY commission DESC LIMIT 1);
```

**Output:**
![Screenshot 2025-05-05 141855](https://github.com/user-attachments/assets/2ec5f2f1-71a6-436f-bfd8-3a33f1e91594)


**Question 8**
---Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

```sql
SELECT student_id, student_name, subject, grade
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);

```

**Output:**



**Question 9**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name             varchar(30)
city             varchar(15)
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
SELECT
    ord_no,purch_amt,ord_date,customer_id,salesman_id FROM orders
WHERE
    salesman_id IN (
    SELECT salesman_id FROM salesman WHERE city = 'London');
```

**Output:**

![Screenshot 2025-05-05 142108](https://github.com/user-attachments/assets/4c9edd61-da38-4317-861f-7347b75e1ad7)


**Question 10**
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

```sql
SELECT DISTINCT name,city FROM customer
WHERE city IN (
        SELECT city FROM customer WHERE id IN (3, 7));
```

**Output:**
![Screenshot 2025-05-05 142221](https://github.com/user-attachments/assets/8d199b30-3b50-4230-acda-69f78b662416)


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
