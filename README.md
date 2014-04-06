starterHadoopMapReduce
======================

Walking through basics of how to program MapReduce in Hadoop 2.x

Steps:

0 - Get your Apache Hadoop 2.x running on your local machine, preferably 2.3.0.
1 - Configure your environment variables; for example, for a Mac OS X host,

export MAVEN_OPTS="-Xms1024m -Xmx4096m -Djava.awt.headless=true"
export HADOOP_VERSION=2.3.0
export HADOOP_PREFIX=/opt/hadoop-${HADOOP_VERSION}
export HADOOP_HOME=${HADOOP_PREFIX}
export HADOOP_MAPRED_HOME=${HADOOP_PREFIX}
export HADOOP_COMMON_HOME=${HADOOP_PREFIX}
export HADOOP_HDFS_HOME=${HADOOP_PREFIX}
export YARN_HOME=${HADOOP_PREFIX}
export HADOOP_COMMON_LIB_NATIVE_DIR=${HADOOP_PREFIX}/lib/native
export HADOOP_CONF_DIR=${HADOOP_PREFIX}/etc/hadoop
export HADOOP_OPTS="-server -Djava.net.preferIPv4Stack=true -Djava.security.krb5.realm=OX.AC.UK -Djava.security.krb5.kdc=kdc0.ox.ac.uk:kdc1.ox.ac.uk -Djava.security.krb5.conf=/dev/null -Dlog4j.configuration=file:${HADOOP_PREFIX}/etc/hadoop/log4j.properties -Djava.library.path=${HADOOP_PREFIX}/lib"
export CLASSPATH=.:${HADOOP_PREFIX}/etc/hadoop:$(find "${HADOOP_PREFIX}" -maxdepth 1 -name '*.jar' |xargs echo  |tr ' ' ':'):$(find "${HADOOP_PREFIX}/lib" -maxdepth 1 -name '*.jar' |xargs echo  |tr ' ' ':')
export PATH=${HADOOP_PREFIX}/sbin:${HADOOP_PREFIX}/bin:${PATH}

2 - Download several books from http://www.gutenberg.org; for example,

http://www.gutenberg.org/ebooks/39064
http://www.gutenberg.org/ebooks/3207

and store those files in your HDFS, e.g., in /tmp/books by uploading using the following command:

hadoop fs -copyFromLocal /dir/book-1.txt /tmp/books
hadoop fs -copyFromLocal /dir/book-2.txt /tmp/books

3 - cd into starterHadoopMapReduce
4 - vi pom.xml
  - change /tmp/rmarano to /tmp/whatever
5 - mvn clean dependency:resolve compile package exec:exec
6 - Check the job is running here: http://localhost:18088/cluster/apps
7 - When job completed, check http://localhost:50075/browseDirectory.jsp?dir=%2Ftmp&namenodeInfoPort=50070&nnaddr=127.0.0.1:9000
  - you should see a file like this /tmp/rmarano/20140405-2258/_SUCCESS and /tmp/rmarano/20140405-2258/part-r-00000
  - you can cat the file with the following command:

hadoop fs -cat /tmp/rmarano/20140405-2258/part-r-00000

CONGRATULATIONS!  You have run your first map-reduce program on Hadoop.

/rob
