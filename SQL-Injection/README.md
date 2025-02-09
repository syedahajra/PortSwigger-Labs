**Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data**

This lab contains a SQL injection vulnerability in the product category filter. When the user selects a category, the application carries out a SQL query like the following:

SELECT * FROM products WHERE category = 'Gifts' AND released = 1

To solve the lab, I perform a SQL injection attack that causes the application to display one or more unreleased products.

I change the parameters being passed to *category* by adding ' OR 1=1-- in the end: 
https://web-security-academy.net/filter?category=Corporate+gifts%27+OR+1=1--

This payload effectively altered the SQL query, making the condition always true (1=1), thereby displaying all products, including unreleased ones.

Lessons Learned
SQL injection can be exploited by manipulating query parameters.
Using ' OR 1=1-- allows an attacker to bypass filters and access hidden data.
Proper input validation and parameterized queries are essential for security.
