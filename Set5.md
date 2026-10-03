Aim : To practice and understand basic HDFS commands in a Hadoop environment.

Description : Hadoop Distributed File System (HDFS) is the storage system used by Hadoop to store and manage large amounts of data across multiple machines. HDFS provides commands to create directories, list files, create empty files, copy and move files, and display file contents. In this task, basic HDFS commands are practiced to understand how files and directories are managed in the Hadoop environment. These commands help users perform common file management operations between the local file system and HDFS.

### Program

**1. List Files and Directories**

The `ls` command is used to list files and directories in HDFS. The `lsr` command can be used for recursive listing.

**Syntax:**

~~~text
$ hdfs dfs -ls <path>
~~~

**Example:**

~~~text
$ hdfs dfs -ls /
~~~

**2. Create a Directory**

The `mkdir` command is used to create a new directory in HDFS.

**Syntax:**

~~~text
$ hdfs dfs -mkdir <directory_path>
~~~

**Example:**

~~~text
$ hdfs dfs -mkdir /Newdirectory
~~~

**3. Create an Empty File**

The `touchz` command is used to create an empty file in HDFS.

**Syntax:**

~~~text
$ hdfs dfs -touchz <file_path>
~~~

**Example:**

~~~text
$ hdfs dfs -touchz /Newdirectory/myfile.txt
~~~

**4. Copy Files from Local File System to HDFS**

The `copyFromLocal` or `put` command is used to copy files or folders from the local file system to HDFS.

**Syntax:**

~~~text
$ hdfs dfs -copyFromLocal <local_file_path> <destination_path>
~~~

**Example:**

~~~text
$ hdfs dfs -copyFromLocal /home/cloudera/myfile.txt /Newdirectory/
~~~

**5. Display File Contents**

The `cat` command is used to display the contents of a file stored in HDFS.

**Syntax:**

~~~text
$ hdfs dfs -cat <file_path>
~~~

**Example:**

~~~text
$ hdfs dfs -cat /Newdirectory/myfile.txt
~~~

**6. Copy Files from HDFS to Local File System**

The `copyToLocal` or `get` command is used to copy files or folders from HDFS to the local file system.

**Syntax:**

~~~text
$ hdfs dfs -copyToLocal <source_path> <local_destination>
~~~

**Example:**

~~~text
$ hdfs dfs -copyToLocal /Newdirectory/myfile.txt /home/cloudera/
~~~

**7. Move Files from Local File System to HDFS**

The `moveFromLocal` command is used to move a file from the local file system to HDFS.

**Syntax:**

~~~text
$ hdfs dfs -moveFromLocal <local_source> <hdfs_destination>
~~~

**Example:**

~~~text
$ hdfs dfs -moveFromLocal /home/cloudera/myfile.txt /Newdirectory/
~~~

**8. Move Files within HDFS**

The `mv` command is used to move or rename files and directories within HDFS.

**Syntax:**

~~~text
$ hdfs dfs -mv <source_path> <destination_path>
~~~

**Example:**

~~~text
$ hdfs dfs -mv /Newdirectory/myfile.txt /Newdirectory/backup/
~~~

### Output
write same in boxes.
