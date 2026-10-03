Aim : To develop a **Pig Latin script** to count the number of words present in a text file.  

Description : Pig Latin is a high-level data flow scripting language used with Apache Pig for processing and analyzing large datasets. It provides simple commands to load, transform, filter, group, and analyze data. Pig Latin scripts are executed by the Apache Pig framework, which converts them into execution jobs. It is commonly used for processing large amounts of structured and semi-structured data. This task demonstrates the use of Pig Latin for basic text file processing. The script reads the contents of a given text file as input. It processes the text and identifies individual words from the file. The total number of words present in the file is calculated. Finally, the word count is displayed as the output.   

### Program

**Step-1:** Create a file `Task6a.txt` on the Cloudera Desktop.

**Step-2:** Open the Cloudera terminal and type `pig -x local`.

**Step-3:** Type the following commands in the Grunt shell.

```text
inputline = LOAD '/home/cloudera/Desktop/task6a.txt' USING PigStorage('\t') AS (data:chararray);
words = FOREACH inputline GENERATE FLATTEN(TOKENIZE(data)) AS word;
filtered_words = FILTER words BY word MATCHES '\\w+';
word_groups = GROUP filtered_words BY word;
word_count = FOREACH word_groups GENERATE COUNT(filtered_words) AS count, group AS word;
ordered_word_count = ORDER word_count BY count DESC;
DUMP ordered_word_count;
```
**Step-4:** The word count output can also be stored in a file using the following
command in grunt shell.       
```text
grunt> store ordered_word_count into '/home/cloudera/Desktop/task6aoutput/';
```

**Step-5:** Open part-r-00000 file. It shows the wordcount output

### Output
<img width="1537" height="753" alt="image" src="https://github.com/user-attachments/assets/0dd8abe1-4669-44ab-b112-489150585ddc" />
