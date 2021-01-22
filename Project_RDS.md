access data from rds to pyspark and vice versa


##how to load data from rds to pyspark

Step1:Download the jar_files.zip
step2:unzip the file
step3:sudo cp mysql-connector-java-5.1.49.jar /lib/spark/jars/
step4:go to pyspark
step5:establish the connection

from  pyspark.sql import SparkSession
from pyspark.sql import SQLContext
spark = SparkSession.builder.config(conf=SparkConf()).getOrCreate()
sqlContext = SQLContext(spark)
hostname='shnakidb.cqb3dula51ug.us-east-1.rds.amazonaws.com'
jdbcPort=3306
dbname='test'
username='admin'
password='admin123'
jdbc_url = "jdbc:mysql://{0}:{1}/{2}".format(hostname, jdbcPort, dbname)
connectionProperties = {
   "user" : username,
   "password" : password
}

step6:read the csv file 
df=spark.read.jdbc(url=jdbc_url,table='project',properties= connectionProperties)

step7:show the records
df.show()






##how to write data from spark to rds

Step1:Create the table in mysql(rds) 
create database test;

use test;
create table project( 
ID varchar(20) Primary key,
Source varchar(40),
TMC int,
Severity int,
Start_Time TIMESTAMP,
End_Time TIMESTAMP,
Start_Lat  double,
Start_Lng double,
Distance double,
Street varchar(200));

step2:Establish the connection
from  pyspark.sql import SparkSession
from pyspark.sql import SQLContext
spark = SparkSession.builder.config(conf=SparkConf()).getOrCreate()
sqlContext = SQLContext(spark)
hostname='shnakidb.cqb3dula51ug.us-east-1.rds.amazonaws.com'
jdbcPort=3306
dbname='test'
username='admin'
password='admin123'
jdbc_url = "jdbc:mysql://{0}:{1}/{2}".format(hostname, jdbcPort, dbname)
connectionProperties = {
   "user" : username,
   "password" : password
 }

step3:Read the file from s3 bucket
df=spark.read.csv("s3://sparktords/Us_accident_RDS.csv")
step4:write the csv file into rds
df.write.jdbc(url=jdbc_url,table='demo',mode='overwrite',properties=connectionProperties)
