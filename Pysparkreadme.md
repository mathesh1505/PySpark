# PySpark:
# 1. Introduction to PySpark: 
# 1.1 PySpark Overview: 
PySpark is the Python API for Apache Spark, used to process large datasets in a distributed computing environment.It allows you to write Spark applications using Python instead of Scala/Java.
# It is commonly used for:
* Big data processing
* Distributed computing
* ETL pipelines
* Data analytics
# It supports:
* Spark SQL
* Spark MLib
* Dataframe
* RDD
# 1.2 Introduction to PySpark and its role in big data processing:
In big data, datasets are too large to process on a single machine.
# PySpark helps by:
* Distributing data across multiple machines (nodes)
* Processing data in parallel
* Using in-memory computation (very fast)
* Providing fault tolerance
# Example scenario:
A company processes 10 TB of user logs every day.PySpark splits logs across 10 machines → each machine processes 1 TB → overall process finishes much faster.
# 1.3 Python API for Apache Spark. 
PySpark provides Python functions to interact with Spark.
# 2. Revision on Spark Architecture: 
# 2.1 Revising the architecture of Spark. 
Spark follows Master–Slave architecture.
# Simple Flow:
* Your PySpark program → runs on Driver
* Driver splits job into tasks
* Cluster manager assigns tasks to Executors
* Executors process data in parallel
* Results are sent back to Driver
# 2.2 Integration with Spark components like Driver and Executors. 
# Driver Program
* Runs your Python code
* Creates SparkSession
* Plans tasks using DAG Scheduler
* Sends tasks to executors
# Executors
* Run tasks given by driver
* Perform transformations like map, filter
* Store data in memory (RDD/DataFrame caching)
* Return results to Driver
# 3. Revision on Spark Components: 
* SparkSession:Entry point for DataFrame, SQL, RDD, ML and it Combines SQLContext, HiveContext, and SparkContext
* RDD:Low-level distributed dataset.It supports transformations (map, filter) and it has no schema.
* DataFrame:High-level structured dataset and it Has schema (rows & columns).Optimized by Catalyst optimizer
* DAG Scheduler:Converts execution plan into stages, Handles failures
# 4. SparkSession: 
# 4.1 Explanation of SparkSession as the entry point to PySpark. 
SparkSession is the entry point to PySpark functionality.You cannot use DataFrames or SQL without SparkSession.
* It provides access to:
* SparkContext
* SQLContext
# 4.2 Configuring and creating a SparkSession. 
<img width="837" height="136" alt="image" src="https://github.com/user-attachments/assets/39ed8ec3-539d-4a54-839e-0cfadd6531bc" />

# 5 DataFrame API in PySpark:
# 5.1 Overview of the DataFrame API
A PySpark DataFrame is a distributed table consisting of rows and columns, similar to SQL or Pandas DataFrame — but optimized for big data and parallel processing.
# Key Features:
* Schema-based (column names + data types)
* Distributed (works across multiple nodes)
* Optimized using Catalyst Optimizer
* Lazy evaluation
* Supports SQL-like operations (select, filter, groupBy)
* Can handle terabytes of data
# 5.2 Comparison: PySpark DataFrame vs Pandas DataFrame
| Feature             | PySpark DataFrame             | Pandas DataFrame                  |
| ------------------- | ----------------------------- | --------------------------------- |
| **Execution**       | Distributed, parallel         | Single machine                    |
| **Data Size**       | Huge datasets (GB–TB–PB)      | Small datasets (fits in RAM)      |
| **Speed**           | Faster for big data           | Faster for small data             |
| **Memory**          | Uses cluster memory           | Uses local RAM                    |
| **API Style**       | SQL + functional              | Pythonic, row-wise                |
| **Lazy Evaluation** | Yes                           | No (runs immediately)             |
| **Optimization**    | Catalyst optimizer            | No optimizer                      |
| **Fault Tolerance** | Yes (using RDD lineage)       | No                                |
| **Best For**        | Big data, ETL, distributed ML | Small/medium data, quick analysis |
# 6 Transformations and Actions in PySpark:
# 6.1 Understanding Transformations and Actions:
Transformations are operations that create a new RDD/DataFrame from an existing one.They are lazy, meaning Spark does not compute the result immediately.
# Two Types of Transformations
* Narrow Transformations:No data shuffle,Fast.Example: map, filter, select
* Wide Transformations:Requires data shuffle between nodes,Slower,Example: groupBy, reduceByKey, join
  
Actions trigger execution of the transformations and return the output to driver (collect),count(),show().
Spark runs the whole DAG only when an action is called.
# 6.2 Examples of Common Transformations and Actions:
# Map:
Applies a function to each element

