## Average Time Of Process Per Machine

### Problem Statement

Table: Activity 

```sql
Create table If Not Exists Activity (machine_id int, process_id int, activity_type ENUM('start', 'end'), timestamp float)
```

The table shows the user activities for a factory website.
(machine_id, process_id, activity_type) is the primary key (combination of columns with unique values) of this table.
machine_id is the ID of a machine.
process_id is the ID of a process running on the machine with ID machine_id.
activity_type is an ENUM (category) of type ('start', 'end').
timestamp is a float representing the current time in seconds.
'start' means the machine starts the process at the given timestamp and 'end' means the machine ends the process at the given timestamp.
The `start` timestamp will always be less than or equal to the `end` timestamp for every `(machine_id, process_id)` pair.
It is guaranteed that each (machine_id, process_id) pair has a 'start' and 'end' timestamp.
 
There is a factory website that has several machines, each running one or more processes.

Write a solution to find the average time each machine takes to complete a process.

The time to complete a process is the 'end' timestamp minus the 'start' timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run on that machine.

The resulting table should have the machine_id along with the average time as processing_time, which should be rounded to 3 decimal places.
Return the result table in any order.

### Solution

```sql
WITH totals_per_machine AS (
    SELECT
        machine_id,
        SUM(
            CASE
                WHEN activity_type = 'start' THEN -activity.timestamp
                ELSE activity.timestamp
            END
        ) AS total_time_to_complete_processes,
        COUNT(DISTINCT process_id) AS total_processes
    FROM activity
    GROUP BY machine_id
)

SELECT
    DISTINCT activity.machine_id,
    ROUND(
        (total_time_to_complete_processes / total_processes)::decimal,
        3
    ) AS processing_time
FROM activity
INNER JOIN totals_per_machine
    ON activity.machine_id = totals_per_machine.machine_id;
```

### Notes

#### Explanation

A CTE is first used to find the total time to complete a process per machine and the total number of distinct processes running per machine by grouping the rows by machine_id and then using the aggregate functions SUM and COUNT. The main query then joins the CTE to the activity table by matching machine_id values. It then finds the processing time and rounds to the desired accuracy. 