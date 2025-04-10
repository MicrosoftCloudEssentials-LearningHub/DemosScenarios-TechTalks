# Azure Synapse: Dynamically Remove Space - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-24

----------

> [!NOTE]
> Both the `table name and column name fields will be reviewed`. We'll remove any blank spaces to create the view.

## Wiki 

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [What is Azure Synapse Analytics?](https://learn.microsoft.com/en-us/azure/synapse-analytics/overview-what-is)
- [What is dedicated SQL pool (formerly SQL DW) in Azure Synapse Analytics?](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is)
- [Serverless SQL pool in Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql/on-demand-workspace-overview)
- [Create and use views using serverless SQL pool in Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/synapse-analytics/sql/create-use-views)
  
</details>

## Content

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Wiki](#wiki)
- [Content](#content)
- [Overview](#overview)
    - [SQL Pools](#sql-pools)
    - [Synapse Views](#synapse-views)
- [How to Dynamically Remove Space in field name](#how-to-dynamically-remove-space-in-field-name)

</details>

## Overview 

> `Azure Synapse Analytics` is an integrated analytics service that accelerates time to insight across data warehouses and big data systems.
> It combines the `best of SQL technologies used in enterprise data warehousing`, Spark technologies for big data, and data integration
> capabilities to provide a unified experience for data professionals

<img width="550" alt="image" src="https://github.com/user-attachments/assets/9a753e36-e229-4da7-8a87-a5c21ddd70f9"> <br/>
From [Microsoft Official Documentation](https://learn.microsoft.com/en-us/azure/synapse-analytics/overview-what-is)

### SQL Pools

SQL pools in Azure Synapse Analytics come in two main types:

| Type | Description | Characteristics | 
| --- | --- | --- |
| Serverless SQL Pool (built in) | This is a built-in, on-demand query service in Azure Synapse Analytics. You don't need to provision or manage any infrastructure. You simply run your queries, and you're billed based on the amount of data processed. It's great for ad-hoc querying and exploring data in your data lake without worrying about the underlying infrastructure. |    - A query service over data in your data lake. <br/> - No infrastructure setup or clusters to maintain. <br/> - Pay-per-use model, charging only for the data processed by queries. <br/> - Suitable for ad-hoc querying and data exploration. |
| Dedicated SQL Pool (formerly SQL DW) | This requires you to provision and manage a set of resources (Data Warehousing Units or DWUs). You have control over the performance and scale of your data warehouse, but it also means you need to manage the infrastructure. It's ideal for large-scale, high-performance analytics and data warehousing. |    - A collection of analytic resources provisioned when using Synapse SQL. <br/> - Uses Data Warehousing Units (DWU) to determine size and performance. <br/> - Ideal for large-scale data warehousing and high-performance analytics. | 

### Synapse Views

> **Synapse views** are `virtual tables created by querying data from one or more tables in Azure Synapse Analytics.
> They don't store data themselves but provide a way to simplify complex queries and reuse them`. Views can be created over both dedicated and serverless SQL pools.

## How to Dynamically Remove Space in field name

- For an overview of Serverless SQL Pool (built-in), please read this [overview](./0_serverlessSQLPool)
- For information on Dedicated SQL Pool (formerly SQL DW), click [here](./1_dedicatedSQLPoolStoreProc)

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
