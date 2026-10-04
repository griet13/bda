Aim : To create User Defined Functions (UDF/Eval functions) in Pig to handle and process unwanted or invalid data during data processing.

Description : Pig User Defined Functions (UDFs) allow users to create custom functions for processing data in Apache Pig. They are useful when the built-in Pig functions are not sufficient for a particular task. In this task, a Java-based UDF is created using the `EvalFunc` class. The UDF takes a string as input and converts it into uppercase. The function is then compiled into a JAR file and registered in Apache Pig. Finally, the UDF is applied to input data using a Pig script and the processed output is displayed.

### Program

**Step-1:** Open Eclipse → File → New → Java Project and name it `PigUDFProject`.

Right-click the project → **Build Path → Configure Build Path**.

Go to **Libraries → Add External JARs** and add the following Pig JARs from Cloudera:

- `pig.jar`
- `hadoop-common.jar`
- `hadoop-mapreduce-client-core.jar`
- `commons-logging.jar`

**Step-2:** Create a new Java class.

Right-click on `src` → **New → Class** and name it `ToUpperCase.java`.

Paste the following code:

```java
import org.apache.pig.EvalFunc;
import org.apache.pig.data.Tuple;
import java.io.IOException;

public class ToUpperCase extends EvalFunc<String> {

    @Override
    public String exec(Tuple input) throws IOException {

        if (input == null || input.size() == 0 || input.get(0) == null) {
            return null;
        }

        try {
            String str = (String) input.get(0);
            return str.toUpperCase();
        } catch (Exception e) {
            throw new IOException("Error processing input", e);
        }
    }
}
```
**Step-3:** Compile and export the JAR.  
            Right-click on the PigUDFProject → Export → JAR File → Click Next.  
            
**Step-4:** Run the UDF in Apache Pig  

**a)** Open the Terminal in the Cloudera VM and navigate to the directory where the JAR file is stored.

~~~text
$ cd /home/cloudera/
~~~

**b)** Start Pig in local mode.

~~~text
$ pig -x local
~~~

**c)** Register the JAR in the Pig Grunt shell.

~~~text
grunt> REGISTER 'ToUpperCase.jar';
~~~

**d)** Define the UDF.

~~~text
grunt> DEFINE ToUpperCase ToUpperCase();
~~~

**e)** Load the data and apply the UDF.

Create a text file named `inputpig.txt` in `/home/cloudera/` with the following content:

~~~text
gokaraju rangaraju institute of engineering and technology
big data cloudera
big data analytics lab
~~~

Run the following Pig commands in the Grunt shell:

~~~text
grunt> data = LOAD 'inputpig.txt' AS name;
grunt> upper_data = FOREACH data GENERATE ToUpperCase(name);
grunt> DUMP upper_data;
~~~

### Output
<img width="1622" height="796" alt="image" src="https://github.com/user-attachments/assets/c7af6b60-aa2a-407e-af20-dbc3f471aebf" />
