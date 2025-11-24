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
