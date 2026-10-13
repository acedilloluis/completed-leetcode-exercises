## Customer Who Visited But Did Not Make Any Transactions

### Problem Statement

Table: Visits

```sql
Create table If Not Exists Visits(visit_id int, customer_id int)
```

visit_id is the column with unique values for this table.
This table contains information about the customers who visited the mall.

Table: Transactions

```sql
Create table If Not Exists Transactions(transaction_id int, visit_id int, amount int)
```

transaction_id is column with unique values for this table.
This table contains information about the transactions made during the visit_id.

Write a solution to find the IDs of the users who visited without making any transactions and the number of times they made these types of visits.

Return the result table sorted in any order.

### Solution

```sql
SELECT customer_id, COUNT(visits.visit_id) AS count_no_trans
FROM visits
WHERE visits.visit_id NOT IN (
    SELECT transactions.visit_id
    FROM transactions
) 
GROUP BY customer_id;
```

### Notes

#### Explanation

The query will first filter out the rows in the visit table where that row's visit_id value is in the transactions table. Then it will group the remaining rows by customer_id and count the number of visit_id's associated to that customer_id. 