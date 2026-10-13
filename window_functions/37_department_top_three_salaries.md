## Department Top Three Salaries

### Problem Statement

Table: Employee 

```sql
Create table If Not Exists Employee (id int, name varchar(255), salary int, departmentId int)
```

id is the primary key (column with unique values) for this table.
departmentId is a foreign key (reference column) of the ID from the Department table.
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.

Table: Department 

```sql
Create table If Not Exists Department (id int, name varchar(255))
```

id is the primary key (column with unique values) for this table.
Each row of this table indicates the ID of a department and its name.

A company's executives are interested in seeing who earns the most money in each of the company's departments. A high earner in a department is an employee who has a salary in the top three unique salaries for that department.

Write a solution to find the employees who are high earners in each of the departments.

Return the result table in any order.
 
Constraints:

- There are no employees with the exact same name, salary and department.

### Solution

```sql
SELECT 
    ranks.department,
    ranks.employee, 
    ranks.salary
FROM (
    SELECT
        department.name AS department,
        employee.name AS employee,
        employee.salary,
        DENSE_RANK() OVER (PARTITION BY department.name ORDER BY employee.salary DESC) AS rank
    FROM employee
    LEFT JOIN department
        ON employee.departmentId = department.id
) AS ranks
WHERE rank BETWEEN 1 AND 3;
```

### Notes

#### Explanation

A subquery is used to rank the salaries for each department. The subquery joins the department table to the employee table by matching departmentId values in the employee table to id values in the department table. It then ranks the salaries within each department using the DENSE_RANK window function and the PARTITION BY statement. DENSE_RANK is used since the solution would like to return the top three salaries for each department including ties. It then ranks those salaries in descending order. The main query then selects the department name, and the employee's names whose salary is in the top three for that department. 