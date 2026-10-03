Aim : To write a MapReduce program to perform matrix multiplication.

Description : MapReduce is a programming model used in Hadoop to process large amounts of data in a distributed manner. It divides the processing into two main phases: Mapper and Reducer. The Mapper processes the input data and generates intermediate key-value pairs, while the Reducer combines and processes these values to produce the final output. In this task, a Java MapReduce program is developed to perform matrix multiplication. The program uses Eclipse to create the Java project, Hadoop libraries to compile the program, and HDFS to store the input and output data.

### Program

**Step-1:** Create a Java Project in Eclipse.

Open Eclipse → **New Java Project** → Name: `MatrixMultiplication` → Click on **Next** → Click on **Libraries** → **Add External JARs** → select **File System** → `usr` → `lib` → `hadoop` → select all JAR files → click on **OK**.

Click on **Libraries** → **Add External JARs** → click on **client** → select all JAR files → click on **OK** → click on **Finish**.

**Step-2:** Create the Java Classes.

Click on project `MatrixMultiplication` → `src` → right-click → **New** → **Class** and create the following classes:

- `MatrixMapper`
- `MatrixReducer`
- `MatrixDriver`

**Step-3:** Open `MatrixMapper.java` and include the following code.

~~~java
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;
import java.io.IOException;

public class MatrixMapper extends Mapper {

    public void map(Object key, Text value, Context context)
            throws IOException, InterruptedException {

        String[] tokens = value.toString().split(",");
        int i = Integer.parseInt(tokens[0]);
        int j = Integer.parseInt(tokens[1]);
        int val = Integer.parseInt(tokens[2]);

        for (int k = 0; k < 2; k++) {
            context.write(new Text(i + "," + k),
                    new IntWritable(val * j));
        }
    }
}
~~~

**Step-4:** Open `MatrixReducer.java` and include the following code.

~~~java
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Reducer;
import java.io.IOException;

public class MatrixReducer extends Reducer<Text, IntWritable, Text, IntWritable> {

    public void reduce(Text key, Iterable<IntWritable> values, Context context)
            throws IOException, InterruptedException {

        int sum = 0;

        for (IntWritable val : values) {
            sum += val.get();
        }

        context.write(key, new IntWritable(sum));
    }
}
~~~

**Step-5:** Open `MatrixDriver.java` and include the following code.

~~~java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class MatrixDriver {

    public static void main(String[] args) throws Exception {

        Configuration conf = new Configuration();

        Job job = Job.getInstance(conf, "MatrixMultiplication");

        job.setJarByClass(MatrixDriver.class);
        job.setMapperClass(MatrixMapper.class);
        job.setReducerClass(MatrixReducer.class);

        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
~~~

**Step-6:** Prepare the input data.

Input Matrix A (`matrixA.txt`):

~~~text
0,0,1
0,1,2
1,0,3
1,1,4
~~~

Input Matrix B (`matrixB.txt`):

~~~text
0,0,5
0,1,6
1,0,7
1,1,8
~~~

**Step-7:** Export the Java Project as a JAR file.

In Eclipse, right-click on `MatrixMultiplication` → **Export** → select **Java** → **JAR file** → select the `classpath` and `project` checkboxes → select the export destination → browse → `cloudera` → `Desktop` → enter the JAR file name as `MatrixMultiplication` → click on **Finish**.

**Step-8:** Upload the Input Data to HDFS.

~~~text
hdfs dfs -mkdir /matrix

hdfs dfs -put /home/cloudera/Desktop/WC/MatrixMul/matrixA.txt /matrix/

hdfs dfs -put /home/cloudera/Desktop/WC/MatrixMul/matrixB.txt /matrix/
~~~

**Step-9:** Compile and Run the MapReduce Program.

~~~text
hadoop jar /home/cloudera/Desktop/matrixmultiplication.jar MatrixDriver /matrix /output
~~~

**Step-10:** Check the Output.

~~~text
hdfs dfs -cat /output/part-r-00000
~~~

### Output
<img width="1617" height="791" alt="image" src="https://github.com/user-attachments/assets/781cb13d-ce4f-49a3-9e41-827e3e8cd770" />
