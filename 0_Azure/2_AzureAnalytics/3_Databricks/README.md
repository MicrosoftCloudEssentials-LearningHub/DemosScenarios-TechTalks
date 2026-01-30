# Azure Databricks

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

## References 

- [What is Azure Databricks?](https://learn.microsoft.com/en-us/azure/databricks/introduction/)
- [Tutorial: Implement Azure Databricks with an Azure Cosmos DB endpoint](https://learn.microsoft.com/en-us/azure/databricks/scenarios/service-endpoint-cosmosdb)
- [Query databases using JDBC](https://learn.microsoft.com/en-us/azure/databricks/connect/external-systems/jdbc)
- [Query SQL Server with Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/connect/external-systems/sql-server)
- [How to connect from Azure Databricks to Azure SQL DB using service](https://stackoverflow.com/collectives/azure/articles/75189853/how-to-connect-from-azure-databricks-to-azure-sql-db-using-service-principal)
- [Azure DataBricks To Connect SQL DataBase with Pyspark](https://stackoverflow.com/questions/76820391/azure-databricks-to-connect-sql-database-with-pyspark)
- [Use a SQL connector, driver, or API](https://learn.microsoft.com/en-us/azure/databricks/dev-tools/index-driver)
- [Connect to azure sql database from databricks](https://community.databricks.com/t5/data-engineering/connect-to-azure-sql-database-from-databricks-using-service/td-p/36174)
- [Query data in Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/databricks/connect/external-systems/synapse-analytics)
- [Connection from databricks to azure synapse](https://stackoverflow.com/questions/72873898/connection-from-databricks-to-azure-synapse)

## Introduction to Azure Databricks

> Azure Databricks is a comprehensive analytics platform for big data and AI, built on Apache Spark. It offers a collaborative workspace for data engineers, scientists, and analysts to engage in data processing, machine learning, and real-time analytics.

<figure>
<img
width="800"
src="https://github.com/user-attachments/assets/c6c298f2-aae2-4ae8-b6cc-0407a22a32a2"
alt="The beautiful MDN logo.">
<figcaption> <br/> From https://www.databricks.com/product/azure </figcaption>
</figure>

| Aspect | Details |
| ----- | ---- | 
| Pricing tier | - **Standard**: Includes core Apache Spark features and Microsoft Entra integration. <br/> - **Premium**: Offers role-based access controls and advanced enterprise features. <br/>  - **Trial**: Provides a 14-day free trial of our premium workspace. | 


### **Key Features**
Here are some of the key features of Azure Databricks:

| **Feature**            | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| **Data Processing**    | Efficiently process large volumes of data using Apache Spark.                   |
| **Machine Learning**   | Build, train, and deploy machine learning models at scale.                      |
| **Real-Time Analytics**| Perform real-time data analysis and generate insights quickly.                  |
| **Collaborative Workspace** | Provides a collaborative environment for different roles to work together. |
| **Scalability**        | Automatically scales resources to handle varying workloads.                     |
| **Integration**        | Seamlessly integrates with other Azure services and open-source tools.          |

This diagram shows how Azure Databricks integrates with various data sources and storage solutions, processes data using Apache Spark, and supports machine learning and real-time analytics.

```mermaid
graph TD
    A[Data Sources] -->|Azure Blob Storage, SQL DB| B[Azure Databricks Workspace]
    B --> C[Machine Learning - MLflow, etc.]

    E[Data Storage] -->|Azure Data Lake, SQL DB| F[Data Processing - Apache Spark]
    F --> D[Real-Time Analytics - Dashboards, etc.]

```

## Architecture and Components

Azure Databricks architecture is divided into two main components: 

| **Component**            | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Control Plane**        | Manages backend services, authentication, job scheduling, and cluster management. Hosts the web application and REST APIs. |
| **Compute Plane**        | Where data processing happens, consisting of clusters running Apache Spark jobs. |

There are two types of compute planes:

| **Type of Compute Plane**            | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Serverless Compute**   | Managed by Azure Databricks, with automatic scaling and resource management. Ideal for users preferring a hands-off approach. |
| **Classic Compute**      | Managed by the user, with full control over compute resources within their Azure subscription. Allows for more customization and manual scaling. |

This diagram below shows how the control plane interacts with both the serverless and classic compute planes.

```mermaid
graph TD
    subgraph Control Plane
        A[Backend Services]
        B[Web Application]
        C[REST APIs]
    end
    subgraph Compute Plane
        D[Serverless Compute]
        E[Classic Compute]
    end
    A --> D
    A --> E
    B --> D
    B --> E
    C --> D
    C --> E
```
  
## Recommended Trainings
- [Explore Azure Databricks](https://learn.microsoft.com/en-us/training/modules/explore-azure-databricks/)
- [Perform data analysis with Azure Databricks](https://learn.microsoft.com/en-us/training/modules/perform-data-analysis-azure-databricks/)
- [Use Apache Spark in Azure Databricks](https://learn.microsoft.com/en-us/training/modules/use-apache-spark-azure-databricks/)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