<img width="690" height="153" alt="Screenshot 2025-11-24 102316" src="https://github.com/user-attachments/assets/97ad9abe-d065-4c9e-a271-9d4405b484aa" />

# Filter:
Filter the element based on the given condition 

<img width="654" height="392" alt="Screenshot 2025-11-24 102841" src="https://github.com/user-attachments/assets/9114a669-695c-4c39-8a1a-3678f73061a2" />

# Joins:
<img width="845" height="317" alt="Screenshot 2025-11-24 103311" src="https://github.com/user-attachments/assets/9eb90e66-11cf-4842-9abb-040c5e81220e" />

# Order by:
It will return the values as ascending or descending order.

<img width="575" height="543" alt="Screenshot 2025-11-24 105118" src="https://github.com/user-attachments/assets/996a6364-ec9d-4766-86a1-520c5b0ff737" />

# Group by:
It will group the results.

<img width="665" height="528" alt="Screenshot 2025-11-24 105033" src="https://github.com/user-attachments/assets/f64706db-9947-4a5a-adf5-15960395733e" />

# 7 Revision on Spark RDDs:
# 7.1 Overview of RDDs in PySpark
RDD (Resilient Distributed Dataset) is the fundamental data structure in Spark.It is a distributed collection of data, processed in parallel across multiple nodes in a cluster.
# 7.2 Differences between RDDs and DataFrames:
| Feature             | RDD                                        | DataFrame                         |
| ------------------- | ------------------------------------------ | --------------------------------- |
| **Definition**      | Low-level distributed data structure       | High-level tabular data structure |
| **Schema**          | No schema (unstructured)                   | Has schema (columns + datatypes)  |
| **Ease of Use**     | Complex (requires custom code)             | Very easy (SQL-like operations)   |
| **Optimization**    | No optimization                            | Optimized by Catalyst optimizer   |
| **Speed**           | Slower                                     | Much faster                       |
| **Memory Usage**    | High                                       | Low (uses Tungsten engine)        |
| **APIs Supported**  | Only functional (map, filter, reduce)      | SQL, DataFrame, MLlib             |
| **Error Handling**  | Harder (no schema)                         | Easier (schema validation)        |
| **Use Cases**       | Unstructured data, complex transformations | Structured data, analytics, ETL   |
| **Lazy Evaluation** | Yes                                        | Yes                               |

# 8 Data Structures in PySpark:
PySpark mainly works with the following distributed data structures:
* RDD (Resilient Distributed Dataset):Low-level distributed list
* DataFrame:Distributed table with schema
* Row:Single record in DataFrame
* Column:Expression representing a column

<img width="664" height="660" alt="Screenshot 2025-11-24 104528" src="https://github.com/user-attachments/assets/0736a6f3-173c-416c-82d9-f9a02f7bd332" />

# 9 SparkContext:
SparkContext is the core entry point for low-level Spark functionality.It allows you to work with RDDs, manage cluster resources, and communicate with the Spark cluster.Today, most applications use SparkSession, but SparkContext still exists inside SparkSession and is used for RDD operations.
# 9.1 The Role of SparkContext in PySpark Applications:
It is the main entry point to Spark's lower-level API (RDD API).
It connects your PySpark application to the Spark cluster.
It is responsible for:
* Creating RDDs
* Managing workers/executors
* Distributing tasks
* Coordinating jobs and stages
# 10 PySpark DataFrames:
10.1 Introduction to PySpark DataFrames
A DataFrame in PySpark is a distributed collection of data organized into named columns, similar to a table in a database or an Excel sheet.
* It is built on top of the Spark SQL engine, meaning:
* It supports SQL queries
* It automatically handles optimizations using Catalyst Optimizer
* It is faster than RDDs due to optimized execution
# 10.1 Operations on DataFrames, including filtering, selecting, and aggregating:

# Filter:
<img width="1266" height="770" alt="Screenshot 2025-11-25 105942" src="https://github.com/user-attachments/assets/319e73de-9421-4cc2-a2ca-8cf015eb4b8a" />

# Selecting and aggregating:
<img width="649" height="473" alt="Screenshot 2025-11-25 105538" src="https://github.com/user-attachments/assets/4b8c326d-ea94-4abe-a86c-4fcf859a539a" />

# 11 Pyspark SQL:
PySpark SQL allows you to write SQL queries on DataFrames.
11.1 Integration of SQL Queries with PySpark
* Run SQL queries
* Create temporary views
* Join DataFrames using SQL
* Use functions (SUM, AVG, COUNT, etc.)
* Work with complex data at scale
# 11.2 Registering DataFrames as Temporary SQL Tables:
To run SQL queries, you must register the DataFrame as a temporary view.

