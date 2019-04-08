# Hive Examples


## Import from MySQL
<pre>ssqoop import --connect jdbc:mysql://localhost/retail_db --username root -P  --table categories  --target-dir=/user/cloudera/retail_db/categories --fields-terminated-by ","--hive-import --create-hive-table --hive-table retail_db.categories</pre>
  
## few commands 
<pre> hive> create database retail; </pre>
<pre> hive> use retail; </pre>
  
<pre> hive> create table person(id INT, Name STRING , age INT); </pre>                          
  
<pre> hive> create table person1(id INT, Name STRING , age INT) row format delimited fields terminated by ',' stored as textfile;</pre>    
<pre> hive> select count(*) from person1; </pre>   
<pre> hive> create table result as select a.name, a.age, b.mail from person a  join mail b on a.name=b.name; </pre>
<pre> hive> create external table mail (name STRING, mail STRING); 
</pre>
The create external keyword is used to create a table and provides a location where the table will create, so that Hive does not use a default location for this table. An EXTERNAL table points to any HDFS location for its storage, rather than default storage

<pre> hive> create table person2(id INT, Name STRING , age INT) partitioned by (gender STRING) clustered by (age) into 5 buckets;
  </pre>   
‘Partitioned by‘ is used to divided the table into the Partition and can be divided in to buckets by using the ‘Clustered By‘
## Writing a Hive script
<pre> create table product ( productid: int, productname: string, price: float, category: string) rows format delimited fields terminated by ‘,’ ;
load data local inpath ‘/home/cloudera/Desktop/data.txt’ into table product;
select * from product;</pre>
## Execute the Hive Script
<pre>hive –f /home/cloudera/Desktop/exemple.sql</pre>