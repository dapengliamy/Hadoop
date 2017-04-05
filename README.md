In this small project,  I are going to implement a Hadoop program that computes the page visit counts of Wikipedia pages.

## 1.Setting Up Hadoop Environment

In this section, we are going to setup the Hadoop environment. First you need to login to the Hadoop server using your engineering account:
ssh hadoop-master.engr.oregonstate.edu

Next you need to set the JAVA HOME and HADOOP HOME variables. These variables help Linux shell to locate the java and hadoop binaries when you are using hadoop commands. Once you are logged in to the Hadoop server, open the shell startup configuration file ∼/.cshrc with an editor and add the following lines to the end of the file:

```
setenv JAVA_HOME "/usr/lib/jvm/java-1.8.0"
setenv PATH "$JAVA_HOME/bin:$PATH"
setenv CLASSPATH ".:$JAVA_HOME/jre/lib:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar"
setenv HADOOP_HOME /opt/hadoop/hadoop
setenv HADOOP_COMMON_HOME $HADOOP_HOME
setenv HADOOP_HDFS_HOME $HADOOP_HOME
setenv HADOOP_MAPRED_HOME $HADOOP_HOME
setenv HADOOP_YARN_HOME $HADOOP_HOME
setenv HADOOP_OPTS "-Djava.library.path=$HADOOP_HOME/lib/native"
setenv HADOOP_COMMON_LIB_NATIVE_DIR $HADOOP_HOME/lib/native
setenv PATH $HADOOP_HOME/sbin:$HADOOP_HOME/bin:$PATH
setenv HADOOP_CLASSPATH "${JAVA_HOME}/lib/tools.jar"
```
After this, you need to reload the startup file:
source ∼/.cshrc

## 2. Working with HDFS

You have a folder on HDFS server at /user/cs540/<your onid user name>. Note that files on HDFS can be manipulated only using the special commands that are given below. Throughout the assignment, you should just use this directory when you need to work with HDFS. You can upload files or write output of your jobs to your directory. Note that this directory is not being backed up. Following is a list of commands that you can use to interact with HDFS:

 1. View list of files and folders: hdfs dfs -ls <path>
 2. Upload a file to HDFS:
      hdfs dfs -put <file on engr account> <path to your directory on HDFS>
 3. Download a file from HDFS:
  hdfs dfs -get <path to your directory on HDFS>/<file_name>
 4. View file on HDFS: hdfs dfs -cat <path to your directory on HDFS>/<file_name> 
 5.  Make a new directory:
     hdfs dfs -mkdir <path your directory on HDFS>/<folder_name>
 5. Remove a file: hdfs dfs -rm <path to your directory on HDFS>/<file_name>
 6. Remove a directory:
     hdfs dfs -rm -r <path to your directory on HDFS>/<folder_name>

## 3. Problem Explanation
Your task is to compute the page visit counts of Wikipedia pages over a period of time. We have provided an input file input.csv that contains page titles and visit counts for each page. Each row of the file has page title, page visit count and content size information. These values are separated by space. There can be multiple rows for a single page. Following is a fragment of sample input file:


Ace_of_Swords 2 17276
Law_school 29 539143
Ace_of_Swords 3 17705

You should write a program that computes the total page visits for each page. For example, the total page visits for Ace of Swords will be 5. The output file should contain page title and the total count separated by a single space. Following is the output for the sample input:

Law_school 29
Ace_of_Swords 5

Note that the rows of the output file do not need to be in the same order as the input file.

## 4. Implementation

You are given a skeleton code PageCount.java and you need to complete the map and reduce functions in this file.

## 5. Mapper
The map function is called once for each key/value pair in the input split. The value argument of map function is of type Text and contains the text of the input file. You can call toString() on it to get a String object of the value 2. You should use value to produce the needed key-value pairs. After that you can call context.write(new key, new value) to send the key values to the reducer.

## 6. Reducer
The reduce function is called once for each key received from the Mapper. You can iterate over the values of that key to do your computations. In the end of the method you can call context.write(another key, another value) to write the results of reduce to an output file.

## 7. Compiling and Running
Once you have finished your implementation you can run the following commands to compile your code and create a jar file:

```
hadoop com.sun.tools.javac.Main PageCount.java
jar cf pc.jar PageCount*.class

Then upload the input file input.csv to your HDFS folder:

hdfs dfs -put input.csv <path to your folder>

Next you you can run the application:

hadoop jar pc.jar PageCount.java <path to your folder>/input <path to your folder>/output 

Note that the output directory should not exist before running the above command. Otherwise you will get an error. After the job is finished you can view the output file:

hdfs dfs -cat <path to your folder>/output/part-r-00000
```

Depending on the number of reducers you may get more than one output files. Use the list command mentioned in the previous section to go through different output files.

  1. You can put your code in a directory under your engineering account’s home folder. This way, after logging in to the Hadoop server, you can access your code in your engineering home folder and you can edit and compile the code there. However, the input file should be uploaded to the HDFS using the given commands.
  2. After running your job you can view its status using a web interface. To do this, login to Hadoop server. If you are a mac user, you need to add −X to ssh command to enable X11 services. After you logged in, type firefox in the terminal. This should open a firefox windonw. Then go to “http://hadoop-master.engr.oregonstate.edu:8088/” in the firefox. You should be able to see information on your hadoop jobs.
