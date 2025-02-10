**Lab: SQL Injection – Determining the Number of Columns**

This lab contained a SQL injection vulnerability in the product category filter. My goal was to determine the number of columns returned by the SQL query using a UNION-based SQL injection attack.

I used Burp Suite Proxy to intercept the request that sets the product category filter.
Found the vulnerable parameter: category.

Then I added *'+UNION+SELECT+NULL* to find number of columns.

Modified the category parameter in the request:
https://web-security-academy.net/filter?category='+UNION+SELECT+NULL--

This caused an error, indicating that the number of selected columns was incorrect.

I incremented the Number of NULL Values to the payload until no errors appeared and the  application returned additional content in the response, confirming the correct number of columns.
*'+UNION+SELECT+NULL,NULL,NULL--*

https://web-security-academy.net/filter?category='+UNION+SELECT+NULL,NULL,NULL--

Lessons Learned
SQL UNION attacks require determining the correct number of columns.
Incrementally adding NULL values helps identify the exact column count.
This technique is useful for extracting sensitive data in further SQL injection attacks.
