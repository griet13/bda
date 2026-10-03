Aim : To ingest structured data from a MySQL database into Hadoop using Apache Sqoop.

Description : Apache Sqoop is a tool used to transfer structured data between relational databases and Hadoop. It allows data from databases such as MySQL to be imported into HDFS for further processing and analysis. In this task, a MySQL database is accessed and one of its tables is selected for importing. Apache Sqoop is then used to transfer the selected table from MySQL into HDFS. Finally, the imported data is verified by listing and displaying the files stored in the Hadoop directory.

### Program

**Step-1:** Open the MySQL terminal using the following command. The username is `root` and the password is `cloudera`.

~~~text
$ mysql -u root -p
~~~

**Step-2:** List the databases available in MySQL.

~~~text
mysql> SHOW DATABASES;
~~~

**Step-3:** Select any one database.

~~~text
mysql> USE retail_db;
~~~

**Step-4:** List the tables available in the selected database.

~~~text
mysql> SHOW TABLES;
~~~

**Step-5:** Check the MySQL port.

~~~text
mysql> SHOW VARIABLES LIKE 'port';
~~~

**Step-6:** Open a new terminal and check the hostname.

~~~text
$ hostname
~~~

**Step-7:** Import the `products` table from MySQL into Hadoop using Apache Sqoop.

~~~text
$ sqoop import --connect jdbc:mysql://quickstart.cloudera:3306/retail_db --username root --password cloudera --m 1 --table products --target-dir /user/landing/sqlImport
~~~

**Step-8:** View the records from the `products` table in MySQL.

~~~text
mysql> SELECT * FROM products;
~~~

**Step-9:** Open a new terminal and list the files in the HDFS landing directory.

~~~text
$ hadoop fs -ls /user/landing/
~~~

**Step-10:** Display the imported data from HDFS.

~~~text
$ hadoop fs -cat /user/landing/sqlImport/part-m-*
~~~

### Output
<img width="997" height="746" alt="image" src="https://github.com/user-attachments/assets/e9144a6b-ba1a-44ad-b297-bf13fe0492b1" />
