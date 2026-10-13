## Invalid Tweets

### Problem Statement

Table: Tweets

```sql
Create table If Not Exists Tweets(tweet_id int, content varchar(50))
```

tweet_id is the primary key (column with unique values) for this table.
content consists of alphanumeric characters, '!', or ' ' and no other special characters.
This table contains all the tweets in a social media app.

Write a solution to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.
Return the result table in any order.

### Solution

```sql
SELECT tweet_id
FROM tweets
WHERE LENGTH(content) > 15;
```

### Notes

#### LENGTH in PostgreSQL

In PostgreSQL LENGTH measures the number of characters in a string. In other databases, LENGTH may measure the number of bytes. 