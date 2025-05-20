# Azure Databases: Optimizing Database Performance by Freeing Up Unused Space - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-05-20

----------

> [!IMPORTANT]
> Please note that `these demos are intended as a guide and are based on my personal experiences. For official guidance, support, or more detailed information, please refer to Microsoft's official documentation or contact Microsoft directly`: [Microsoft Sales and Support](https://support.microsoft.com/contactus?ContactUsExperienceEntryPointAssetId=S.HP.SMC-HOME)

> Microsoft offers a variety of database solutions, both relational and non-relational. Quick overview about strategies for managing and reducing their size, ensuring optimal performance and efficient use of storage resources. It's essential to `follow best practices and monitor the operation to avoid potential issues like long-running commands or blocking sessions`.

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Shrink a database](https://learn.microsoft.com/en-us/sql/relational-databases/databases/shrink-a-database?view=sql-server-ver16)
- [Types of Databases](https://azure.microsoft.com/en-gb/products/category/databases/)
- [Shrink Database Task (Maintenance Plan)](https://learn.microsoft.com/en-us/sql/relational-databases/maintenance-plans/shrink-database-task-maintenance-plan?view=sql-server-ver16)
- [Manage file space for databases in Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/file-space-manage?view=azuresql-db)
- [DBCC SHRINKFILE (Transact-SQL)](https://learn.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql?view=sql-server-ver16)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Overview](#overview)
- [Relational Databases](#relational-databases)
  - [Azure SQL Database](#azure-sql-database)
  - [Azure SQL Managed Instance](#azure-sql-managed-instance)
  - [SQL Server on Azure Virtual Machines](#sql-server-on-azure-virtual-machines)
  - [Azure Database for PostgreSQL](#azure-database-for-postgresql)
  - [Azure Database for MySQL](#azure-database-for-mysql)
- [Non-Relational Databases](#non-relational-databases)
  - [Azure Cosmos DB](#azure-cosmos-db)
  - [Azure Managed Instance for Apache Cassandra](#azure-managed-instance-for-apache-cassandra)
  - [Azure Cache for Redis](#azure-cache-for-redis)

</details>

## Overview 

> General Strategies for All Databases:

- **Archiving Old Data**: Move old or rarely accessed data to an archive database or storage solution. Reduces the size of the active database, improving performance and manageability. `Use SQL Server's built-in tools or third-party solutions to archive data based on specific criteria (e.g., date, usage).`
- **Data Compression**: Apply data compression techniques to reduce storage space.
- **Partitioning Tables**: Split large tables into smaller, more manageable pieces.
- **Index Optimization**: Regularly rebuild or reorganize indexes to reduce fragmentation.
- **Removing Unused Indexes**: Identify and remove indexes that are not being used.
- **Cleaning Up Unused Data**: Regularly delete or archive unused or obsolete data.
- **Monitoring and Maintenance**: Regularly monitor database size and performance, and perform maintenance tasks.
- **Using Filegroups**: Distribute database objects across multiple filegroups to improve performance and manageability.

<div align="center">
  <img src="https://github.com/user-attachments/assets/81d088ab-da80-4643-9c2c-2558709c90ff" alt="Centered Image" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

From [Managing database file space in Azure SQL Database](https://learn.microsoft.com/zh-cn/azure/azure-sql/database/file-space-manage?view=azuresql-db)

> General Tips:

| **Category**             | **Recommendation**                                                                                                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Regular Maintenance**  | Perform regular database maintenance tasks such as index rebuilding, updating statistics, and cleaning up old data.|
| **Monitoring and Alerts**| Set up monitoring and alerts to notify you when free space falls below your defined thresholds. Use Azure Monitor and SQL Insights for comprehensive monitoring.|
| **Backup and Recovery**  | Ensure you have a robust backup and recovery strategy in place to prevent data loss and minimize downtime.|

## Relational Databases

```mermaid
graph TD
    A[Relational Databases]

    A1[Azure SQL Database]
    A2[Azure SQL Managed Instance]
    A3[SQL Server on Azure Virtual Machines]
    A4[Azure Database for PostgreSQL]
    A5[Azure Database for MySQL]

    A --> A1
    A --> A2
    A --> A3
    A --> A4
    A --> A5

    A1 --> A1_1[Shrinking the Database]
    A1 --> A1_2[Data Compression]
    A1 --> A1_3[Index Optimization]
    A1 --> A1_4[Partitioning Tables]

    A2 --> A2_1[Shrinking the Database]
    A2 --> A2_2[Archiving Old Data]
    A2 --> A2_3[Removing Unused Indexes]
    A2 --> A2_4[Using Filegroups]

    A3 --> A3_1[Cleaning Up Unused Data]
    A3 --> A3_2[Monitoring and Maintenance]
    A3 --> A3_3[Data Compression]

    A4 --> A4_1[Partitioning Tables]
    A4 --> A4_2[Index Optimization]
    A4 --> A4_3[Archiving Old Data]

    A5 --> A5_1[Data Compression]
    A5 --> A5_2[Index Optimization]
    A5 --> A5_3[Cleaning Up Unused Data]
```

### Azure SQL Database

> Click here for additional information on this topic [Azure SQL Database: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/relational/0_az-sql-db.md) 

### Azure SQL Managed Instance

> Click here for additional information on this topic [Azure SQL Managed Instance: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/relational/1_az-sql-mi.md) 

### SQL Server on Azure Virtual Machines

> Click here for additional information on this topic [Azure SQL Managed Instance: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/relational/2_sql-az-vm.md)

### Azure Database for PostgreSQL

> Click here for additional information on this topic [Azure Database for PostgreSQL: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/relational/3_az-postgreSQL.md)

### Azure Database for MySQL

> Click here for additional information on this topic [Azure Database for MySQL: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/relational/4_az-db-mysql.md)

## Non-Relational Databases

```mermaid
graph TD
    A[Non-Relational Databases]

    A1[Azure Cosmos DB]
    A2[Azure Managed Instance for Apache Cassandra]
    A3[Azure Cache for Redis]

    A --> A1
    A --> A2
    A --> A3

    A1 --> A1_1[Partitioning]
    A1 --> A1_2[Index Optimization]
    A1 --> A1_3[Archiving Old Data]

    A2 --> A2_1[Data Compression]
    A2 --> A2_2[Index Optimization]
    A2 --> A2_3[Cleaning Up Unused Data]

    A3 --> A3_1[Data Eviction Policies]
    A3 --> A3_2[Monitoring and Maintenance]
```

### Azure Cosmos DB

> Click here for additional information on this topic [Azure Cosmos DB: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/non-relational/0_az-cosmosdb.md)

### Azure Managed Instance for Apache Cassandra

> Click here for additional information on this topic [Azure Managed Instance for Apache Cassandra: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/non-relational/1_az-mi-apache-cassandra.md)

### Azure Cache for Redis

> Click here for additional information on this topic [Azure Cache for Redis: Freeing Up Unused Space - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/8_DBFreeingUpUnusedSpace/non-relational/2_az-cache-redis.md)

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
