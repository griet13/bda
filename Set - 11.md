Aim : To develop a program using the Spark framework for processing large datasets.

Description : Apache Spark is a fast and distributed data processing framework used to process large amounts of data efficiently. It supports operations on structured and unstructured data and provides APIs for languages such as Scala, Java, Python, and R. Spark uses Resilient Distributed Datasets (RDDs) to store and process data across multiple machines. In this task, basic Spark operations are performed using Scala. The programs demonstrate mathematical operations, file creation, reading data from a file, and counting the occurrences of words.

### Program

**Example-1:** To print the square of the given numbers.

~~~text
val data = Seq(1, 2, 3, 4, 5)
val rdd = sc.parallelize(data)
rdd.map(x => x * x).collect().foreach(println)
~~~

To exit the Spark shell, press:

~~~text
:quit
~~~

**Example-2:** To create a new file `sample.txt`.

~~~scala
import java.io._

val writer = new PrintWriter(new File("/home/cloudera/sample.txt"))

writer.write("Hello Spark\nSpark is powerful\nScala is fun\nBig data processing is amazing\nHello world")

writer.close()
~~~

**Example-3:** To print the first 5 lines in the file `sample.txt`.

~~~scala
import org.apache.spark.{SparkConf, SparkContext}

val conf = new SparkConf().setAppName("TextFileExample").setMaster("local")
val sc = new SparkContext(conf)

val rdd = sc.textFile("file:///home/cloudera/sample.txt")

rdd.take(5).foreach(println)

sc.stop()
~~~

**Example-4:** To count the number of words in the file `sample.txt`.

~~~scala
val rdd = sc.textFile("file:///home/cloudera/sample.txt")

val wordCounts = rdd
    .flatMap(line => line.split(" "))
    .map(word => (word, 1))
    .reduceByKey(_ + _)

wordCounts.collect().foreach(println)
~~~

### Output
<img width="1405" height="797" alt="image" src="https://github.com/user-attachments/assets/154bd9a1-3743-4c8e-9c43-a6bbb9691f9c" />

