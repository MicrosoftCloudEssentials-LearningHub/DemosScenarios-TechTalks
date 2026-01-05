# Connecting to SQL Databases

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->

> You can connect to SQL databases using JDBC or SQL connectors. Here are the steps for both methods:

## **Using JDBC**

**Configure the Connection**: Use the following code snippet in a Databricks notebook to configure the connection to SQL Server or Azure SQL Database:

```python
# Configuration for SQL Database
jdbcHostname = "your_sql_server_hostname"
jdbcPort = 1433
jdbcDatabase = "your_database_name"
jdbcUsername = "your_username"
jdbcPassword = "your_password"

jdbcUrl = f"jdbc:sqlserver://{jdbcHostname}:{jdbcPort};database={jdbcDatabase}"

# Read data from SQL Database
df = spark.read.format("jdbc") \
    .option("url", jdbcUrl) \
    .option("dbtable", "your_table_name") \
    .option("user", jdbcUsername) \
    .option("password", jdbcPassword) \
    .load()

df.show()
```

## **Using SQL Connectors**

**Install the SQL Spark Connector**: You can install the SQL Spark Connector using Maven coordinates or within a Databricks notebook using `%pip`.

```python
# Install the SQL Spark Connector
%pip install pyodbc

# Configuration for SQL Database
jdbcHostname = "your_sql_server_hostname"
jdbcPort = 1433
jdbcDatabase = "your_database_name"
jdbcUsername = "your_username"
jdbcPassword = "your_password"

jdbcUrl = f"jdbc:sqlserver://{jdbcHostname}:{jdbcPort};database={jdbcDatabase}"

# Read data from SQL Database
df = spark.read.format("jdbc") \
    .option("url", jdbcUrl) \
    .option("dbtable", "your_table_name") \
    .option("user", jdbcUsername) \
    .option("password", jdbcPassword) \
    .load()

df.show()
```
