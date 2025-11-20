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
