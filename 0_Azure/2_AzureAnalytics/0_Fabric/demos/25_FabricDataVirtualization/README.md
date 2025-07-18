# Fabric: Data Virtualization Capabilities

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

Data Virtualization can be leveraged either through a dedicated tool or an integrated approach:

> `Dedicated Tool`: Traditional data virtualization tools (e.g., Denodo, Informatica, etc) are specifically designed for data virtualization. <br/>
> `Integrated Approach`: Microsoft Fabric provides data virtualization capabilities by integrating a range of services, each specializing in areas such as data integration (Azure Data Factory), storage (Data Lake Storage), querying (Azure Synapse Analytics), and visualization (Power Bi).

> Considerations: <br/>
> - **Scalability**: Ensure your ingestion process can handle varying data volumes and can scale up or down as needed. <br/>
> - **Latency**: Consider the acceptable latency for your use case. Real-time ingestion requires low latency, while batch ingestion can tolerate higher latency. <br/>
> - **Data Quality**: Implement data validation and cleansing during the ingestion process to ensure the quality of the ingested data. <br/>
> - **Security**: Secure data in transit and at rest using encryption and access control mechanisms.

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [What is Microsoft Fabric?](https://learn.microsoft.com/en-us/fabric/get-started/microsoft-fabric-overview)
- [Introducing Microsoft Fabric: Data analytics for the era of AI](https://azure.microsoft.com/en-us/blog/introducing-microsoft-fabric-data-analytics-for-the-era-of-ai/)
- [Step-by-Step Tutorial: Building ETLs with Microsoft Fabric](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/step-by-step-tutorial-building-etls-with-microsoft-fabric/3885183)
- [What is Data Science in Microsoft Fabric?](https://learn.microsoft.com/en-us/fabric/data-science/data-science-overview)
- [Microsoft Fabric security white paper](https://learn.microsoft.com/en-us/fabric/security/white-paper-landing-page)
- [Microsoft Fabric security white paper - Git repo](https://github.com/MicrosoftDocs/fabric-docs/blob/main/docs/security/white-paper-landing-page.md)
- [Getting from Azure Data Factory to Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/compare-fabric-data-factory-and-azure-data-factory)
- [Data virtualization with Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/data-virtualization-overview?view=azuresql&tabs=managed-identity)
- [Data virtualization now generally available in Azure SQL Managed Instance](https://techcommunity.microsoft.com/blog/azuresqlblog/data-virtualization-now-generally-available-in-azure-sql-managed-instance/3624292)
- [Announcing Data virtualization with Azure SQL Managed Instance – preview](https://techcommunity.microsoft.com/blog/azuresqlblog/announcing-data-virtualization-with-azure-sql-managed-instance-%E2%80%93-preview/3250347)
- [What are shortcuts?](https://learn.microsoft.com/en-us/fabric/onelake/onelake-shortcuts#what-are-shortcuts)
- [Create an Azure Data Lake Storage Gen2 shortcut](https://learn.microsoft.com/en-us/fabric/onelake/create-adls-shortcut)
- [Azure Data Lake Storage hierarchical namespace](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-namespace)
- [Overview of Copilot for Power BI](https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-introduction#copilot-requirements)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [What is Data Virtualization?](#what-is-data-virtualization)
    - [Key Features & Fabric Components](#key-features--fabric-components)
    - [Benefits:](#benefits)
    - [Data Ingestion](#data-ingestion)
        - [Key Components of Data Ingestion](#key-components-of-data-ingestion)
        - [Examples of Data Ingestion](#examples-of-data-ingestion)
    - [Data Integration](#data-integration)
        - [Key Components of Data Integration](#key-components-of-data-integration)
        - [Examples of Data Integration](#examples-of-data-integration)
    - [Example of how DV looks in Azure SQL MI](#example-of-how-dv-looks-in-azure-sql-mi)
- [Demo](#demo)
    - [Step 1: Set Up Your Environment](#step-1-set-up-your-environment)
    - [Step 2: Ingest Data & Data Integration](#step-2-ingest-data--data-integration)
    - [Step 3: Query and Analyze Data](#step-3-query-and-analyze-data)

</details>

## What is Data Virtualization?

> Data virtualization is a data management approach that `allows applications to retrieve and manipulate data without needing to know the technical details about the data, such as its format or physical location`.
> Is `commonly used in business intelligence, service-oriented architecture, cloud computing, and master data management`. It helps organizations `make data-driven decisions by providing a comprehensive and up-to-date view of their data`.

###  Key Features & Fabric Components

| Key Features | Fabric Component |
| --- | --- |
| **Unified Data Access**: Provides a single access layer for data from multiple sources, such as databases, data warehouses, and cloud services | - **OneLake**: Acts as a unified data lake, enabling seamless access to data from various sources. Centralizes data storage, making it easier to access and manage data from different sources. <br/> - **Azure Synapse Analytics**: Allows querying across different data sources without moving the data, providing a virtualized view. Offers a unified analytics platform that integrates big data and data warehousing, allowing for seamless data querying and analysis. |
| **Real-Time Data Integration**: Allows real-time access to data without moving it from its original location | - **Shortcuts and Mirroring (Data Factory)**: Facilitate real-time data integration and transformation, allowing you to work with data in its original location. <br/> - **Real-Time Intelligence**: Supports real-time analytics and insights, enhancing decision-making processes. <br/> - **Azure Stream Analytics**: Processes real-time data streams for immediate insights. Provides real-time data processing capabilities, enabling you to analyze data as it arrives. |
| **Flexibility and Efficiency**: Users can access and combine data quickly and cost-effectively, accelerating data delivery and decision-making | **Microsoft Fabric**: Provides a comprehensive data management and analytics solution. <br/> - **Power BI**: Connects to various data sources to create interactive reports and dashboards, enhancing data-driven decision-making. Enhances data visualization and reporting, allowing users to create interactive and insightful dashboards. <br/> - **Azure Data Factory**: Enables flexible data integration and transformation workflows. |

<p align="center">
  <img src="https://github.com/user-attachments/assets/44f2b7dc-ea99-4ea3-b4ec-90654cb434c1" alt="image" width="750">
</p>

###  Benefits:
- **Reduced Data Movement**: Minimizes the need to move data, reducing the risk of errors and ensuring the most current data is used.
- **Simplified Data Integration**: Makes it easier to integrate data from various sources, providing a unified view of the data.
- **Enhanced Data Governance**: Centralizes data security and governance, making it easier to manage and enforce policies.

### Data Ingestion

**Data ingestion** is the process of `collecting and importing data` from various sources into a centralized storage system, such as a data warehouse or data lake. This process involves several steps and can be performed using different tools and techniques depending on the source and type of data.

#### Key Components of Data Ingestion

1. **Data Sources**:
   - **Structured Data**: Data from relational databases, CSV files, spreadsheets, etc.
   - **Semi-Structured Data**: Data from JSON, XML files, etc.
   - **Unstructured Data**: Data from text files, images, videos, etc.
   - **Streaming Data**: Real-time data from IoT devices, logs, social media feeds, etc.
2. **Ingestion Methods**:
   - **Batch Ingestion**: Collecting and processing data in large chunks at scheduled intervals. Suitable for scenarios where real-time processing is not required.
   - **Real-Time Ingestion**: Continuously collecting and processing data as it arrives. Suitable for scenarios requiring immediate data processing and analysis.
3. **Ingestion Tools**:
   - **Azure Data Factory (ADF)**: A cloud-based data integration service that allows you to create, schedule, and orchestrate data pipelines. It supports a wide range of data sources and destinations.
   - **Azure Stream Analytics**: A real-time analytics service designed to process and analyze streaming data from various sources.
   - **Azure Event Hubs**: A big data streaming platform and event ingestion service capable of receiving and processing millions of events per second.
   - **Azure IoT Hub**: A managed service that enables bi-directional communication between IoT applications and the devices it manages.

#### Examples of Data Ingestion

| Method | Steps |
|--------|-------|
| **Uploading CSV Files to Azure Data Lake Storage (ADLS)** | 1. Prepare your CSV files with the data you want to ingest.<br>2. Use Azure Storage Explorer or Azure portal to upload the CSV files to a designated container in ADLS.<br>3. Configure access control and permissions to ensure the data is secure and accessible to authorized users. |
| **Using Azure Data Factory to Copy Data from On-Premises Databases to a Cloud Data Warehouse** | 1. Set up a self-hosted integration runtime in Azure Data Factory to connect to your on-premises database.<br>2. Create a pipeline in Azure Data Factory with a copy activity to transfer data from the on-premises database to the cloud data warehouse.<br>3. Schedule the pipeline to run at regular intervals or trigger it based on specific events. |
| **Streaming Data from IoT Devices into a Data Lake** | 1. Set up an Azure IoT Hub to collect data from IoT devices.<br>2. Use Azure Stream Analytics to process the streaming data in real-time.<br>3. Output the processed data to Azure Data Lake Storage for further analysis and storage. |

### Data Integration

**Data integration** involves `combining data` from different sources and providing a unified view. This process often includes transforming, cleaning, and enriching the data to ensure consistency and usability. Data integration is crucial for creating a cohesive dataset that can be used for analysis, reporting, and decision-making.

#### Key Components of Data Integration

1. **Data Sources**:
   - **Structured Data**: Data from relational databases, CSV files, spreadsheets, etc.
   - **Semi-Structured Data**: Data from JSON, XML files, etc.
   - **Unstructured Data**: Data from text files, images, videos, etc.
   - **Streaming Data**: Real-time data from IoT devices, logs, social media feeds, etc.
2. **Integration Methods**:
   - **Batch Integration**: Combining data at scheduled intervals.
   - **Real-Time Integration**: Continuously combining and processing data as it arrives.
3. **Integration Tools**:
   - **Azure Data Factory (ADF)**: For batch and real-time data integration.
   - **Azure Synapse Analytics**: For data warehousing and big data analytics.
   - **Azure Stream Analytics**: For real-time data processing.
   - **Azure Data Lake Storage (ADLS)**: For storing integrated data.
   - **Power BI**: For data visualization and reporting.

#### Examples of Data Integration

| Method | Steps |
|--------|-------|
| **Combining Sales Data from Multiple Regions into a Single Dataset for Analysis** | 1. Use Azure Data Factory to create pipelines that extract sales data from different regional databases.<br>2. Transform the data to ensure consistency (e.g., currency conversion, date format standardization).<br>3. Load the transformed data into a central data warehouse or data lake for unified analysis. |
| **Using Shortcuts and Mirroring to Enable Real-Time Data Integration** | 1. Create shortcuts in Microsoft Fabric to link data from different sources (e.g., ADLS, S3, GCS).<br>2. Use mirroring to synchronize data between the source and the target in real-time.<br>3. Access and analyze the integrated data in real-time using tools like Azure Synapse Analytics. |
| **Setting Up Real-Time Intelligence to Process and Analyze Streaming Data from Various Sources** | 1. Set up Azure IoT Hub or Azure Event Hubs to collect streaming data from various sources.<br>2. Use Azure Stream Analytics to process the streaming data in real-time.<br>3. Output the processed data to Azure Data Lake Storage or Azure Synapse Analytics for further analysis and visualization. |

### Example of how DV looks in Azure SQL MI

> Querying Azure Data Lake Storage files from Azure SQL Managed Instance via T-SQL queries:

<img width="450" alt="image" src="https://github.com/user-attachments/assets/af5a4c16-170c-4670-a6ca-b34df9312b76" />

## Demo 

> This setup demo how to use Microsoft Fabric and its integrated services to provide a comprehensive data management and analytics solution, achieving data virtualization.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/3096fe37-96c9-4d35-a0ff-6c3041be256f">

### Step 1: Set Up Your Environment

1. **Create a Microsoft Fabric Workspace**:
   - Sign in to the [Microsoft Fabric portal](https://app.fabric.microsoft.com/).
   - Navigate to `Workspaces` > `New Workspace`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/aac646ef-6ead-4f57-a1c4-7f525852f312" />

   - Fill out the workspace details and select `Apply`.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/199e60ee-03c5-4d6f-9fad-74724ffe20a3" />

2. **Create a Data Warehouse and Lakehouse**: Click [here to see more information about these types of data architecture](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/17_Overview.md#lakehouse--data-warehouse)
   - In your workspace, select `New Item` > `Warehouse` to create a Data Warehouse `-> structured`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/89e412f2-3c15-4de8-9272-ac7cc62cc938" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/dc5694be-a571-450c-aecd-2cff77859142" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/ccc18717-98a8-41ff-b6f0-53b99ab3c2aa" />

   - Similarly, select `New Item` > `Lakehouse` to create a Lakehouse `-> both structured + unstructured`.
  
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/5ab352bb-1f94-404a-880d-d2c8c2a9ef1d" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/5967d5cb-09e2-4190-bc66-e08354235279" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/128d6f24-fa01-4c8a-9456-71ff6102befa" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/d46edb62-619e-4def-bcd1-e43242159cdd" />

### Step 2: Ingest Data & Data Integration

> Data ingestion (getting data into your system): <br/> 
> - Uploading CSV files to Azure Data Lake Storage (ADLS). <br/>
> - Using Azure Data Factory to copy data from on-premises databases to a cloud data warehouse. <br/>
> - Streaming data from IoT devices into a data lake. <br/>
> Data integration (combining and processing data from different sources in real-time): <br/>
> - Combining sales data from multiple regions into a single dataset for analysis. <br/>
> - Using shortcuts and mirroring to enable real-time data integration, allowing data from different sources to be accessed and analyzed together. <br/>
> - Setting up real-time intelligence to process and analyze streaming data from various sources.

```mermaid
graph LR
    A[Upload CSV Files to ADLS Gen2] --> B[ADLS Gen2 Storage]
    B --> C[Create Shortcuts]
    C--> D[Access Data ]
    D --> E[Analyze Data]

    subgraph Azure
        B
    end

    subgraph Microsoft Fabric
        C
        D
        E
    end
```

> Data ingestion by Shortcuts:

<p align="center">
  <img src="https://github.com/user-attachments/assets/067d6624-483a-48be-a881-a03645eca4f5" alt="image" width="650">
</p>

1. **Upload Data to Azure Data Lake Storage (ADLS)**:

   - Upload your sample datasets (e.g., Sale-SalesOrderHeader, Sales-SalesOrderDetail, health-samples) to ADLS Gen2.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/d9bcd97c-5b54-4582-b4a7-5e1a5e13163f" />

> [!IMPORTANT]
> Use Shortcuts and Mirroring to enable real-time data integration. Click [here to see a quick guide](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/17_Overview.md#shortcuts--mirroring)

> [!NOTE]
> The ability to create shortcuts in Microsoft Fabric is available starting from the F64 SKU and higher. This feature allows you to create symbolic links to data stored in external storage systems like ADLS Gen 2, S3, or GCS, enabling in-place reads and writes without copying the data. Click [here for more information about it](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features). <br/>
> Please ensure that Hierarchical Namespaces are enabled on your ADLS Gen 2 storage account.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/f9fdf6a3-6617-48ba-9ef1-4c6af08732af" />

> Once completed:
<img width="550" alt="image" src="https://github.com/user-attachments/assets/b2693d59-4644-4d61-a297-5b54e1053aff" />

2. **Create Shortcuts in the Lakehouse**:

   - In the Lakehouse explorer, hover over the `Tables` folder and select `New Shortcut`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/32046cb7-9cc1-4a49-bcb3-0fff6fbbfb8d" />

   - Choose `ADLS Gen2` as the external source and provide the necessary details to link your data.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/5dba174a-e934-4374-8a12-5478ebd1363c" />

    - Use an existing connection or create one to your `ADLS Gen2`:

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/a299f44e-66bb-48eb-a33d-98c8990c8cea" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/494478d1-6cb2-4035-adbb-b0d3a73012cd" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/a1428ddc-94ea-47c1-bedc-d8ee17f896b4" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/8bc5ce3e-6d78-4352-a9f0-600e8692b325" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa2d9226-ad75-4ddc-9069-d16a9bb2a6e3" />

> Set Up Data Integration by Data Factory

1. **Create a Data Pipeline in Azure Data Factory**:
   - Please create a subfolder in the lakehouse to store the information extracted from the ADLS:
   
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/df62af48-c3a4-4398-86b4-4d56d2f13c0b" />

   - Navigate to **Data Factory** in your Microsoft Fabric workspace.
   - Create a new data pipeline and use the **Copy Data** tool to configure your data source and destination.
   - Select your sample dataset from ADLS as the source and your Data Warehouse as the destination.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/84c47d9a-33ab-4b8e-a46c-0d26183b0c96" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/cb07c58c-02e4-462a-9a4e-37b769b812bd" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/c1037c94-92b2-4220-ba0a-0f3fd8353d23" />

     | Source | Destination |
     | --- | --- |
     | <img width="750" alt="image" src="https://github.com/user-attachments/assets/8b5c66e0-5e51-4927-ae7d-40374be9855a" /> | <img width="750" alt="image" src="https://github.com/user-attachments/assets/9f52c7c9-6c77-474b-9422-b7309f4d96a4" /> | 

   - Remember to `Save`, and `Validate, Run`:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/41920d70-af0b-4842-829e-71db5357e0aa" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/0488baf0-63ba-46d2-ad37-e491f94f5d3c" />

### Step 3: Query and Analyze Data

1. To generate reports, we need to build tables from the CSV files to create the semantic model. We can achieve this either through the shortcut or by using the extracted information. In this scenario, let's assume the shortcut represents the gold layer, meaning all the data in CSV format is ready for use. I will proceed to load that information into tables.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/4b782db1-e2c1-411a-9412-0b65e0b2119b" />

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/0c628ef5-15a0-4de9-b717-f2139df8fa3a" />

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/6271e569-ed04-4c67-a332-d2d7ad614fe4">

    > At this point, you will find the following objects in your workspace:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/c213242b-2cda-4ecc-92dd-1b3acdf153ea" />

2. **Create Interactive Reports with Power BI**:
   - To create interactive dashboards and reports for data visualization, connect Power BI to your semantic model. Click on `...` on your semantic model.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/fdc1de90-1d9a-4021-9c47-1eacae2fe2a0" />
   
   - We can leverage `Copilot` capabilities to automatically generate a report based on our semantic model and further edit it.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/df36962c-b8c2-40e3-b549-74cb067624ec" />

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/d9156fbc-29d1-4abe-a73b-68263f4d0d58" />

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
