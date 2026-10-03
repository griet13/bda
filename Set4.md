Aim : To use Apache Hive to create, alter, and drop databases, tables, and views.

Description : Apache Hive is a data warehouse tool used for managing and analyzing large datasets stored in Hadoop. It provides SQL-like commands called HiveQL to perform various operations on databases, tables, and views. In this task, different Hive commands are used to create and modify databases and tables. The task also demonstrates how to insert data into a table and remove databases and tables when they are no longer required. Finally, a view is created from an existing table and dropped using Hive commands.

### Program

**1: Create Database**

A database can be created using the `CREATE DATABASE` command. If the database already exists, Hive will display an error.

**Syntax:**

~~~text
CREATE DATABASE <database_name>;
~~~

**Example:**

~~~text
Hive> CREATE DATABASE griet;
~~~

**2: Alter Database**

The `ALTER DATABASE` command is used to change the existing properties or characteristics of a database.

**Syntax:**

~~~text
ALTER DATABASE <database_name> SET DBPROPERTIES (<property_name> = <property_value>);
~~~

**Example:**

~~~text
Hive> ALTER DATABASE griet SET DBPROPERTIES ('owner' = 'GOKARAJU', 'date' = '01-02-2025');
~~~

**3: Drop Database**

The `DROP DATABASE` command is used to remove a database from the Hive system.

**Syntax:**

~~~text
DROP DATABASE [IF EXISTS] <database_name> [RESTRICT | CASCADE];
~~~

**Example:**

~~~text
Hive> DROP DATABASE griet;
~~~

**4: Create Table**

Tables are created inside a database. First, use the required database using the `USE` command.

**Syntax:**

~~~text
USE <database_name>;
~~~

**Example:**

~~~text
Hive> USE griet;
~~~

**5: Insert Data into Table**

Hive tables provide a structure for storing data in different formats. Data can be inserted into a table using the `INSERT INTO TABLE` command.

**Syntax:**

~~~text
INSERT INTO TABLE <table_name> VALUES (<values>);
~~~

**Example:**

~~~text
Hive> INSERT INTO TABLE student_data VALUES ('anil',1,90), ('akash',2,98), ('abhi',3,99);
~~~

**6: Drop Table**

The `DROP TABLE` command is used to remove a table and its associated metadata from the Hive Metastore.

**Syntax:**

~~~text
DROP TABLE [IF EXISTS] <table_name>;
~~~

**Example:**

~~~text
Hive> DROP TABLE student_data;
~~~

**7: Create View**

A view can be created using the result of a `SELECT` statement. A view provides a virtual representation of the data from one or more tables.

**Syntax:**

~~~text
CREATE VIEW [IF NOT EXISTS] <view_name> AS SELECT ...;
~~~

**Example:**

~~~text
Hive> CREATE VIEW v1 AS SELECT * FROM student_data;
~~~

**8: Drop View**

A view can be removed from Hive using the `DROP VIEW` command.

**Syntax:**

~~~text
DROP VIEW <view_name>;
~~~

**Example:**

~~~text
Hive> DROP VIEW v1;
~~~

### Output
write the same in boxes.
