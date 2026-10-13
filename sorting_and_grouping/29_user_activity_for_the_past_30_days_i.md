## User Activity For The Past 30 Days I

### Problem Statement

Table: Activity 

```sql
Create table If Not Exists Activity (user_id int, session_id int, activity_date date, activity_type ENUM('open_session', 'end_session', 'scroll_down', 'send_message'))
```

This table may have duplicate rows. The activity_type column is an ENUM (category) of type ('open_session', 'end_session', 'scroll_down', 'send_message'). The table shows the user activities for a social media website. Note that each session belongs to exactly one user.

Write a solution to find the daily active user count for a period of 30 days ending 2019-07-27 inclusively. A user was active on someday if they made at least one activity on that day. Return the result table in any order.

### Solution

```sql
SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users
FROM activity
GROUP BY activity_date
HAVING activity_date > '2019-06-27'
    AND activity_date <= '2019-07-27';
```

### Notes

#### Explanation

The query first groups the rows in the activity table by activity_date. It then filters the grouped rows to only include those with activity_date within the desired range. From these rows it counts the distinct number of user_id's associated with a particular activity_date. 
