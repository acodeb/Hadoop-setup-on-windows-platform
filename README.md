# Hadoop-setup-on-windows-platform

Prerequisites for installing hadoop on windows

1. Install Cygwin64 on you windows machine

2. Make sure you have java 1.7 installed in your machine and added in environment variables


Steps to setup hadoop 2.5.1 on Windows Platform

1. Download hadoop 2.5.1 tar file from here.

2. uzip thie file.

3. Go to "etc\hadoop" directory inside hadoop folder

4. Replace core-site.xml with following
	
        <configuration>
                <property>
                        <name>fs.defaultFS</name>
                        <value>hdfs://localhost:9000</value>
                </property>
        <configuration>

5. Replace hdfs-site.xml with following

        <configuration>
	        <property>
                        <name>dfs.replication</name>
                        <value>1</value>
                </property>
                <property>
                        <name>dfs.namenode.name.dir</name>
                        <value>file:/hadoop/data/dfs/namenode</value>
                </property>
                <property>
                        <name>dfs.datanode.data.dir</name>
                        <value>file:/hadoop/data/dfs/datanode</value>
                </property>
        </configuration>

6. Replace yarn-site.xml with following

        <configuration>
                <property>
                        <name>yarn.nodemanager.aux-services</name>
                        <value>mapreduce_shuffle</value>
                </property>
                <property>
                        <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
                        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
                </property>
                <property>
                        <name>yarn.application.classpath</name>
                        <value>
                        %HADOOP_HOME%\etc\hadoop,
                        %HADOOP_HOME%\share\hadoop\common\*,
                        %HADOOP_HOME%\share\hadoop\common\lib\*,
                        %HADOOP_HOME%\share\hadoop\mapreduce\*,
                        %HADOOP_HOME%\share\hadoop\mapreduce\lib\*,
                        %HADOOP_HOME%\share\hadoop\hdfs\*,
                        %HADOOP_HOME%\share\hadoop\hdfs\lib\*,          
                        %HADOOP_HOME%\share\hadoop\yarn\*,
                        %HADOOP_HOME%\share\hadoop\yarn\lib\*
                        </value>
                </property>
        </configuration>

7. Add following the the Environment variables

        Platform=x64
        HADOOP_HOME = <Location of you hadoop folder> //In my case it is "C:\hadoop"
        Path =C:\hadoop\bin;C:\cygwin64\bin;%Path%

8. Open cmd prompt and go to bin folder inside hadoop folder and run following command to format namenode

        hadoop namenode -format

9. Open cmd prompt and go to sbin folder inside hadoop folder and run following command to start hadoop

        start-dfs.cmd
It will start namenode and datanode



