Aim : To write and practice HBase queries for handling databases.

Description : HBase is a distributed, column-oriented NoSQL database that runs on top of Hadoop. It is used to store and manage large amounts of structured and semi-structured data. HBase provides commands to create and modify tables, insert and retrieve data, delete records, and manage users and permissions. In this task, basic HBase commands, Data Definition Language (DDL) commands, Data Manipulation Language (DML) commands, and security commands are practiced.

### Program

### i. General Commands

**1:** `whoami`

The `whoami` command is used to retrieve information about the current HBase user.

~~~text
Syntax:
whoami
~~~

**2:** `status`

The `status` command provides information about the HBase cluster, including the cluster health, number of servers, and regions.

~~~text
Syntax:
status

Output:
1 active master, 3 region servers, 6 regions
~~~

**3:** `version`

The `version` command retrieves the version information of HBase.

~~~text
Syntax:
version

Output:
HBase 2.4.0
~~~

**4:** `cluster_help`

The `cluster_help` command provides information about commands related to cluster management.

~~~text
Syntax:
cluster_help

Output:
status
version
~~~

### ii. Data Definition Language in HBase

**1:** Create

The `create` command is used to create a new table in HBase.

~~~text
Syntax:
create 'table_name', 'column_family1', 'column_family2', ...

Output:
0 row(s) in 1.4860 seconds
~~~

**2:** Describe

The `describe` command provides information about a specified table, including its column families and region details.

~~~text
Syntax:
describe 'table_name'

Output:
Table employees is ENABLED
employees COLUMN FAMILIES DESCRIPTION
~~~

**3:** Alter

The `alter` command is used to modify the schema of an existing table.

~~~text
Syntax:
alter 'table_name', {NAME => 'new_column_family'}

Output:
0 row(s) in 1.4860 seconds
~~~

**4:** Exists

The `exists` command is used to check whether a table exists in HBase.

~~~text
Syntax:
exists 'table_name'

Output:
Table table_name does not exist
~~~

### iii. Data Manipulation Language in HBase

**1:** Put

The `put` command is used to insert or update data in an HBase table.

~~~text
Syntax:
put 'table_name', 'row_key', 'column_family:column_qualifier', 'value'

Output:
0 row(s) in 1.4860 seconds
~~~

**2:** Get

The `get` command is used to retrieve data from a table based on the row key.

~~~text
Syntax:
get 'table_name', 'row_key'

Output:
COLUMN CELL
personal:name, timestamp=1628272254000, value=John Doe
~~~

**3:** Scan

The `scan` command is used to retrieve multiple rows or a range of rows from a table.

~~~text
Syntax:
scan 'table_name'

Output:
ROW COLUMN+CELL
1001 column=personal:name, timestamp=1628272254000, value=Sample user
~~~

**4:** Delete

The `delete` command is used to delete data from a table based on the row key, column family, and column qualifier.

~~~text
Syntax:
delete 'table_name', 'row_key', 'column_family:column_qualifier'

Output:
0 row(s) in 1.4860 seconds
~~~

### iv. Security Commands

**1:** Create

The `create` command is used to create a new user with a specified username and password.

~~~text
Syntax:
create 'user', 'password'

Output:
0 row(s) in 1.5680 seconds
~~~

**2:** Grant

The `grant` command is used to grant permissions to a user on a specific table.

~~~text
Syntax:
grant 'user', 'permissions', 'table'

Output:
0 row(s) in 1.5680 seconds
~~~

**3:** Revoke

The `revoke` command is used to revoke permissions from a user on a specific table.

~~~text
Syntax:
revoke 'user', 'permissions', 'table'

Output:
0 row(s) in 1.5680 seconds
~~~

**4:** User Permissions

The `user_permission` command is used to list the permissions assigned to a specific user.

~~~text
Syntax:
user_permission 'user_name'

Output:
User Table, Family, Qualifier, Permission
bob  employees  :  [read]
~~~

### Output
write same in boxes.
