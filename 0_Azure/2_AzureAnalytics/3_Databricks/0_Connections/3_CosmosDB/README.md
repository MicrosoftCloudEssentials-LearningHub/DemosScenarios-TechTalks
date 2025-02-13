#  Connecting to Azure Cosmos DB

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-02-13

----------

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

```mermaid
graph TD
    A[Azure Databricks] --> B[Azure Cosmos DB]
    B --> C[Data Processing - Apache Spark]
    B --> D[Machine Learning - MLflow, etc.]
    B --> E[Real-Time Analytics - Dashboards, etc.]
````
1. Ensure you have Cosmos DB and Databricks with the cluster set up.
2.  Install the Cosmos DB Spark Connector:
     - Download the latest `azure-cosmosdb-spark` library.
     - Upload the JAR file to your Databricks workspace.
     - Install the library on your Databricks cluster.
3. Configure the Connection: Use the following code snippet in a Databricks notebook to configure the connection to Cosmos DB.
   
   > This setup allows you to read from and write to Azure Cosmos DB directly from your Databricks environment, enabling efficient data processing and analytics.

```python
   # Configuration for Cosmos DB
cosmos_endpoint = "your_cosmos_db_endpoint"
cosmos_master_key = "your_cosmos_db_master_key"
cosmos_database_name = "your_database_name"
cosmos_container_name = "your_container_name"

# Read data from Cosmos DB
cosmos_config = {
    "Endpoint": cosmos_endpoint,
    "Masterkey": cosmos_master_key,
    "Database": cosmos_database_name,
    "Collection": cosmos_container_name,
    "Upsert": "true"
}

df = spark.read.format("com.microsoft.azure.cosmosdb.spark").options(**cosmos_config).load()
df.show()
```
