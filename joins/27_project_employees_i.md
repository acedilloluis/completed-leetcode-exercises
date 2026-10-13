## Project Employees I

### Problem Statement

Table: Project

```sql
Create table If Not Exists Project (project_id int, employee_id int)
```

(project_id, employee_id) is the primary key of this table. employee_id is a foreign key to Employee table. Each row of this table indicates that the employee with employee_id is working on the project with project_id.

Table: Employee

```sql
Create table If Not Exists Employee (employee_id int, name varchar(10), experience_years int)
```

employee_id is the primary key of this table. It's guaranteed that experience_years is not NULL. Each row of this table contains information about one employee.

Write an SQL query that reports the average experience years of all the employees for each project, rounded to 2 digits.

Return the result table in any order.

### Solution

```sql
SELECT project_id, ROUND(AVG(experience_years), 2) AS average_years
FROM project
INNER JOIN employee
    ON project.employee_id = employee.employee_id
GROUP BY project_id;
```

### Notes

#### Why INNER JOIN?

Since the goal is to determine the average number of years of experience per project, the query should only look at employees that are assigned to a project. INNER JOIN will only return those rows that have an employee assigned to a project.