<img width="861" height="596" alt="Screenshot 2025-11-25 103411" src="https://github.com/user-attachments/assets/5037d9d9-06bf-4a15-a0d6-b1c70ba4a454" />

# 12 Techniques for caching and persisting RDDs and DataFrames.
PySpark uses lazy evaluation, meaning transformations are not executed until an action is called. When a DataFrame/RDD is used multiple times, Spark can recompute it repeatedly, which is expensive.
To avoid recomputation, Spark provides cache() and persist() to store RDD/DataFrame in memory or disk.
# Cache():
cache() is a shorthand for persisting the data in memory only.
# How it works:
* When you call df.cache(), Spark marks the DataFrame to be stored in memory.
* The first action triggers the computation and stores partitions in memory.
* Future actions will reuse the cached data → faster.
# persist():
persist() allows you to specify the storage level (memory, disk, serialization).

| Storage Level     | Meaning                                    |
| ----------------- | ------------------------------------------ |
| `MEMORY_ONLY`     | Store only in RAM                          |
| `MEMORY_AND_DISK` | RAM first, spill to disk if not enough RAM |
| `DISK_ONLY`       | Store only on disk                         |
| `MEMORY_ONLY_SER` | Serialized format in memory                |
| `OFF_HEAP`        | Store in off-heap memory (Tungsten)        |

# 13 General DataFrame Functions:

| Function           | Purpose                    |
| ------------------ | -------------------------- |
| show()             | Display DataFrame          |
| collect()          | Return all rows to driver  |
| take(n)            | Return first n rows        |
| printSchema()      | Print column names + types |
| count()            | Row count                  |
| select()           | Select specific columns    |
| filter() / where() | Filter rows                |
| like()             | Pattern matching           |
| sort()             | Sort rows                  |
| describe()         | Summary statistics         |
| columns            | List of column names       |

# Printschema,describe:

<img width="701" height="532" alt="Screenshot 2025-11-25 111009" src="https://github.com/user-attachments/assets/d9eb3345-486f-4beb-bb89-de327f2995e4" />

<img width="806" height="505" alt="Screenshot 2025-11-25 111023" src="https://github.com/user-attachments/assets/9c27e177-aee0-488b-ace1-e34b1f3567b2" />

## 14. String Functions

### **14.1 upper()**

Converts all characters in a string to uppercase.

**Example:**

```python
from pyspark.sql.functions import upper

Df.withColumn("UpperName", upper(col("name")))
```


### **14.2 trim()**

Removes both leading and trailing spaces.

**Example:** `trim(col("name"))`


### **14.3 ltrim()**

Removes leading (left) spaces.

### **14.4 rtrim()**

Removes trailing (right) spaces.

### **14.5 substring_index()**

Extracts substring before/after a delimiter based on position.

**Example:**
`substring_index(col("email"), "@", 1)` → returns string before '@'.

### **14.6 substring()**

Extracts substring from a given position with length.

**Example:**
`substring(col("name"), 1, 3)` → first 3 characters.

### **14.7 split()**

Splits a string into an array by the given delimiter.

**Example:**
`split(col("address"), ",")`

### **14.8 repeat()**

Repeats a string N times.

**Example:**
`repeat(col("category"), 3)`


### **14.9 rpad()**

Pads the right side of a string until a fixed length.

**Example:**
`rpad(col("code"), 6, "0")`

### **14.10 lpad()**

Pads the left side of a string.

**Example:**
`lpad(col("code"), 6, "0")`

### **14.11 regex_replace()**

Replaces a substring that matches a regex.

**Example:**
`regex_replace(col("phone"), "-", "")`

### **14.12 lower()**

Converts all characters to lowercase.

### **14.13 regex_extract()**

Extracts substring using regex pattern.

**Example:**
`regex_extract(col("email"), "(.*)@", 1)`

### **14.14 length()**

Returns length of a string.

**Example:**
`length(col("name"))`

### **14.15 instr()**

Finds position of a substring in a string.

**Example:**
`instr(col("email"), "@");`

### **14.16 initcap()**

Converts first letter of each word to uppercase.

**Example:**
`initcap(col("full_name"))`

<img width="1099" height="661" alt="Screenshot 2025-11-25 181643" src="https://github.com/user-attachments/assets/6f2ad8e7-9ed3-4b25-8170-93cf4e89da56" />

## 15. Numeric Functions

### **15.1 SUM()**

Returns the sum of values.

