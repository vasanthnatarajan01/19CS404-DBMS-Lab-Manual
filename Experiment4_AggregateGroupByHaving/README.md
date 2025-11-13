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
How many medical records were created in each month?

Sample table:MedicalRecords Table

<img width="1089" height="164" alt="image (6)" src="https://github.com/user-attachments/assets/c66e9cfd-6b77-46e0-975d-f6f626654ad6" />


```sql
SELECT strftime('%Y-%m', Date) AS Month, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY Month
ORDER BY Month;
```

**Output:**

<img width="574" height="410" alt="image" src="https://github.com/user-attachments/assets/3ae13b16-f60d-4518-a562-b9968ddbcc0f" />


**Question 2**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table

<img width="1089" height="164" alt="image (6) (1)" src="https://github.com/user-attachments/assets/1b84056f-0c3f-4695-9b89-82dd369696f1" />



```sql
SELECT PatientID, COUNT(Medications) AS AvgMedications
FROM MedicalRecords GROUP BY PatientID;
```

**Output:**

<img width="610" height="584" alt="image-1" src="https://github.com/user-attachments/assets/cd877944-903e-4c86-a8ad-734e8552966e" />


**Question 3**
---
How many patients are there in each city?

Sample table: Patients Table

<img width="1076" height="161" alt="image (3)" src="https://github.com/user-attachments/assets/5c282d0e-f9a0-4e6c-9775-8bd764941669" />


```sql
SELECT Address, COUNT(PatientID) AS TotalPatients 
FROM Patients
GROUP BY Address;
```

**Output:**

<img width="588" height="381" alt="image-2" src="https://github.com/user-attachments/assets/e81e5554-49f5-4b1c-8e2f-d7daab654d09" />


**Question 4**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.

Sample table: orders
```
ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001
```

```sql
SELECT COUNT(DISTINCT Salesman_id) COUNT FROM orders;
```

**Output:**

<img width="325" height="291" alt="image-3" src="https://github.com/user-attachments/assets/ec92a212-c529-4eef-b8a0-e15695b3dab5" />


**Question 5**
---
Write a SQL query to find how many employees have an income greater than 50K?

Table: employee
```
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```

```sql
SELECT COUNT(id) AS employees_count FROM employee WHERE income > 50000;
```

**Output:**

<img width="411" height="295" alt="image-4" src="https://github.com/user-attachments/assets/fbb8903f-ad36-4a82-b554-2f4162aa0933" />


**Question 6**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer
```
name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
```

```sql
SELECT AVG(LENGTH(email)) AS avg_email_length FROM customer;
```

**Output:**

<img width="419" height="278" alt="image-5" src="https://github.com/user-attachments/assets/1e62a36e-4e94-427d-99e7-db21e81c7995" />


**Question 7**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee
```
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
```

```sql
SELECT SUM(income) AS total_income FROM employee WHERE age >= 40;
```

**Output:**

<img width="356" height="290" alt="image-6" src="https://github.com/user-attachments/assets/c5b38e34-7c19-49b4-97f8-cba289859db3" />


**Question 8**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1


<img width="992" height="173" alt="unnamed" src="https://github.com/user-attachments/assets/ce6eb388-c23e-48b0-9eca-e72f376b1253" />

```sql
SELECT (age/5) * 5 AS age_group, MAX(salary)
FROM customer1
GROUP BY age_group
HAVING MAX(salary) > 8000;
```

**Output:**

<img width="558" height="336" alt="image-7" src="https://github.com/user-attachments/assets/b95f6bbb-9ee6-4cc4-a976-7a194e969a5d" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1

<img width="992" height="173" alt="unnamed (1)" src="https://github.com/user-attachments/assets/caf0b698-b334-4621-950c-542b7651e507" />

```sql
SELECT address, SUM(salary) FROM customer1 GROUP BY address HAVING SUM(salary) > 2000;
```

**Output:**

<img width="553" height="457" alt="image-8" src="https://github.com/user-attachments/assets/74e247da-dc59-42a8-b65b-06b8160a3963" />

**Question 10**
---
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

Sample table: products

<img width="972" height="212" alt="unnamed (2)" src="https://github.com/user-attachments/assets/c42200b6-9728-437a-8229-ca6d6b2f2ea6" />

```sql
SELECT category_id, SUM(price) AS Total_Cost FROM products GROUP BY category_id HAVING Total_Cost > 50;
```

**Output:**


<img width="555" height="309" alt="image-9" src="https://github.com/user-attachments/assets/bf2b6eeb-5ca7-4b32-a15a-493203bfdd51" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

