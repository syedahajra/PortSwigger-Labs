**Lab: SQL injection UNION attack, finding a column containing text**

This lab contained a SQL injection vulnerability in the product category filter. The goal was to determine which column in the query accepts string data by injecting a random string value provided by the lab.

I intercepted the category filter request using *Burp Suite*. 
Then I figured out number of columns was *3* by changing payload to *'+UNION+SELECT+NULL,NULL,NULL--*.

I replaced each NULL value with string 'CPuMuw' (provided by lab), testing each column.
'+UNION+SELECT+'CPuMuw',NULL,NULL--  
'+UNION+SELECT+NULL,'CPuMuw',NULL--  
'+UNION+SELECT+NULL,NULL,'CPuMuw'--  

This request *'+UNION+SELECT+NULL,'CPuMuw',NULL--* did not cause error, confirming that the second column supports string data.

