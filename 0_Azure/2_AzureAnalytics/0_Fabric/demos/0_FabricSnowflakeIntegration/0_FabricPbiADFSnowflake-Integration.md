#  Microsoft Fabric for Power BI and Azure Data Factory (ADF) with a focus on Snowflake integration 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

## Wiki 

- [Frequently asked questions for Mirroring Snowflake in Microsoft Fabric (Preview)](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/snowflake-mirroring-faq#can-snowflake-mirroring-be-accessed-through-the-power-bi-gateway-or-behind-a-firewall--)

## Content 

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>
    
- [Wiki](#wiki)
- [Content](#content)
- [Overview](#overview)
- [Demo](#demo)
    - [Requirements](#requirements)
    - [Hands-On Activities](#hands-on-activities)
        - [Data Integration Exercise:](#data-integration-exercise)
        - [Report Creation with Copilot:](#report-creation-with-copilot)
        - [Mirroring Setup:](#mirroring-setup)
- [Recommended Trainings](#recommended-trainings)

</details>

## Overview

Here are some key points and new features you can highlight:

> Microsoft Fabric for Power BI
1. **Copilot Integration**: Power BI now includes Copilot, which uses generative AI to help create reports and analyze data by simply describing the insights you need.
2. **Unified Platform**: Fabric brings together Power BI, Azure Synapse, and Azure Data Factory into one unified SaaS platform, making it easier for different roles to collaborate.
3. **Enhanced Data Integration**: With Data Factory in Fabric, you can unify hybrid and multicloud data estates, combining the ease of Power Query with the power of Data Factory.
4. **New Visualization Features**: Power BI has added new formatting capabilities, including dark mode support and improved visual calculations.

> Microsoft Fabric for Azure Data Factory (ADF)
1. **Data Integration**: Fabric Data Factory offers new connectors, including those for Oracle, MySQL, Google BigQuery, and Snowflake, enhancing data integration and transformation capabilities.
2. **Simplified Data Pipelines**: The new Data Factory in Fabric integrates better with the unified data platform, including Lakehouse and Data Warehouse, making data pipelines more efficient.
3. **Real-Time Data Replication**: Mirroring in Fabric allows for near real-time replication of data from various sources into OneLake, simplifying data management and analytics.

<img width="700" alt="image" src="https://github.com/user-attachments/assets/f84ae4c4-22e7-44ae-9d21-fa7976e163e4">

| **Option**                | **Description**                                                                                                                                                                                                 |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Dataflow Gen2**         | The new generation of dataflows in Microsoft Fabric, offering improved features like **shorter authoring flows, auto-save, background publishing, and better integration with data pipelines**. Primarily focuses on the **transformation** of data.                      |
| **Data pipeline**         | A series of processes that move data from one system to another, involving data ingestion, transformation, and storage to ensure data is ready for analysis or other uses. Manages the **movement** of data, including ingestion, transformation, and loading.                                       |
| **Data Factory**          | A cloud-based data integration service that allows you to **create, schedule, and manage data pipelines**, supporting various data sources and providing tools for data transformation and movement.                  |
| **Data workflow (Preview)** | Uses **Apache Airflow to create and manage data workflows**, providing a cloud-based platform for developing, scheduling, and monitoring data workflows, making it easier to handle complex data processes.           |
| **Copy job (Preview)**    | Automates **data loading from Amazon S3 to Amazon Redshift**, detecting new files in specified paths and loading them automatically to simplify the data ingestion process.                                          |
| **API for GraphQL (Preview)** | Allows interaction with data using GraphQL, **a query language for APIs**, enabling **efficient querying of multiple data sources** and providing a flexible way to fetch data in a single request.                     |

> Impact on Snowflake Usage
1. **Mirroring**: Fabric's Mirroring feature allows you to replicate data from Snowflake into OneLake in near real-time, reducing the need for complex ETL pipelines.
2. **Unified Analytics**: With data mirrored into OneLake, you can leverage Fabric's analytics tools, such as Spark, notebooks, and Power BI, to analyze and visualize data seamlessly.
3. **Cost and Latency**: Mirroring provides a low-cost and low-latency solution for data replication, making it easier to keep your data up-to-date and accessible for analytics.

## Demo

### Requirements

| **Category** | **Requirements** |
|--------------|------------------|
| **General Requirements** | - Active Microsoft Fabric subscription  <br> - Fabric capacity (measured in Capacity Units or CUs) |
| **Data Integration Exercise** | - Permissions to access and manage Data Factory within Microsoft Fabric  <br> - Credentials and connection details for data sources (e.g., Snowflake, Oracle, MySQL)  <br> - Configuration details for the destination (e.g., Azure Data Lake, OneLake) |
| **Report Creation with Copilot** | - Permissions to access and use Power BI within Microsoft Fabric  <br> - Copilot enabled in Power BI settings  <br> - A compatible workspace with write access assigned to a Copilot-enabled capacity (F64 or higher) or a Power BI Premium capacity (P1 or higher), [more information here](https://learn.microsoft.com/en-us/power-bi/create-reports/copilot-create-report-service) |
| **Mirroring Setup** | - Permissions to access and manage the Fabric service within the Azure portal  <br> - Connection details for Snowflake database (e.g., account name, username, password)  <br> - Configuration details for OneLake as the destination for mirrored data  <br> - Ability to choose specific tables for mirroring and control over the initiation and suspension of mirroring processes, [more information here](https://eng.ms/docs/cloud-ai-platform/azure-data/azure-data-intelligence-platform/synapse-dw/fabric-dw-top-level-service/trident-dw/clientexperiences/mirroring/overview) |
| **Additional Considerations** | - User permissions for accessing and managing services and resources  <br> - Compliance with organizational security and compliance policies |

### Hands-On Activities

#### **Data Integration Exercise**: 

> Set up a data pipeline using Data Factory in Fabric to integrate data from multiple sources, including Snowflake

1. **Access Data Factory within Fabric**:
    - Log in to the Microsoft Fabric portal.
    - Navigate to the Data Factory service within Fabric.
      
    <img width="200" alt="image" src="https://github.com/user-attachments/assets/3b57f63c-bb09-4f11-9012-06f59dfa4893">

2. **Create a New Data Pipeline**:
    - Click on the “Create pipeline” button.
    
    <img width="400" alt="image" src="https://github.com/user-attachments/assets/52cfe364-9022-47b0-a76d-33f78d85144e">

3. **Add Data Sources**:
    - Click on the “Activity” tab.
    - Add a Copy Data activity to the pipeline.
    - Select the type of data source (e.g., Snowflake, Oracle, MySQL).
    - Configure the connection settings for each data source (e.g., server name, database name, credentials).
    
    <img width="400" alt="image" src="https://github.com/user-attachments/assets/8032577f-b415-40a9-9610-9046dbae7870">

4. **Configure Data Integration**:
    - Add a sink to load the data into the desired destination (e.g., Azure Data Lake, OneLake).
    <img width="400" alt="image" src="https://github.com/user-attachments/assets/4fbaa9dc-8cb9-4d3f-99c1-88fe309362af">

5. **Run and Monitor the Pipeline**:
    - Save and publish the pipeline.
    - Trigger the pipeline to run.
    - Monitor the pipeline execution for any errors or issues.
    

#### **Report Creation with Copilot**: 

> Use Copilot in Power BI to generate reports and visualizations based on specific business questions.

1. **Access Power BI within Fabric:**
    - Open Power BI within the Microsoft Fabric portal.
    
    <img width="200" alt="image" src="https://github.com/user-attachments/assets/6145fce7-7e4d-4ada-882f-5d842d617ca8">

2. **Enable Copilot:**
   - Ensure that Copilot is enabled in your Power BI settings:
      1. **Sign in to Microsoft Fabric** using your admin account credentials.
      2. **Navigate to the Admin Portal**:
         - Select **Fabric settings** from the menu.
         - Choose **Admin portal**.
      
      3. **Enable Copilot**:
         - In the Admin portal, select **Tenant settings**.
         - Use the search feature to locate the **Copilot and Azure OpenAI Service (preview)** settings.
         - Toggle the switch to **Enable Copilot in Fabric**.
         - Click **Apply** to save your changes.
      
      4. **Verify Access**:
         - Ensure that your workspace is in either **Premium Power BI (P1 and above)** or **paid Fabric (F64 and above)** capacity.

3. **Create a New Report:**
    - Click on “Create” and select “Report”.
    
    <img width="300" alt="image" src="https://github.com/user-attachments/assets/572bfb26-9154-4ae9-99f7-24221fb9559e">

    - Choose the source 
    
    <img width="400" alt="image" src="https://github.com/user-attachments/assets/88fb050c-3919-4fb9-b27e-df590d546ab9">

4. **Use Copilot for Insights:**
    - In the report canvas, click on the Copilot icon.
    - Describe the insights or visualizations you need (e.g., “Show me sales trends over the last year”).
    - Copilot will generate the appropriate visuals and insights based on your description.
      
    <img width="600" alt="image" src="https://github.com/user-attachments/assets/809558d4-e78b-45c8-9c46-e658c77b1ce8">

5. **Customize the Report:**
    - Adjust the visuals as needed (e.g., change chart types, add filters).
    - Add additional visuals or data points to enhance the report.
6. **Save and Share the Report:**
   - Save the report to your workspace.
   - Share the report with stakeholders or publish it to the Power BI Service.

#### **Mirroring Setup**: 

> Demonstrate how to set up Mirroring for a Snowflake database and explore the replicated data in OneLake.

1. **Access Fabric**:
   - Log in to the Azure portal.
   - Navigate to the Fabric service.

2. **Set Up Mirroring**:
    - Enable Mirroring
        1. Open Microsoft Fabric: Log in to your Microsoft Fabric account.
        2. **Access Tenant Settings**:
           - Navigate to the **Admin Portal**.
           - In the Admin Portal, go to **Tenant Settings**.
        3. Expand Mirroring (Preview): In the Tenant Settings, find and expand the **Mirroring (Preview)** section.
        4. Enable Mirroring: Toggle the **Mirroring (Preview)** switch to **On**.
        5. Optional: Specific Security Groups: If you want to enable Mirroring for specific users, use the **Specific Security Groups** option to select the users or groups.
        6. Save Settings: After enabling Mirroring, make sure to **Save** your settings.
     
        <img width="600" alt="image" src="https://github.com/user-attachments/assets/e721b814-245b-4d07-9774-aec125e821dd">

        <img width="600" alt="image" src="https://github.com/user-attachments/assets/f8a71081-02c0-48aa-a675-5c2ebff03040">
        
        <p float="left">
          <img src="https://github.com/user-attachments/assets/63376753-d650-4b1c-a6dc-6f2cbdcf6ff7" width="200" height="300" />
          <img src="https://github.com/user-attachments/assets/102c2542-6ac7-4df4-a028-8876bbdc2190" width="300" height="300" />
        </p>

    - Set Up Mirroring: [click here for more details](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/snowflake-tutorial)
       - In Fabric, go to the **Mirroring** section.
       - Click on **Create Mirroring**.

        <img width="600" alt="image" src="https://github.com/user-attachments/assets/4ec17f1a-5395-4ef2-9856-33ca2eda6410">

3. **Configure Snowflake Connection**:
   - Select Snowflake as the source.
   - Enter the connection details for your Snowflake database (e.g., account name, username, password).

        <img width="600" alt="image" src="https://github.com/user-attachments/assets/32633b95-a79e-4550-9460-43b64c4cb3cc">

4. **Select Data to Mirror**:
   - Choose the tables or schemas you want to replicate.
   - Configure any transformation or filtering rules if needed.

5. **Configure OneLake as Destination**:
   - Select OneLake as the destination for the mirrored data.
   - Configure the connection settings for OneLake.

6. **Start Mirroring**:
   - Save and start the mirroring process.
   - Monitor the mirroring status to ensure data is being replicated correctly.

7. **Explore Replicated Data**:
   - Once mirroring is complete, access OneLake.
   - Use tools like Power BI or Azure Synapse to explore and analyze the replicated data.

## Recommended Trainings 
- [Use Data Factory pipelines in Microsoft Fabric](https://learn.microsoft.com/en-us/training/modules/use-data-factory-pipelines-fabric/): This module covers how to describe pipeline capabilities, use the Copy Data activity, create pipelines based on predefined templates, and run and monitor pipelines.
- [Extend data insights with Copilot in Power BI](https://learn.microsoft.com/en-us/training/modules/power-bi-copilot/): This module teaches you how to create reports and summaries using Copilot in Power BI, enhancing your data interaction and report creation experience.
- [Configure a Microsoft Fabric mirrored database from Snowflake](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/snowflake-tutorial): This tutorial guides you through configuring a mirrored database from Snowflake, including setting up a secure connection, starting the mirroring process, and exploring the mirrored data in OneLake.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
