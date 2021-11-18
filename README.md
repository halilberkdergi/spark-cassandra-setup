# spark-cassandra-setup
Quick Spark-Cassandra Setup for Ubuntu

# 1) Spark Setup

- Check java version.
```` 
java --version
````
```` 
sudo apt-get install openjdk-11-jre
````
```` 
sudo apt-get install openjdk-11-jdk
````
- Download Apache Spark 3.1.2 from :  [Here](https://www.apache.org/dyn/closer.lua/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz).
  - Extract and move to HOME as 'spark'.
- Edit Bashrc.
```` 
cd ~/
````
```` 
nano .\bashrc
````
Write at the bottom.
```` 
export SPARK_HOME=/home/$USER/spark
export PATH=$PATH:$SPARK_HOME/bin
````
Press Ctrl + S and then Ctrl + X .
```` 
source .\bashrc
````

-Install pip3
```` 
sudo apt install python3-pip
````
```` 
pip3 --version
````
- Install pyspark
```` 
sudo pip3 install pyspark
````
- Open spark-hell
```` 
spark-shell
````
- Then exit with 'Ctrl+D'
# 2) Cassandra Setup
- Install Java 8
```` 
sudo apt-get install openjdk-8-jdk -y
````
```` 
sudo update-alternatives --config java
````
press : 2
- Download Apache Cassandra 4.0.1 from :  [Here](https://www.apache.org/dyn/closer.lua/cassandra/4.0.1/apache-cassandra-4.0.1-bin.tar.gz).
  - Extract and move to HOME as 'cassandra'.
- Edit Bashrc.
```` 
cd ~/
````
```` 
nano .\bashrc
````
Write at the bottom.
```` 
export CASSANDRA_HOME=/home/$USER/cassandra
export PATH=$PATH:$CASSANDRA_HOME/bin
````
Press Ctrl + S and then Ctrl + X .
```` 
source .\bashrc
````
run cassandra
```` 
cassandra
````
show status
```` 
nodetool status
````
- Close cassandra
```` 
nodetool stopdaemon
````

# 3 Jupyter Notebook + Pyspylon_Kernel Setup
```` 
sudo apt-get install ipython3
````
```` 
pip3 install jupyter
````
```` 
pip3 install jupyter
````
- Edit Bashrc.
```` 
cd ~/
````
```` 
nano .\bashrc
````
Write at the bottom.
```` 
export PYSPARK_PYTHON=/usr/bin/python3.8
export PYSPARK_DRIVER_PYTHON="jupyter"
export PYSPARK_DRIVER_PYTHON_OPTS="notebook"
````
Press Ctrl + S and then Ctrl + X .
```` 
source .\bashrc
````
- Install Pysplon Kernel
```` 
pip3 install spylon-kernel
````
```` 
python3 -m spylon_kernel install --user
````
- Look kernel list
```` 
jupyter kernelspec list
````
- Start jupyter notebook 
```` 
jupyter notebook
````
- open new spylon_kernel notebook (by the way dont forget to run cassandra)
```ruby
%%init_spark
launcher.packages = ["com.datastax.spark:spark-cassandra-connector_2.12:3.1.0"]
launcher.conf.set("spark.sql.extensions", "com.datastax.spark.connector.CassandraSparkExtensions")
launcher.num_executors = 4
launcher.executor_cores = 2
launcher.driver_memory = '4g'
```
```ruby
spark
```
```ruby
import com.datastax.spark.connector._
```
```ruby
val cassandraHost = "127.0.0.1" // change the cassandra IP
```
```ruby
// Tell Spark the address of one Cassandra node:
spark.conf.set("spark.cassandra.connection.host", cassandraHost)
```

### AND FINISHHHHHH.....
