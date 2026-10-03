Aim : To develop a Pig Latin script to find the maximum temperature across all the years using a weather dataset.

Description : Apache Pig is a high-level data flow platform used to process and analyze large datasets. Pig Latin provides operators for loading, transforming, grouping, and analyzing data. In this task, a weather dataset containing dates and temperatures is loaded into Pig. The year is extracted from each date, the records are grouped based on the year, and the maximum temperature for each year is calculated using the `MAX` function. The final result displays the maximum temperature recorded for each year.

### Program

**Step-1:** Create a file `temp.txt` on the Cloudera Desktop. Enter the date and temperature separated by a tab.

~~~text
Date    Temperature
01/01/2020    35
02/01/2020    38
03/01/2021    40
04/01/2021    42
05/01/2022    39
06/01/2022    45
~~~

**Step-2:** Open the Cloudera terminal and type `pig -x local`.

~~~text
$ pig -x local
~~~

**Step-3:** Type the following script in the Grunt shell.

~~~text
raw_data = LOAD '/home/cloudera/Desktop/temp.txt' USING PigStorage('\t') AS (date:chararray, temperature:double);

data_with_year = FOREACH raw_data GENERATE SUBSTRING(date,5,9) AS year, temperature;

grouped_data = GROUP data_with_year BY year;

max_temp_year = FOREACH grouped_data GENERATE group AS year, MAX(data_with_year.temperature) AS max_temperature;

DUMP max_temp_year;
~~~

### Output
<img width="1476" height="720" alt="image" src="https://github.com/user-attachments/assets/8b57c94f-2f1e-4b90-9434-3a8ff1ede47d" />
