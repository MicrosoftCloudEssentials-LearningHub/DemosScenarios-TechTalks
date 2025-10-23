# Azure Cosmos DB Partition Merge: Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

- [Merge partitions in Azure Cosmos DB (preview)](https://learn.microsoft.com/en-us/azure/cosmos-db/merge?tabs=azure-powershell%2Cnosql)
- [Redistribute throughput across partitions (preview)](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/distribute-throughput-across-partitions?tabs=azure-powershell%2Cnosql)
- [Provision an Azure Cosmos DB account with continuous backup and point in time restore](https://learn.microsoft.com/en-us/azure/cosmos-db/provision-account-continuous-backup)
- [Online backup and on-demand data restore in Azure Cosmos DB](https://bing.com/search?q=workaround+for+switching+Azure+Cosmos+DB+from+continuous+mode+to+periodic+mode)
- [Frequently asked questions about continuous backup](https://learn.microsoft.com/en-us/azure/cosmos-db/continuous-backup-restore-frequently-asked-questions)
- [Migrate data using the desktop data migration tool](https://learn.microsoft.com/en-us/azure/cosmos-db/how-to-migrate-desktop-tool)
- [Relocate an Azure Cosmos DB NoSQL account to another region](https://learn.microsoft.com/en-us/azure/operational-excellence/relocation-cosmos-db)
- [An Introduction to the new Data Migration Tool for Azure Cosmos DB](https://learn.microsoft.com/en-us/shows/azure-cosmos-db-conf-2023/an-introduction-to-the-new-data-migration-tool-for-azure-cosmos-db)
- [Live Migrate Azure Cosmos DB SQL API Containers data with Spark Connector and Azure Databricks](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/cosmos/azure-cosmos-spark_3_2-12/Samples/DatabricksLiveContainerMigration)


## Requirements 

To be eligible for the partition merge preview in Azure Cosmos DB, your account must meet the following criteria:

| **Requirement** | **Details** | **Why This Matters** |
|-----------------|-------------|----------------------|
| **API Version** | - API for NoSQL or MongoDB with version 3.6 or higher | Newer API versions include optimizations and features necessary for the partition merge functionality. |
| **Provisioned Throughput** | - Must use provisioned throughput (manual or autoscale) <br> - Not applicable to serverless accounts | Provisioned throughput ensures predictable performance and is required for managing partition merges effectively. |
| **SDK Compatibility** | - .NET SDK version 3.27.0 or higher <br> - Java SDK version 4.42.0 or higher <br> - Azure Cosmos DB Spark connector version 4.18.0 or higher | Supported SDK versions include necessary updates and compatibility for partition merge operations. |
| **Throughput and Storage Conditions** | - Current RU/s per physical partition is less than 3000 RU/s <br> - Current average storage in GB per physical partition is less than 20 GB | These conditions ensure that partitions are not overloaded, which is crucial for a smooth merge process. |
| **Backup Mode** | - Must not be using the Point-in-Time Restore (PITR) feature | PITR can interfere with the partition merge process, so it must be disabled to proceed. |

## How to Pass the Eligibility Check

1. **Update SDKs**: 
   - Ensure your applications are using the supported SDK versions. Update them if necessary.
   - **Steps**:
     - Check your current SDK version in your project dependencies.
     - Update to the latest supported version using your package manager (e.g., NuGet for .NET, Maven for Java).
2. **Monitor Throughput and Storage**: 
   - Regularly check your containers to ensure they meet the throughput and storage conditions.
   - **Steps**:
     - Use the Azure portal to monitor RU/s and storage metrics.
     - Adjust throughput settings if necessary to stay within the required limits.
3. **Check Backup Mode**:
   - Navigate to the **Backup & Restore** section in the Azure portal for your Cosmos DB account.
   - Ensure that your account is not configured for Point-in-Time Restore (PITR). 
   - **Steps**:
     - Go to your Cosmos DB account in the Azure portal.
     - Select **Backup & Restore**.
     - Verify the backup mode and disable PITR if necessary.
4. **Run the Eligibility Check**: To check the eligibility for the partition merge preview in Azure Cosmos DB, follow these steps:
   - Open the Azure portal and go to your Azure Cosmos DB account overview page.
   - From the overview page, navigate to **Diagnose and solve problems**.
   - Under the Diagnose and solve problems section, choose **Throughput and Scaling**.

      <img width="450" alt="image" src="https://github.com/user-attachments/assets/e11dd2f4-5caa-4b9c-94ab-cec80345f0e1">

   - Click on **Partition Merge** and run the **Check eligibility for partition merge preview** diagnostic.
   - **Steps**:
     - Follow the on-screen instructions to complete the diagnostic.
     - Review the results and take any recommended actions.
       
       <img width="450" alt="image" src="https://github.com/user-attachments/assets/93301f2d-bdab-4f02-a762-cedef8414a84">
   
## Troubleshooting Guide: Additional Steps if Fails

### if Backup Policy Needs Adjustment

<p float="left">
  <img src="https://github.com/user-attachments/assets/f0a5a6d3-08dd-4c76-a568-392bd9776222" width="550" height="300" />
  <img src="https://github.com/user-attachments/assets/7660f3f9-350b-4982-9542-281e206b07d4" width="450" height="300" />
</p>

> Unfortunately, once you migrate an Azure Cosmos DB account to continuous backup mode (either 30 days or 7 days), it is not possible to revert it back to periodic backup mode. This migration is a one-way process and cannot be undone. <br/>

> [!Note]
> You would have to create a new Azure Cosmos DB account with the periodic backup policy and migrate your data to this new account.

Workaround - Create a New Account with Periodic Backups: 

1. **Create a New Cosmos DB Account**:
   - Navigate to the Azure portal and select **Create a resource**.
   - Search for **Azure Cosmos DB** and select **Create**.
   - Choose the **API** you want to use (e.g., Core (SQL), MongoDB, etc.).
   - In the **Backup policy** section, select **Periodic**.
   - Complete the rest of the setup and create the account.

     <img width="955" alt="image" src="https://github.com/user-attachments/assets/6c190ae6-21cd-4256-b5f4-2a3507ea2843">

2. **Migrate Data to the New Account**:
   - Use Azure Data Migration tools, Azure Data Factory or scripts to transfer your data from the existing account to the new one.
   - Ensure that all data and configurations are correctly migrated.
  
| **Method**                | **Steps**                                                                                     | **Suitable For**                                                                 |
|---------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Data Migration Tool**   | 1. **Install the Tool**: Download and install from GitHub.<br/>2. **Prepare Databases**: Set up source and target databases.<br/>3. **Configure Tool**: Set up source and target connections.<br/>4. **Perform Migration**: Select data and start migration.<br/>5. **Verify Data**: Check data integrity.<br/>6. **Update Applications**: Update connection strings and test applications. | Small to medium-sized migrations, one-time migrations, and scenarios where a simple tool is sufficient. |
| **Azure Data Factory**    | 1. **Create Data Factory**: Set up a new Data Factory instance in the Azure portal.<br/>2. **Set Up Linked Services**: Create linked services for source and target Cosmos DB accounts.<br/>3. **Create Pipeline**: Add a "Copy Data" activity.<br/>4. **Configure Source**: Set up source settings.<br/>5. **Configure Sink**: Set up target settings.<br/>6. **Run Pipeline**: Validate and trigger the pipeline.<br/>7. **Monitor Migration**: Track progress using monitoring tools. | Large-scale migrations, complex data transformations, and scenarios requiring automation and scheduling. |
| **Cosmos DB Spark Connector** | 1. **Set Up Environment**: Ensure Databricks workspace and Cosmos DB accounts are ready.<br/>2. **Install Connector**: Add the Azure Cosmos DB Spark connector library to your Databricks cluster.<br/>3. **Configure Spark Session**: Set up Spark session with Cosmos DB configurations.<br/>4. **Read Data**: Use Spark DataFrame API to read data from the source Cosmos DB.<br/>5. **Write Data**: Configure target Cosmos DB and write data.<br/>6. **Monitor Migration**: Use Databricks monitoring tools to track progress. | Real-time or live migrations, large-scale data processing, and scenarios requiring integration with Databricks for advanced analytics. |

3. **Update Applications**:
   - Update your applications to point to the new Cosmos DB account.
   - Test thoroughly to ensure everything works as expected.
   - Validate the data in the new account before decommissioning the old one.

## How to Migrate Data to the New Account

### Using the Azure Data Migration tool

- Step 1: Install the Data Migration Tool
  1. **Download the Tool**:
     - Go to the [GitHub repository](https://github.com/AzureCosmosDB/data-migration-desktop-tool) and download the latest version of the desktop data migration tool.
     - Extract the files to a suitable location on your machine.
  2. **Install Prerequisites**: Ensure you have .NET 6.0 or later installed on your machine.
- Step 2: Prepare the Source and Target Databases
  1. **Source Database**: Identify the source database and container from which you want to migrate data.
  2. **Target Database**:
     - Create a new Azure Cosmos DB account if you don't have one.
     - Create a new database and container in the target account using the Azure portal, Azure CLI, or PowerShell.
- Step 3: Configure the Migration Tool
  1. **Open the Tool**: Launch the data migration tool.
  2. **Set Up Source Connection**:
     - Select the source type (e.g., Azure Cosmos DB for NoSQL, MongoDB, etc.).
     - Provide the connection details for the source database.
  3. **Set Up Target Connection**:
     - Select the target type (e.g., Azure Cosmos DB for NoSQL).
     - Provide the connection details for the target database.
- Step 4: Perform the Migration
  1. **Select Data to Migrate**: Choose the specific collections or tables you want to migrate.
  2. **Start Migration**: Initiate the migration process. The tool will transfer the data from the source to the target database.
  3. **Monitor Progress**: Keep an eye on the migration progress to ensure everything is running smoothly.
- Step 5: Verify Data Integrity
  1. **Check Data**:
     - Once the migration is complete, verify that all data has been correctly transferred to the target database.
     - Ensure that the data structure and configurations are intact.
- Step 6: Update Applications
  1. **Update Connection Strings**: Update your application’s connection strings to point to the new Cosmos DB account.
  2. **Test Applications**: Run tests to ensure that your applications are functioning correctly with the new database.

### Using Azure Data Factory

1. **Create an Azure Data Factory Instance**:
   - Go to the [Azure portal](https://portal.azure.com/).
   - Click on `Create a resource` and search for `Data Factory`.
   - Follow the prompts to create a new Data Factory instance.
2. **Set Up Linked Services**:
   - In the Data Factory, go to `Manage` and then `Linked services`.
   - Create linked services for both your source and target Cosmos DB accounts by providing the necessary connection details.
3. **Create a Pipeline**:
   - Go to the `Author` section and create a new pipeline.
   - Add a `Copy Data` activity to the pipeline.
4. **Configure the Source**:
   - In the `Copy Data` activity, configure the source settings by selecting the linked service for your source Cosmos DB account.
   - Specify the database and container you want to migrate.
5. **Configure the Sink (Target)**:
   - Configure the sink settings by selecting the linked service for your target Cosmos DB account.
   - Specify the target database and container.
6. **Run the Pipeline**:
   - Validate the pipeline to ensure there are no errors.
   - Trigger the pipeline to start the data migration process.
7. **Monitor the Migration**: Use the monitoring tools in Azure Data Factory to track the progress of your data migration.

### Using the Azure Cosmos DB Spark connector for live migrations

> This method is particularly useful for large-scale data migrations and can be integrated with Databricks for a seamless process.

1. **Set Up Your Environment**:
   - **Databricks Workspace**: Ensure you have a Databricks workspace set up.
   - **Azure Cosmos DB Accounts**: Have both the source and target Azure Cosmos DB accounts ready.
2. **Install the Azure Cosmos DB Spark Connector**: Add the Azure Cosmos DB Spark connector library to your Databricks cluster. You can do this by navigating to the Libraries tab in your cluster configuration and installing the library from Maven coordinates:
     ```
     com.azure.cosmos.spark:azure-cosmos-spark_3_2-12:<version>
     ```
3. **Configure the Spark Session**: Configure your Spark session to use the Azure Cosmos DB Spark connector. Here’s an example configuration:
     ```scala
     import com.azure.cosmos.spark._
     import org.apache.spark.sql.SparkSession

     val spark = SparkSession.builder()
       .appName("CosmosDBLiveMigration")
       .config("spark.cosmos.accountEndpoint", "<source-account-endpoint>")
       .config("spark.cosmos.accountKey", "<source-account-key>")
       .config("spark.cosmos.database", "<source-database>")
       .config("spark.cosmos.container", "<source-container>")
       .getOrCreate()
     ```
     
4. **Read Data from the Source Cosmos DB**: Use the Spark DataFrame API to read data from the source Cosmos DB container:
     ```scala
     val sourceDF = spark.read.cosmos()
       .option("spark.cosmos.accountEndpoint", "<source-account-endpoint>")
       .option("spark.cosmos.accountKey", "<source-account-key>")
       .option("spark.cosmos.database", "<source-database>")
       .option("spark.cosmos.container", "<source-container>")
       .load()
     ```

5. **Write Data to the Target Cosmos DB**: Configure the target Cosmos DB account and write the data:
     ```scala
     sourceDF.write.cosmos()
       .option("spark.cosmos.accountEndpoint", "<target-account-endpoint>")
       .option("spark.cosmos.accountKey", "<target-account-key>")
       .option("spark.cosmos.database", "<target-database>")
       .option("spark.cosmos.container", "<target-container>")
       .mode("append")
       .save()
     ```
     
6. **Monitor the Migration**: Use Databricks monitoring tools to track the progress and performance of your migration job.

## Risks & Mitigation 

| **Risk**                         | **Description**                                                                 | **Mitigation Strategies**                                                                                   |
|----------------------------------|---------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Data Integrity and Consistency** | Risk of data corruption or loss during migration.                              | Implement comprehensive data validation checks before and after migration. Use reliable tools like Azure Data Factory or Cosmos DB Spark Connector. |
| **Downtime and Service Disruption** | Potential downtime or service disruption during migration.                     | Plan migration during low-traffic periods. Use a phased approach to gradually transfer data. Implement a rollback plan. |
| **Configuration and Compatibility Issues** | Differences in configurations between old and new accounts.                    | Thoroughly review and replicate settings from the old account. Test the new setup in a staging environment before going live. |
| **Performance Impact**            | Temporary performance impact during migration.                                 | Monitor performance closely and adjust throughput settings as needed. Use burst capacity feature to handle peak loads. |
| **Security Concerns**             | Handling sensitive information during data transfer.                           | Ensure data is encrypted during transfer. Conduct a security review of the new setup. |
| **Cost Implications**             | Additional costs incurred during setup and migration.                          | Estimate costs beforehand and ensure benefits outweigh expenses. Optimize new account configuration to avoid unnecessary costs. |
| **Complexity and Resource Requirements** | Complexity and resource-intensive nature of the migration process.             | Allocate sufficient resources and time for migration. Engage experts or use professional services if needed. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->