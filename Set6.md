Aim : To practice User Defined Functions (UDFs) and indexes using Hive.

Description : Hive User Defined Functions (UDFs) are used to perform custom operations on data that are not directly available through built-in Hive functions. UDFs can be written in Java and added to Hive using a JAR file. In this task, a Java UDF is created to find the maximum marks among three subjects and is used in a Hive query. The task also demonstrates how to create, view, and drop an index on a Hive table.

### Program

**Step-1:** Prepare the Data.

Create the `student` table in Hive.

~~~text
hive> create table student (name string, no int, eng float, maths float, science float) row format delimited fields terminated by ',';
~~~

Describe the table structure.

~~~text
hive> describe student;
~~~

Insert student data into the table.

~~~text
hive> insert into table student values ('sri',1,98,67,77), ('sai',2,99,56,79), ('ram',3,95,96,92), ('sita',4,91,84,87), ('anu',5,88,86,82);
~~~

Display the table contents.

~~~text
hive> select * from student;
~~~

**Step-2:** Implement the Code for UDF in Java.

Open Eclipse in Cloudera.

Create a Java project named `hiveUDFs` and create a class named `Getmaxmarks.java`.

~~~java
package hiveUDFs;

import org.apache.hadoop.hive.ql.exec.UDF;

public class Getmaxmarks extends UDF {

    public double evaluate(double math, double eng, double social) {
        double maxmark = math;

        if (eng > maxmark) {
            maxmark = eng;
        }

        if (social > maxmark) {
            maxmark = social;
        }

        return maxmark;
    }
}
~~~

**Step-3:** Package Java Class into JAR File.

Right-click on `Getmaxmarks.java` → **Export** → **JAR file** and create the JAR file as `getmaxmarks.jar`.

**Step-4:** Add JAR File into Hive.

In the Cloudera Hive shell, enter the following command.

~~~text
hive> add jar /home/cloudera/Desktop/getmaxmarks.jar;
~~~

**Step-5:** Create Temporary Function in Hive.

Create a temporary Hive function using the Java UDF.

~~~text
hive> create temporary function getmarks as 'hiveUDFs.Getmaxmarks';
~~~

**Step-6:** Use Hive UDF Using Query.

Use the created UDF to find the maximum marks among English, Mathematics, and Science.

~~~text
hive> select getmarks(eng,maths,science) from student;
~~~

**1. Creating an Index in Hive**

An index can be created on a Hive table using the `CREATE INDEX` statement.

~~~text
CREATE INDEX index_name ON TABLE table_name (column_name) AS 'COMPACT' WITH DEFERRED REBUILD;
~~~

**Example:**

~~~text
CREATE INDEX id2 ON TABLE student (maths) AS 'COMPACT' WITH DEFERRED REBUILD;
~~~

**2. Viewing Indexes**

Use the following command to view the indexes created on a table.

~~~text
SHOW INDEX ON table_name;
~~~

**Example:**

~~~text
SHOW INDEX ON student;
~~~

**3. Dropping an Index**

Use the following command to remove an index from a table.

~~~text
DROP INDEX index_name ON table_name;
~~~

**Example:**

~~~text
DROP INDEX id1 ON student;
~~~

### Output For User Defined functions
<img width="1480" height="726" alt="image" src="https://github.com/user-attachments/assets/8fced383-5308-4ad2-8654-0bb054c59bb3" />

### Output For Views
write same in boxes.
