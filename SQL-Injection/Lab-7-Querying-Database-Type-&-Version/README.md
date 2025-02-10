**Lab: SQL Injection UNION Attack - Querying Database Type and Version**

This lab contained a SQL injection vulnerability in the product category filter. The goal was to use a UNION attack to retrieve the database version string.

I used Burp Suite to intercept and modify the request that sets the product category filter.

I then identified how many columns were returned by the SQL query and used the following payload in the category parameter to confirm two columns contained text:
**'+UNION+SELECT+'abc','def'#**

Then to retrieve the database version and type I used the following payload:
**'+UNION+SELECT+@@version,+NULL#**

Successfully retrieved and confirmed the database version **8.0.39-0ubuntu0.20.04.1** from the application's response.
That confirms the database is **MySQL 8.0.39 running on Ubuntu 20.04.1**