**Example:**
`df.groupBy().sum("salary")`


### **15.2 AVG()**

Returns average value.

### **15.3 MIN()**

Returns minimum value.

### **15.4 MAX()**

Returns maximum value.

### **15.5 ROUND()**

Rounds numeric values to a given number of decimal places.

**Example:**
`round(col("price"), 2)`

### **15.6 ABS()**

Returns the absolute value.

**Example:**
`abs(col("difference"))`

<img width="1026" height="542" alt="Screenshot 2025-11-25 181713" src="https://github.com/user-attachments/assets/d913dafb-3501-492d-a3c6-4b7d4e3b2408" />


# 16. Date and Time Functions

## 16.1 CURRENT_DATE()

Returns the current system date.

```python
df = spark.range(1).
    withColumn("current_date", F.current_date())
df.show()
```

## 16.2 CURRENT_TIMESTAMP()

Returns the current timestamp.

```python
df = spark.range(1).
    withColumn("current_ts", F.current_timestamp())
df.show()
```

## 16.3 DATE_ADD()

Adds days to a date.

```python
df = df.withColumn("date_plus_5", F.date_add(F.current_date(), 5))
```

## 16.4 DATEDIFF()

Returns the number of days between two dates.

```python
df = spark.createDataFrame([("2024-01-01", "2024-01-10")]).toDF("start", "end")
df = df.withColumn("diff", F.datediff("end", "start"))
```

## 16.5 YEAR()

Extracts year from date.

```python
df = df.withColumn("year", F.year(F.current_date()))
```

## 16.6 MONTH()

Extracts month from date.

```python
df = df.withColumn("month", F.month(F.current_date()))
```

## 16.7 DAY()

Extracts day of month.

```python
df = df.withColumn("day", F.dayofmonth(F.current_date()))
```

## 16.8 TO_DATE()

Converts string to date.

```python
df = spark.createDataFrame([("2024-11-10",)], ["dt_str"])
df = df.withColumn("dt", F.to_date("dt_str"))
```

## 16.9 DATE_FORMAT()

Formats date to a specific pattern.

```python
df = df.withColumn("formatted", F.date_format(F.current_date(), "dd-MM-yyyy"))
```

---
<img width="1435" height="978" alt="image" src="https://github.com/user-attachments/assets/466b705e-90d0-4fbb-a361-1faf787de7af" />


# 17. Aggregate Functions

## 17.1 mean()

Calculates mean.

```python
df.select(F.mean("value")).show()
```

## 17.2 avg()

Alias of mean.

```python
df.select(F.avg("value")).show()
```

## 17.3 collect_list()

Collects values into a list including duplicates.

```python
df.groupBy("id").agg(F.collect_list("value")).show()
```

## 17.4 collect_set()

Collects unique values into a set.

```python
df.groupBy("id").agg(F.collect_set("value")).show()
```

## 17.5 countDistinct()

Counts distinct values.

```python
df.select(F.countDistinct("value")).show()
```

## 17.6 count()

Counts rows.

```python
df.count()
```

## 17.7 first()

Returns first element.

```python
df.select(F.first("value")).show()
```

## 17.8 last()

Returns last element.

```python
df.select(F.last("value")).show()
```

## 17.9 max()

Returns maximum value.

```python
df.select(F.max("value")).show()
```

## 17.10 min()

Returns minimum value.

```python
df.select(F.min("value")).show()
```

## 17.11 sum()

Returns sum of values.

```python
df.select(F.sum("value")).show()
```

---

# 18. Joins

Assume two DataFrames:

```python
df1 = spark.createDataFrame([(1, "A"), (2, "B")], ["id", "value1"])
df2 = spark.createDataFrame([(1, "X"), (3, "Y")], ["id", "value2"])
```

## 18.1 Inner Join

Returns matching rows.

```python
df1.join(df2, "id", "inner").show()
```

## 18.2 Cross Join

Cartesian product.

```python
df1.crossJoin(df2).show()
```

## 18.3 Outer Join (Full Outer)

Returns matched + unmatched rows.

```python
df1.join(df2, "id", "outer").show()
```

## 18.4 Left Join

Returns all rows from left.

```python
df1.join(df2, "id", "left").show()
```

## 18.5 Right Join

Returns all rows from right.

```python
df1.join(df2, "id", "right").show()
```

## 18.6 Left Semi Join

Returns rows from left when match exists, but only left columns.

```python
df1.join(df2, "id", "left_semi").show()
```

## 18.7 Left Anti Join

Returns rows from left *without* match.

```python
df1.join(df2, "id", "left_anti").show()
```
