## Product Sales Analysis I

### Problem Statement

Table: Sales

```sql
Create table If Not Exists Sales (sale_id int, product_id int, year int, quantity int, price int)
```

(sale_id, year) is the primary key (combination of columns with unique values) of this table. product_id is a foreign key (reference column) to Product table. Each row of this table shows a sale on the product product_id in a certain year. Note that the price is per unit.

Table: Product

```sql
Create table If Not Exists Product (product_id int, product_name varchar(10))
```

product_id is the primary key (column with unique values) of this table. Each row of this table indicates the product name of each product.

Write a solution to report the product_name, year, and price for each sale_id in the Sales table.

Return the resulting table in any order.

### Solution

```sql
SELECT product_name, year, price
FROM sales
INNER JOIN product
    ON sales.product_id = product.product_id;
```

### Notes

#### Why INNER JOIN?

Since product_id is the primary key in the product table and the foreign key in the sales table, the query can match the rows from each table using the product_id. 