Aim : To write a Pig Latin script to sort, group, join, project, and filter the data.

Description : Apache Pig is a high-level data flow platform used to process and analyze large datasets. Pig Latin provides simple operators to load, transform, filter, group, join, project, and sort data. In this task, different Pig Latin operators are used to perform common data processing operations. The `LOAD` operator reads data from the file system, `FOREACH` projects required fields, `FILTER` selects records based on conditions, `JOIN` combines data from multiple relations, `ORDER BY` sorts the data, and `GROUP` groups records based on a common field.

### Program

**1:** LOAD

The `LOAD` operator is used to load data from the file system or HDFS into a Pig relation. Open the Cloudera terminal and type `pig -x local`.

~~~text
grunt> loading1 = load '/home/cloudera/task5/first.txt' using PigStorage(',') as (user:chararray,url:chararray,id:int);
grunt> dump loading1;
~~~

**2:** FOREACH

The `FOREACH` operator is used to perform transformations on the columns of a relation. It can be used to add or remove fields from a relation.

~~~text
grunt> for_each = foreach loading1 generate url,id;
grunt> dump for_each;
~~~

**3:** FILTER

The `FILTER` operator is used to select tuples from a relation based on a specified condition.

~~~text
grunt> filter_command = filter loading1 by id > 500;
grunt> dump filter_command;
~~~

**4:** JOIN

The `JOIN` operator is used to perform an inner join of two or more relations based on common field values. Inner joins ignore null keys.

First, load the second file.

~~~text
grunt> loading2 = load '/home/cloudera/task5/second.txt' using PigStorage(',') as (url:chararray,id:int);
grunt> dump loading2;
~~~

Perform the join using the common `url` field.

~~~text
grunt> join_command = join loading1 by url, loading2 by url;
grunt> dump join_command;
~~~

**5:** ORDER BY

The `ORDER BY` operator is used to sort a relation based on one or more fields. The data can be sorted in ascending or descending order using `ASC` and `DESC`.

~~~text
grunt> loading3 = order loading2 by url asc;
grunt> dump loading3;
~~~

The contents of `loading2` are sorted in ascending order of `url`.

**6:** GROUP

The `GROUP` operator is used to group data from one or more relations. It collects records having the same key.

**Syntax:**

~~~text
grunt> Group_data = GROUP Relation_name BY variable;
~~~

**Example:**

~~~text
grunt> a = group loading1 by url;
grunt> dump a;
~~~

### Output
write same in boxes.
