## Replace Employee Id With The Unique Identifier

### Problem Statement

Table: Employees 

```sql
Create table If Not Exists Employees (id int, name varchar(20))
```

id is the primary key (column with unique values) for this table.
Each row of this table contains the id and the name of an employee in a company.

Table: EmployeeUNI 

```sql
Create table If Not Exists EmployeeUNI (id int, unique_id int)
```

(id, unique_id) is the primary key (combination of columns with unique values) for this table.
Each row of this table contains the id and the corresponding unique id of an employee in the company.

Write a solution to show the unique ID of each user, If a user does not have a unique ID replace just show null.
Return the result table in any order.

### Solution

```sql
SELECT unique_id, name
FROM employees
LEFT JOIN employeeuni
    ON employees.id = employeeuni.id;
```

### Notes

#### Why use LEFT JOIN?

Since the solution asks to return NULL if a user does not have a unique id, using LEFT JOIN, and matching on the id value of the employees table with the id value in the employeeuni table, will keep every employee in the employees table and assign a NULL value to the unique id column if that employee's id is not contained in the employeeuni table.