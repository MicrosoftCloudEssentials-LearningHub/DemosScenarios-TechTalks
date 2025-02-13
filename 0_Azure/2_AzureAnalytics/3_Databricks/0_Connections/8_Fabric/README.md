# Connecting to Azure Fabric

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-15

----------

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

## Wiki
- [Using Azure Databricks with Microsoft Fabric and OneLake](https://blog.fabric.microsoft.com/en-us/blog/using-azure-databricks-with-microsoft-fabric-and-onelake?ft=All:)

<img width="600" alt="image" src="https://github.com/user-attachments/assets/4806d8dc-5a64-4a68-bc03-28ebcf6b9672">

- [Modern Analytics with Microsoft Fabric and Azure Databricks](https://microsoft.github.io/TechBoost-Fabric-with-Databricks-for-Data-Analytics/)

<img width="600" alt="image" src="https://microsoft.github.io/TechBoost-Fabric-with-Databricks-for-Data-Analytics/docs/media/instructions240153/ArchitectureDiagramMFADBNew.png">

- [Integrating Microsoft Fabric with Azure Databricks Delta Tables](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/integrating-microsoft-fabric-with-azure-databricks-delta-tables/ba-p/3916332)
  
<img width="600" alt="image" src="https://github.com/user-attachments/assets/d1ad3eff-393c-4844-b59c-61c02b8b6bbd">

- [Unlock real-time insights with AI-powered analytics in Microsoft Fabric](https://www.microsoft.com/en-us/microsoft-fabric/blog/2024/05/21/unlock-real-time-insights-with-ai-powered-analytics-in-microsoft-fabric/?msockid=3503e0f1146666d41e52f49515ff6798)

- [Microsoft Fabric with Azure Databricks for Data Analytics](https://microsoft.github.io/TechExcel-Fabric-with-Databricks-for-Data-Analytics/)

<img width="600" alt="image" src="https://microsoft.github.io/TechExcel-Fabric-with-Databricks-for-Data-Analytics/docs/media/instructions240153/ArchitectureDiagramMFADBNew.png">

## How to Integrate Microsoft Fabric with Azure Databricks

```mermaid
graph TD
    A[Azure Databricks] -->|Read/Write Data| B[OneLake in Microsoft Fabric]
    B -->|Store Data| C[Data Lakehouse]
    C -->|Process Data| A
    C -->|Visualize Data| D[Power BI]
    D -->|Create Reports| E[Business Insights]
    subgraph Setup
        A1[Create Databricks Workspace] --> A2[Create Cluster]
        B1[Create Fabric Workspace] --> B2[Set Up OneLake]
    end
    subgraph Connectivity
        A3[Connect Databricks to OneLake] --> A4[Load Data]
        A4 --> A5[Process Data]
        A5 --> A6[Write Data to OneLake]
        A6 --> A7[Verify Data]
    end
    subgraph Visualization
        D1[Connect Power BI] --> D2[Create Reports]
    end
    Setup --> Connectivity --> Visualization
```

1. Set Up Azure Databricks
   - **Create a Databricks Workspace**: Go to the Azure portal and create a new Databricks workspace.
   - **Create a Cluster**: In the Databricks workspace, create a new cluster. Ensure that you enable Azure Data Lake Storage (ADLS) credential passthrough in the advanced options for authentication.

2. Configure Microsoft Fabric
   - **Create a Fabric Workspace**: Set up a workspace in Microsoft Fabric.
   - **Set Up OneLake**: Ensure OneLake is configured as your unified data lake within Microsoft Fabric.

3. Establish Connectivity
   - **Connect Databricks to OneLake**:
      - Open a notebook in your Databricks workspace.
      - Copy the Azure Blob Filesystem (ABFS) path from your Fabric lakehouse properties.
      - Use this path in your Databricks notebook to read and write data.

      ```python
      oneLakePath = 'abfss://myWorkspace@onelake.dfs.fabric.microsoft.com/myLakehouse.lakehouse/Files/'
      ```

   - **Load Data**: Load data from your existing data sources into a DataFrame in Databricks.

      ```python
      dataDF = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("path_to_your_data.csv")
      ```

   - **Process Data**: Filter, transform, or prepare your data as needed.

      ```python
      processedDF = dataDF.filter(dataDF['column_name'] < value)
      ```

   - **Write Data to OneLake**: Write the processed data back to your Fabric lakehouse.

      ```python
      processedDF.write.format("csv").option("header", "true").mode("overwrite").csv(oneLakePath)
      ```

   - **Verify Data**: Read the data back from OneLake to ensure it was written correctly.

      ```python
      lakehouseRead = spark.read.format('csv').option("header", "true").load(oneLakePath)
      display(lakehouseRead.limit(10))
      ```

4. Visualize Data in Power BI
   - **Connect Power BI**: 
      - Use Power BI in Microsoft Fabric to connect directly to your OneLake data.
   - **Create Reports**: 
      - Build and share reports based on the data processed in Azure Databricks.
