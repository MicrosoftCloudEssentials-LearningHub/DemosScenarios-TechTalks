# Azure Data Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Azure Data Storage provides scalable, secure, and accessible cloud storage, ideal for big data and analytics, with various storage tiers. It supports a wide range of services and tools. Azure also offers relational and non-relational databases, with built-in management for high availability and performance, catering to different application needs.


## Content 

- [Data Storage](./0_DataStorage/)
- [Databases](./1_Databases/)

## Differences between Azure Data Storage and Databases

Azure Data Storage and Databases both persist data but are optimized for different purposes. Storage provides durable capacity while databases structure data for efficient access. Storage suits long-term file retention while databases enable interactive applications.

<img width="700" alt="image" src="https://github.com/brown9804/MSCloudEssentials_LPath/assets/24630902/ab71485a-5434-401e-ae25-277957c2ffb7">

Image from [here](https://www.edureka.co/blog/azure-storage-tutorial/)

| Storage | Database |
| --- | --- |
| Storage provides raw data capacity | It is structured for efficient querying and analysis |
| Data is opaque to storage system | Database has schema and metadata to represent data |
| Address data blocks through locations | Database uses abstractions like tables, documents |
| Enterprise storage connects to servers | Databases are accessed by clients |
| Durable long-term retention | Temporary persistence tier |


## DataFrames types: 

Comparative analysis of various types of DataFrames. Each type of DataFrame has its unique features and is suited for different use cases. The table below summarizes the key characteristics and common applications of each type:

| Feature                | Pandas DataFrame                                      | Spark DataFrame                                      | Azure Machine Learning Tables (MLTable)              | Azure Databricks DataFrames                          | AzureML Datasets                                     |
|------------------------|-------------------------------------------------------|------------------------------------------------------|------------------------------------------------------|------------------------------------------------------|------------------------------------------------------|
| **Data Size**          | Small to medium datasets that fit into memory         | Large datasets that require distributed computing    | Small to large datasets                              | Large datasets that require distributed computing    | Small to large datasets                              |
| **Execution**          | Eager execution (operations are executed immediately) | Lazy execution (operations are executed when an action is performed) | Eager execution                                      | Lazy execution                                       | Eager execution                                      |
| **Parallelization**    | Single-node processing                                | Multi-node processing                                | Single-node or multi-node processing                 | Multi-node processing                                | Single-node or multi-node processing                 |
| **Mutability**         | Mutable (can be changed)                              | Immutable (cannot be changed)                        | Mutable                                              | Immutable                                            | Mutable                                              |
| **Complex Operations** | Easier to perform                                     | More complex to perform                              | Easier to perform                                    | More complex to perform                              | Easier to perform                                    |
| **Performance**        | Slower for large datasets                             | Faster for large datasets                            | Depends on the underlying DataFrame                  | Faster for large datasets                            | Depends on the underlying DataFrame                  |
| **Primary Use Cases and Applications** | Data analysis, manipulation, and visualization; EDA, data cleaning, feature engineering, creating visualizations | Big data processing, machine learning, and streaming; large-scale data processing, ETL operations, running ML algorithms on big data | Data loading, transformation, and preprocessing for ML experiments; defining data loading blueprints with column type conversions and data filtering | Big data processing, collaborative data science, and running ML algorithms on distributed data | Data analysis, manipulation, preprocessing, and feeding data into ML models |
| **Language Support**   | Python                                                | Python, Scala, Java, R                               | Python                                               | Python, Scala, Java, R                               | Python                                               |
| **Azure Products**     | Azure Synapse Analytics, Azure Machine Learning, Azure Databricks, Azure Blob Storage, Azure Data Lake Storage | Azure Databricks, Azure Synapse Analytics, Azure HDInsight, Azure Data Explorer | Azure Machine Learning | Azure Databricks | Azure Machine Learning, Azure Open Datasets |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-366-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
