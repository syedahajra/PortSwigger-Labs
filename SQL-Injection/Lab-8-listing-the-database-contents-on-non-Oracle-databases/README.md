**SQL Injection Attack: Listing the Database Contents on Non-Oracle Databases**

This lab contained an SQL injection vulnerability in the product category filter. The application returns results from the query, allowing the use of a UNION-based SQL injection attack to extract data from other tables. The database contains a table that holds usernames and passwords.

**Step 1: Determine the Number of Columns**

I used Burp Suite to intercept and modify the request setting the product category filter. I identified the number of columns by injecting:

'+UNION+SELECT+'abc','def'--

Ensured the number of columns matched the database structure.

**Step 2: Extract Table Names**

Retrieved the table names using the following SQL injection payload:

'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--

At this point, I went through a phase of trial and error to find the right table that would provide the necessary information. First, I attempted querying the UDT_privileges table, but it did not contain the relevant data. Then, I explored the administrable_role_authorizations table, PG_roles table, and pg_users table expecting it to provide admin-related privileges, but it was not helpful.

I noticed there were pages listing PG_user and PG_roles, which seemed relevant, but they did not lead directly to the required credentials. Finally, after further experimentation, I discovered the correct table: users_YPDDYM. This was the breakthrough that led me to extract the needed information.

**Step 3: Extract Column Names**

Once the correct user table was identified (users_YPDDYM), I retrieved column names with:

'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_YPDDYM'--

Identified the columns containing usernames and passwords.

**Step 4: Retrieve User Credentials**

Extracted usernames and passwords using:

'+UNION+SELECT+username_fenyys,+password_xsfukb+FROM+users_ypddym--

Located the administrator's credentials.

**Step 5: Log In as Administrator**

Used the extracted admin credentials to log into the application and complete the lab.
