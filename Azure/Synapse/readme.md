# Synapse

2 Types of Databases available

## 1. Datalake - Compute = Spark pool

Datalake Store - unmanaged (or self managed) file storage in ADLS Gen2 using csv, parquet and delta formats

* ADLS Gen2 big data store (you have to manage)
* Code - Notebook
  * %%pyspark, %%sql, %%csharp etc.
  * Use **mssparkutils** in place of dbutils


## 2. Dedicated SQL (Warehouse) - Compute = Dedicated SQL Pool
* Fully managed SQL big data store
* Code - Notebook
  * SQL scripts

Snippets: 
1. [READ Pyspark Dataframe from a Dedicated SQL Table](code/snippets/pyspark/load-dataframe-from-a-dedicated-SQL-internal-table.md)
2. [WRITE Pyspark Dataframe to a Dedicated SQL Table](code/snippets/pyspark/write-dataframe-to-a-dedicated-SQL-internal-table.md)

