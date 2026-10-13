## Article Views I

### Problem Statement

Table: Views 

```sql
Create table If Not Exists Views (article_id int, author_id int, viewer_id int, view_date date)
```

There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.

Write a solution to find all the authors that viewed at least one of their own articles.
Return the result table sorted by id in ascending order.

### Solution

```sql
SELECT DISTINCT author_id AS id
FROM views
WHERE author_id = viewer_id
ORDER BY id ASC;
```

### Notes

#### Why use DISTINCT?
The problem statement asks for authors that viewed at least one of their own articles. If only the WHERE clause where used, then the query may return rows with the same author_id. 