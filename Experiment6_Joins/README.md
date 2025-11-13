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
![Screenshot 2025-04-29 174738](https://github.com/user-attachments/assets/290f6cc3-7622-40ec-bce9-baab7ccc99d4)

```
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM 
    patients p
INNER JOIN 
    test_results t ON p.patient_id = t.patient_id;
```

**Output:**
![Screenshot 2025-04-29 174918](https://github.com/user-attachments/assets/b84a6bd2-6f8f-4d38-837b-57166978d12b)



**Question 2**
![Screenshot 2025-04-29 174935](https://github.com/user-attachments/assets/e7d12367-c15c-4650-9777-4ad31d543d8f)

```
SELECT 
    s.name,
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c ON s.salesman_id = c.salesman_id
WHERE 
    s.salesman_id IN (
        SELECT salesman_id
        FROM customer
        GROUP BY salesman_id
        HAVING COUNT(*) > 1
    );
```
**Output:**

![Screenshot 2025-04-29 175002](https://github.com/user-attachments/assets/9a0ed5bd-f6dd-46e5-bcaa-495473df23de)


**Question 3**
![Screenshot 2025-04-29 175112](https://github.com/user-attachments/assets/3879d1c5-55f5-49fe-a2f3-b2032876f3d2)
```
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
INNER JOIN 
    customer c ON o.customer_id = c.customer_id
INNER JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```
**Output:**
![Screenshot 2025-04-29 175130](https://github.com/user-attachments/assets/91bab884-416d-4095-80a2-eb16a2630085)



**Question 4**
![Screenshot 2025-04-29 175137](https://github.com/user-attachments/assets/831a0f4d-2857-4f9f-aede-73aa34685bb9)
```

SELECT 
    n.nurse_id,
    d.department_name
FROM 
    nurses n
INNER JOIN 
    departments d ON n.department_id = d.department_id
WHERE 
    n.first_name = 'David'
    AND n.last_name = 'Moore';

```
**Output:**

![Screenshot 2025-04-29 175158](https://github.com/user-attachments/assets/af46f22f-0ab2-417c-aef5-e582ca72804a)

**Question 5**
```
![Screenshot 2025-04-29 175209](https://github.com/user-attachments/assets/cc47527b-5baf-4234-8d7a-b2abb0c994ac)


SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.city AS "city",
    s.commission
FROM 
    customer c
INNER JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    c.city <> s.city
    AND s.commission > 0.12;

```
**Output:**
![Screenshot 2025-04-29 175224](https://github.com/user-attachments/assets/413a432c-dd89-4e8f-8288-f00abffeb5b8)


**Question 6**
![Screenshot 2025-04-29 175237](https://github.com/user-attachments/assets/7393e493-d969-4937-b0cc-af18d6b6c084)
```
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```
**Output:**

![Screenshot 2025-04-29 175258](https://github.com/user-attachments/assets/c8ecdbbc-d9e5-4a57-abe8-6199aca67f20)


**Question 7**

![Screenshot 2025-04-29 175310](https://github.com/user-attachments/assets/14ffae86-0cbe-475d-91cc-ace6e344cfaf)

```
SELECT 
    p.*
FROM 
    patients p
INNER JOIN 
    test_results t ON p.patient_id = t.patient_id
WHERE 
    t.test_name = 'X-Ray'
    AND t.result = 'Normal';
```
**Output:**
![Screenshot 2025-04-29 175327](https://github.com/user-attachments/assets/7b590030-6408-4316-b579-cb8b6b87ee9b)



**Question 8**
![Screenshot 2025-04-29 175339](https://github.com/user-attachments/assets/8624974e-1ab4-4f28-8ebb-0480e40ad829)
```
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;
```
**Output:**

![Screenshot 2025-04-29 175357](https://github.com/user-attachments/assets/073e1b8f-b132-4cbe-a19c-75b1121caa64)


**Question 9**
![Screenshot 2025-04-29 175406](https://github.com/user-attachments/assets/d536876a-3e8d-45ef-8de3-30c2c6286eef)
```
SELECT 
    c.cust_name,
    s.name
FROM 
    customer c
LEFT JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    c.city = s.city;
```
**Output:**

![Screenshot 2025-04-29 175420](https://github.com/user-attachments/assets/b383cc08-9b59-455a-89bc-b04b9194b2bd)


**Question 10**
![Screenshot 2025-04-29 175428](https://github.com/user-attachments/assets/09a5d616-b0ae-4a08-a609-a8acac6d3c71)

```
SELECT 
    c.cust_name AS "Customer Name",
    c.city AS "city",
    s.name AS "Salesman",
    s.commission AS "commission"
FROM 
    customer c
JOIN 
    salesman s ON c.salesman_id = s.salesman_id;
```
**Output:**

![Screenshot 2025-04-29 175443](https://github.com/user-attachments/assets/46d235a3-4449-4eaa-add0-2b863fde835e)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
