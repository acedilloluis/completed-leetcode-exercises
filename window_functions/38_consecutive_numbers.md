## Consecutive Numbers

### Problem Statement

Table: Logs 

```sql
Create table If Not Exists Logs (id int, num int)
```

id is the primary key for this table.
id is an autoincrement column starting from 1.

Find all numbers that appear at least three times consecutively.

Return the result table in any order.

### Solution

```sql
SELECT DISTINCT num AS consecutivenums
FROM (
    SELECT
        num,
        LAG(num, 1) OVER (ORDER BY id) AS previous_num,
        LEAD(num, 1) OVER (ORDER BY id) AS next_num
    FROM logs
)
WHERE num = previous_num
    AND num = next_num;
```

### Notes

#### LAG and LEAD

LAG and LEAD are window_functions that access the previous OFFSET row or the next OFFSET row, respectively. Note that PARTITION BY may passed, but ORDER BY is required.

#### Explanation

Since the solution asks for numbers that repeats at least three times consecutively, it is only necessary to check whether a num repeats three times consecutively and then return those distinct numbers that repeat three times consecutively. LAG and LEAD are used to check the previous row and the next row, respectively.