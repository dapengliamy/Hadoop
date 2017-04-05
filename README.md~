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
 4. View file on HDFS: hdfs dfs -cat <path to your directory on HDFS>/<file_name> • Make a new directory:
      hdfs dfs -mkdir <path your directory on HDFS>/<folder_name>
 5. Remove a file: hdfs dfs -rm <path to your directory on HDFS>/<file_name>
 6. Remove a directory:
     hdfs dfs -rm -r <path to your directory on HDFS>/<folder_name>