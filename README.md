# R-Oracle-Data-Integration
R-ODBC-Oracle-Examples: Code examples for working with Oracle databases in R using RODBC package
To connect to a remote Oracle database from R, you can use the RODBC package. Here are the steps to connect to a remote Oracle database using RODBC:

=========================================================
Loading ODBC to R Environment
=========================================================

Install the RODBC package:

install.packages("RODBC")

Load the RODBC package into your R session:

library(RODBC)

Set up a connection to the remote Oracle database using the odbcConnect function. Here's an example:

con <- odbcConnect("your_DSN_name", uid = "your_username", pwd = "your_password")

Here, replace "your_DSN_name", "your_username", and "your_password" with the actual credentials for the remote Oracle database. Note that you may need to set up a DSN on your machine to connect to the remote database. You can create a DSN by going to Control Panel > Administrative Tools > ODBC Data Sources (64-bit) > System DSN > Add, and following the prompts.

Execute SQL queries on the remote Oracle database using the sqlQuery function. Here's an example:

=========================================================
Select Query
=========================================================

result <- sqlQuery(con, "SELECT * FROM your_table_name")
Here, replace "your_table_name" with the actual name of the table you want to query.

After you have finished working with the remote Oracle database, close the connection using the odbcClose function:

odbcClose(con)

=========================================================
Adding ODBC Connection to Server
=========================================================

These are the basic steps to connect to a remote Oracle database from R using RODBC. You may need to adjust the connection details depending on your specific setup.

When you create a DSN (Data Source Name) using the ODBC Data Source Administrator, you'll need to provide the following information to connect to a remote Oracle database:

Name: Enter a name for the DSN that you can use to identify it later.

Description: Enter a brief description of the DSN.

TNS Service Name: This is the name of the Oracle service that you want to connect to. You can find this information in your tnsnames.ora file, which is typically located in your ORACLE_HOME/network/admin directory. The TNS Service Name is typically a string like "ORCL" or "XE".

User ID: Enter the username that you use to connect to the Oracle database.

Password: Enter the password for the username.

Host Name: Enter the hostname or IP address of the server where the Oracle database is located.

Port: Enter the port number that the Oracle database is listening on. The default port number for Oracle databases is 1521.

Driver: Select the appropriate Oracle ODBC driver that you have installed on your machine.

Optionally, you can also set up advanced options, such as the connection timeout, fetch buffer size, and others.

Once you have provided this information, you can test the connection to ensure that it is working correctly. When you're finished, you can save the DSN and use it to connect to the Oracle database using RODBC or other ODBC-based tools.

=========================================================
Display Results
=========================================================

result <- sqlQuery(con, "SELECT * FROM my_table")
print(result)

=========================================================
Insert New Record 
=========================================================

# Establish connection
con <- odbcConnect("your_DSN_name", uid = "your_username", pwd = "your_password")

# Create a data frame with the data to insert
my_data <- data.frame(id = 1:10, name = LETTERS[1:10], value = rnorm(10))

# Insert the data into a new table
sqlSave(con, my_data, tablename = "my_table", rownames = FALSE, append = FALSE)

# Close the connection
odbcClose(con)

=========================================================
Update Exsisiting Records
=========================================================

# Establish connection
con <- odbcConnect("your_DSN_name", uid = "your_username", pwd = "your_password")

# Update the value column for rows where id is even
sqlQuery(con, "UPDATE my_table SET value = value * 2 WHERE id % 2 = 0")

# Close the connection
odbcClose(con)

This code updates the value column in the my_table table for rows where the id column is even, doubling the value of the value column for those rows. Note that the sqlQuery function is used to execute the SQL statement directly on the Oracle database. You can use any valid SQL statement to update data in the database.

Remember to always be careful when updating data in a production database, as updates can have unintended consequences. It's always a good idea to test updates in a development environment first.


=========================================================
Delete Exsisiting Records
=========================================================

# Establish connection
con <- odbcConnect("your_DSN_name", uid = "your_username", pwd = "your_password")

# Delete rows where id is greater than 5
sqlQuery(con, "DELETE FROM my_table WHERE id > 5")

# Close the connection
odbcClose(con)

This code deletes all rows from the my_table table where the id column is greater than 5. Note that the sqlQuery function is used to execute the SQL statement directly on the Oracle database. You can use any valid SQL statement to delete data from the database.

Remember to always be careful when deleting data from a production database, as deletions can have unintended consequences. It's always a good idea to test deletions in a development environment first.

