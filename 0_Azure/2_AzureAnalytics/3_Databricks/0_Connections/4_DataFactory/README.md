# Connecting to Azure Data Factory

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
    subgraph DataFactoryIntegration
        DF1[Create Data Factory] --> DF2[Create Pipeline]
        DF2 --> DF3[Create Linked Service to Databricks]
        DF3 --> DF4[Create Databricks Notebook Activity]
        DF4 --> DF5[Trigger and Monitor Pipeline]
    end
    Setup --> Connectivity --> Visualization --> DataFactoryIntegration
```

1. Create an Azure Databricks Workspace
    - **Go to the Azure Portal**: Navigate to the Azure portal and create a new Databricks workspace.
    - **Create a Cluster**: In the Databricks workspace, create a new cluster. Ensure that you enable Azure Data Lake Storage (ADLS) credential passthrough in the advanced options for authentication.

2. Create an Azure Data Factory
    - **Go to the Azure Portal**: Navigate to the Azure portal and create a new Data Factory.
    - **Create a Pipeline**: In the Data Factory, create a new pipeline.

3. Create a Linked Service to Azure Databricks
    - **Navigate to Manage Tab**: In Azure Data Factory, switch to the Manage tab on the left panel.
    - **Create Linked Service**: Select Linked services under Connections, and then select + New.
    - **Select Azure Databricks**: In the New linked service window, select Compute > Azure Databricks, and then select Continue.
    - **Configure Linked Service**: Complete the required fields:
    - **Name**: Enter a name for the linked service.
    - **Cluster URL**: Enter the URL of your Databricks cluster.
    - **Access Token**: Enter the access token for your Databricks workspace.
    - **Select Cluster**: Choose the cluster you created earlier.
    **Test Connection**: Click on Test connection to ensure the settings are correct, then click Create.

4. Create a Databricks Notebook Activity in the Pipeline
    - **Add Activity**: In the pipeline, add a new Databricks Notebook activity.
    - **Configure Activity**: Set up the activity by selecting the linked service you created earlier.
    - **Select Notebook**: Choose the notebook you want to run in Databricks.
    - **Set Parameters**: If needed, set any parameters required by the notebook.

5. Trigger and Monitor the Pipeline
    - **Trigger Pipeline**: Set up a trigger to run the pipeline manually or on a schedule.
    - **Monitor Pipeline**: Use the Monitor tab in Azure Data Factory to monitor the pipeline execution and check for any errors.


