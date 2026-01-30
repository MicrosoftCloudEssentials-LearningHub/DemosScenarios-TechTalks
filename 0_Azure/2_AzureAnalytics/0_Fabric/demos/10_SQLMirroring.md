# SQL Database Mirroring in Microsoft Fabric

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

## Wiki 

- [Public Preview: Azure SQL Database Mirroring in Microsoft Fabric](https://azure.microsoft.com/en-us/updates/public-preview-azure-sql-database-mirroring-in-microsoft-fabric/)
- [Mirroring Azure SQL Database (Preview)](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-sql-database)
- [Announcing the Public Preview of Mirroring in Microsoft Fabric](https://blog.fabric.microsoft.com/en-us/blog/announcing-the-public-preview-of-database-mirroring-in-microsoft-fabric?ft=All)
- [Announcing Mirroring Azure SQL Database in Fabric for Public Preview](https://techcommunity.microsoft.com/t5/azure-sql-blog/announcing-mirroring-azure-sql-database-in-fabric-for-public/ba-p/4085988)
- [How do I enable Mirroring in my tenant?](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/overview#how-do-i-enable-mirroring-in-my-tenant)
- [Limitations and behaviors in Microsoft Fabric mirrored databases from Azure SQL Database (Preview)](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-sql-database-limitations)

## Mirroring SQL Database in Microsoft Fabric

> Mirroring for Azure SQL Database is now available in public preview. This feature allows you to replicate your data residing in Azure SQL databases in near real-time directly into Microsoft Fabric's OneLake. However, it currently does not support Azure SQL Database instances behind a private network. You must update your Azure SQL logical server firewall rules to allow public network access to use this feature.

### Alternatives for Near Real-Time Data

If you need near real-time data from SQLDB and your SQL Server is in a private network, consider the following alternatives:

1. **Change Data Capture (CDC)** is a feature that captures changes made to data in your SQL Server tables. It records insert, update, and delete activities and makes the change data available for downstream processing.
    - **How it works**: CDC captures changes from the transaction log and stores them in change tables. These changes can then be processed and replicated to other systems.
    - **Use case**: Ideal for scenarios where you need to track and replicate changes in near real-time without impacting the performance of your primary database.
2. **Azure Data Factory with Self-hosted Integration Runtime**: Allows you to securely connect to your on-premises SQL Server and replicate data to Azure services.
    - **How it works**: Install the self-hosted integration runtime on a machine within your network. Create pipelines in ADF to copy data from SQL Server to your destination (e.g., Azure Blob Storage, Azure SQL Database).
    - **Use case**: Suitable for environments where the SQL Server is behind a private network and you need to orchestrate complex data workflows.
3. **Azure Event Hubs**: Is a big data streaming platform and event ingestion service capable of receiving and processing millions of events per second.
    - **How it works**: Use CDC or other mechanisms to capture changes and send them to Event Hubs. From there, you can stream the data to Azure Synapse Analytics or Azure Data Lake Storage for processing.
    - **Use case**: Best for scenarios requiring high-throughput data ingestion and real-time analytics.
4. **Azure Synapse Analytics**: Integrates big data and data warehousing capabilities, allowing you to analyze large volumes of data in near real-time.
    - **How it works**: Use Synapse pipelines to orchestrate data movement and transformation. Stream data from Event Hubs or other sources into Synapse for real-time processing.
    - **Use case**: Ideal for complex analytics and reporting on large datasets.

### Architecture References
1. [Near Real-Time Lakehouse Data Processing](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/data/real-time-lakehouse-data-processing): This architecture uses Azure Event Hubs, Azure Synapse Analytics, and Azure Data Lake Storage to keep lakehouse data in sync in near real-time. It involves capturing changes using Debezium connectors, streaming data to Event Hubs, and processing it in Synapse Analytics.
2. [Mirroring Azure SQL Database in Microsoft Fabric](https://www.mssqltips.com/sqlservertip/8001/microsoft-fabric-mirroring-for-data-replication/): Mirroring in Microsoft Fabric allows for near real-time replication of Azure SQL Database into Fabric's OneLake. This feature leverages SQL's CDC stack to keep data in sync without complex ETL processes. For more [click here](https://techcommunity.microsoft.com/t5/azure-sql-blog/announcing-mirroring-azure-sql-database-in-fabric-for-public/ba-p/4085988).
3. [Azure Well-Architected Framework](https://learn.microsoft.com/en-us/azure/well-architected/service-guides/azure-sql-database-well-architected-framework): This framework provides best practices for designing and operating reliable, secure, efficient, and cost-effective systems in the cloud. It includes guidance on using Active Geo-Replication and Auto Failover Groups for high availability and disaster recovery.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->