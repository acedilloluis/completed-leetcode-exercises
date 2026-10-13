## Sales Analysis III

### Problem Statement

Table: Product

```sql
Create table If Not Exists Product (product_id int, product_name varchar(10), unit_price int)
```

product_id is the primary key (column with unique values) of this table. Each row of this table indicates the name and the price of each product.

Table: Sales

```sql
Create table If Not Exists Sales (seller_id int, product_id int, buyer_id int, sale_date date, quantity int, price int)
```

This table can have duplicate rows. product_id is a foreign key (reference column) to the Product table. Each row of this table contains some information about one sale.

Write a solution to report the products that were only sold in the first quarter of 2019. That is, between 2019-01-01 and 2019-03-31 inclusive.

Return the result table in any order.

### Solution

```sql
SELECT 
	product.product_id, 
	product.product_name
FROM product
WHERE 
	product.product_id NOT IN (
		SELECT product_id
		FROM sales
		WHERE 
			sale_date > '2019-03-31'
			OR sale_date < '2019-01-01'
	) 
	AND product.product_id IN (
		SELECT product_id
		FROM sales
	);
```

### Notes

#### Explanation

For each row in the product table, the query will run two subqueries. One subquery will check that the product_id value for that row was not sold either before 2019-01-01 or after 2019-03-31. The second subquery will check that the product_id is contained in the sales table, since the first subquery may return a row that was not sold at all.