**PortSwigger SQL Injection Lab: Bypassing Login Authentication**

This lab contained a SQL injection vulnerability in the login function. The objective was to log in as the administrator user by exploiting the SQL injection flaw in the username field.

I exploited the vulnerability by entering **administrator'--** in the username field. 

The application processed the following SQL query:
SELECT * FROM users WHERE username = 'administrator'--' AND password = '<user_input>'

Since -- comments out the rest of the query, the password check was bypassed, granting access as the administrator to me.

Lessons Learned
SQL injection can be used to bypass authentication mechanisms.
Single quotes (') and comments (--) can manipulate SQL logic.
Secure coding practices, such as using prepared statements, are necessary to prevent authentication bypass vulnerabilities.
