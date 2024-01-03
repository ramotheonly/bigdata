# Write Pyspark Dataframe to Dedicated SQL Table 

## Write to an Internal Table
<pre>
  <code class="language-mermaid">graph LR
    Spark-Dataframe --&gt; Dedicated-SQL-Internal-Table
  </code>
</pre>

```python
import com.microsoft.spark.sqlanalytics
from com.microsoft.spark.sqlanalytics.Constants import Constants

database_name = "your-database-name"
schema_name = "your-schema-name"
table_name = "your-table-name"
data_source_name = "<data-source-name>"

dfToWrite.write
               .option(Constants.SERVER, f"{mssparkutils.env.getWorkspaceName()}.sql.azuresynapse.net")
             # .option(Constants.DATA_SOURCE, f"{data_source_name}>)
               .mode("overwrite")      # other options => "error", "errorifexists", "append", "ignore"
               .synapsesql(f"{database_name}.{schema_name}.{table_name}")

```


## Write to an External Table
<pre>
  <code class="language-mermaid">graph LR
    Spark-Dataframe --&gt; Dedicated-SQL-External-Table
  </code>
</pre>

```python
write_to_path = "/path/to/ext/table"
dfToWrite.write
               .option(Constants.SERVER, f"{mssparkutils.env.getWorkspaceName()}.sql.azuresynapse.net")
             # .option(Constants.DATA_SOURCE, f"{data_source_name}>)
               .mode("overwrite")      # other options => "error", "errorifexists", "append", "ignore"
               .synapsesql(f"{database_name}.{schema_name}.{table_name}"
                              , Constants.EXTERNAL, write_to_path)

# **Note: If write_to_path = None, the path will default to /{database_name}/{schema_name}/{table_name}**
```
