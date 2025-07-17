# Fabric + Databricks: Medallion Architecture 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [TechExcel: Microsoft Fabric with Azure Databricks for Data Analytics (lvl 300 / CSU) lab](https://microsoft.github.io/TechExcel-Fabric-with-Databricks-for-Data-Analytics/)
- [Databricks Unity Catalog tables available in Microsoft Fabric](https://blog.fabric.microsoft.com/en-us/blog/databricks-unity-catalog-tables-available-in-microsoft-fabric/)
- [Integrate OneLake with Azure Databricks](https://learn.microsoft.com/en-us/fabric/onelake/onelake-azure-databricks)
- [Tutorial: Configure Microsoft Fabric mirrored databases from Azure Databricks (Preview)](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-databricks-tutorial)
- [Integrating Microsoft Fabric with Azure Databricks Delta Tables](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/integrating-microsoft-fabric-with-azure-databricks-delta-tables/3916332)
- [Data Intelligence End-to-End with Azure Databricks and Microsoft Fabric](https://techcommunity.microsoft.com/blog/azurearchitectureblog/data-intelligence-end-to-end-with-azure-databricks-and-microsoft-fabric/4232621)

</details>

## Overview 

| Resource   | Key Components           | Details                                                                 |
|------------|--------------------------|-------------------------------------------------------------------------|
| Databricks | - ETL Tasks<br/> - Data Ingestion              | ETL Tasks: Databricks efficiently handles Extract, Transform, Load (ETL) tasks. It manages the bronze, silver, and gold layers of the medallion architecture: <br> - **Bronze Layer**: Raw data ingestion from various sources. <br> - **Silver Layer**: Data cleaning and transformation. <br> - **Gold Layer**: Aggregated and refined data ready for analysis. <br> Data Ingestion: Supports batch and streaming data ingestion, ensuring real-time data processing capabilities. <br> - **Data Cleaning**: Utilizes Apache Spark's powerful processing engine to clean and transform data at scale. <br> - **Aggregation**: Performs complex aggregations and computations, making data ready for downstream analytics. |
| Fabric     | - Data Integration <br> - Orchestration <br> - Monitoring and Management | Fabric seamlessly integrates with Databricks, providing a unified interface for managing data workflows. <br> - **Data Integration**: Facilitates the orchestration of data pipelines, ensuring smooth data flow between different stages of processing. <br> - **Monitoring and Management**: Offers robust monitoring and management tools to track data pipeline performance and troubleshoot issues. |

> Here is a [reference of a medallion architecture using only Fabric](https://github.com/MicrosoftCloudEssentials-LearningHub/MS-Fabric-Essentials-Workshop/tree/main/AzurePortal/1_MedallionArch):

<p align="center">
  <img width="650" alt="image" src="https://github.com/user-attachments/assets/15a7dbfe-524b-4aa9-9b45-3db6bca2dd03" />
</p>

> If you need to handle `complex data transformations and large-scale data processing`, you can use our combined solution of **Fabric + Databricks**. This powerful combination leverages the strengths of both platforms to provide a robust data processing pipeline. This workshop on [Fabric with Databricks for Data Analytics](https://microsoft.github.io/TechExcel-Fabric-with-Databricks-for-Data-Analytics/) offers a comprehensive step-by-step guide on developing Medallion Architecture using Fabric and Databricks. <br/>

<p align="center">
  <img width="650" alt="image" src="https://github.com/user-attachments/assets/58431d3b-e294-46fe-89a4-92a046168ec4" />
</p>

## Integration with Multiple Sources:

> In these two examples of Medallion Architecture, `Azure SQL Database` was used as the input source, but the solution is highly flexible and can integrate with multiple data sources, including:

- **Cloud Storage**: Azure Blob Storage, AWS S3, Google Cloud Storage.
- **Databases**: SQL Server, MySQL, PostgreSQL, Oracle.
- **Streaming Sources**: Kafka, Event Hubs, IoT Hub.
- **APIs and Web Services**: REST APIs, SOAP services.


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-366-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
