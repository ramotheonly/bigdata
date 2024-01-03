# Read from Dedicated SQL (internal) Table into a pyspark Dataframe

<pre>
  <code class="language-mermaid">graph LR
Dedicated SQL Query--&gt;Spark Dataframe
  </code>
</pre>

```python
import com.microsoft.spark.sqlanalytics
from com.microsoft.spark.sqlanalytics.Constants import Constants
from pyspark.sql.functions import col

database_name = "your-database-name"
schema_name = "your-schema-name"
table_name = "your-table-name"
filter_column = "filter-column-name"
filter_value = "filter-on-value"

limit_count = 10

col1 = "column1-name"
col2 = "column2-name"
col3 = "column3-name"

dfToLoad = ( spark.read
                 .option(Constants.SERVER, f"{mssparkutils.env.getWorkspaceName()}.sql.azuresynapse.net")
               # .option(Constants.TEMP_FOLDER, f"abss://{temp_container_name}@{temp_storage_account}.dfs.core.windoes.net/{temp_base_dir}/{temp_sub_dir}>)
                 .synapsesql(f"{database_name}.{schema_name}.{table_name}")
                 .select(f"{col1},{col2},{col3}")
                 .filter(col(f"{filter_column}").contains(f"{filter_value}"))
                 .limit(limit_count)
            )
dfToLoad.show()
```
## Using SQL
<pre>
  <code class="language-mermaid">graph LR
Dedicated SQL Table--&gt;Spark Dataframe
  </code>
</pre>

```python
dfToLoadUsingSQL = ( spark.read
                # .option(Constants.SERVER, f"{mssparkutils.env.getWorkspaceName()}.sql.azuresynapse.net")
                # .option(Constants.TEMP_FOLDER, f"abss://{temp_container_name}@{temp_storage_account}.dfs.core.windoes.net/{temp_base_dir}/{temp_sub_dir}>)
                 .option(Constants.DATABASE, database_name)
                 .option(Constants.QUERY, "SELECT COUNT(1) AS COUNT FROM [dbo].[test-feed-in]")
                 .synapsesql()
                 .limit(limit_count)
            )
dfToLoadUsingSQL.show()
```
