Aim : To ingest structured and unstructured data using Apache Flume.

Description : Apache Flume is a distributed data ingestion tool used to collect, transport, and transfer large amounts of data from different sources to a destination. It follows a simple architecture consisting of a source, channel, and sink. The source collects data, the channel temporarily stores the data, and the sink delivers the data to the required destination. In this task, structured data in CSV format and unstructured data in text format are created and ingested using Flume. The data is read from a local directory and stored in another local directory using a Flume agent.

### Program

**Step-1:** Open the Cloudera terminal and check the Flume version.

~~~text
$ flume-ng version
~~~

**Step-2:** Create folders in Cloudera with the names `flume_data` and `flume_output`.

~~~text
$ mkdir /home/cloudera/flume_data
$ mkdir /home/cloudera/flume_output
~~~

**Step-3:** Create a file `employees.csv` containing structured data in the `flume_data` folder.

~~~text
id,name,age,salary
1,s,30,4000
2,b,40,6000
3,bc,50,9000
~~~

**Step-4:** Create a file `sample1.txt` containing unstructured data in the `flume_data` folder.

~~~text
Hello how are you
Spark is powerful
Scala is fun
Flume is used to ingest data
It uses source, channel and sink
~~~

**Step-5:** Open the Cloudera terminal and edit the Flume configuration file `flume-hdfs.conf`.

~~~text
$ sudo nano /etc/flume-ng/conf/flume-hdfs.conf
~~~

Enter the following configuration:

~~~text
agent.sources = src
agent.channels = ch
agent.sinks = sk

agent.sources.src.type = spooldir
agent.sources.src.spoolDir = /home/cloudera/flume_data
agent.sources.src.fileHeader = true

agent.channels.ch.type = memory
agent.channels.ch.capacity = 1000
agent.channels.ch.transactionCapacity = 100

agent.sinks.sk.type = file_roll
agent.sinks.sk.sink.directory = /home/cloudera/flume_output
agent.sinks.sk.sink.rollInterval = 60

agent.sources.src.channels = ch
agent.sinks.sk.channel = ch
~~~

**Step-6:** Run the Flume agent using the configuration file.

~~~text
$ flume-ng agent --conf /etc/flume-ng/conf --conf-file /etc/flume-ng/conf/flume-hdfs.conf --name agent -Dflume.root.logger=INFO,console
~~~

**Step-7:** Check the `flume_data` directory. The processed files will be marked as `COMPLETED`.

**Step-8:** Check the files created in the `flume_output` directory.

~~~text
$ ls /home/cloudera/flume_output
~~~

**Step-9:** Open the first output file. It displays the contents of the `employees.csv` file.

**Step-10:** Open the second output file. It displays the contents of the `sample1.txt` file.

### Output
<img width="1348" height="657" alt="image" src="https://github.com/user-attachments/assets/38cffb9e-4310-4282-80d2-26d15ba268ea" />
