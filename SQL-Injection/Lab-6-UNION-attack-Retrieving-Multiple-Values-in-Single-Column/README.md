**Lab: SQL Injection UNION Attack - Retrieving Mutiple Values in Single Column**

This lab contains a SQL injection vulnerability in the product category filter. The goal is to use a UNION attack to retrieve all usernames and passwords from the database in single column and log in as the administrator.

I used Burp Suite to intercept the request that sets the product category filter.

Changed the payload to identify number of columns and if their data type is string. 
'+UNION+SELECT+NULL,'def'--

The page loads without errors and displays "def", it confirms that the query returns two columns, but only one of them contains text.

Once the number of columns is known, use the following payload to extract usernames and passwords from the users table:
**'+UNION+SELECT+NULL,username||'~'||password+FROM+users--**

The application's response contained the extracted usernames and passwords concatenated with ~, including administrator's credentials.

I then used the extracted credentials to log in as the administrator.
