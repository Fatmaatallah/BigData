# Sqoop commands


## List all databases
<pre>sqoop-list-databases --connect jdbc:mysql://localhost --username root --password cloudera</pre>

## List all tables from <b>retail_db</b> database
<pre>sqoop-list-tables --connect jdbc:mysql://localhost/retail_db --username root -P </pre>

## Evaluate
<pre>sqoop eval --connect jdbc:mysql://localhost/retail_db --username root --password cloudera --query "select * from categories"</pre>

## IMPORT Command with target directory
<pre>sqoop import --connect jdbc:mysql://localhost/retail_db --username root --password cloudera --table categories --m 1 --target-dir=/user/cloudera/out</pre>
<pre>-m 1 using one mapper task</pre>

## IMPORT Command with Where Clause
<pre>sqoop import --connect jdbc:mysql://localhost/retail_db --username root --password cloudera --table categories --m 3 --where "category_department_id in (2, 4)" --target-dir=/user/cloudera/out1
</pre>

## Import table with  parquet format into a single file
<pre>sqoop-import --connect jdbc:mysql://localhost/retail_db --username root --password cloudera  --table categories --m 3 --where "category_department_id in (2, 4)" --target-dir /user/cloudera/out1/cat_parquet --as-parquetfile </pre>

## Import All Tables
<pre>sqoop import-all-tables --connect jdbc:mysql://localhost/retail_db --target-dir= /user/cloudera/retaildb/ --username root -P</pre>

## Incremental Import
<pre>sqoop import --connect jdbc:mysql://localhost/retail_db --username root --table categories --target-dir=/user/cloudera//out --incremental append --check-column category_department_id --last-value 8
 -P</pre>

## Export command
<pre>sqoop export --connect jdbc:mysql://localhost/employees --username root --table cat --export-dir= /user/cloudera/output
 -P</pre>













