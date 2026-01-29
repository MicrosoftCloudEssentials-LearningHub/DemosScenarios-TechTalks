# Azure Synapse migrate to Microsoft Fabric - Overview 

 Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Migrating from Azure Synapse Spark to Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/migrate-synapse-overview)

     <img width="992" height="355" alt="image" src="https://github.com/user-attachments/assets/ccb6ce71-bb2e-4e27-b234-70e312fd64b6" />

- [Migration planning: Azure Synapse Analytics dedicated SQL pools to Fabric Data Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/migration-synapse-dedicated-sql-pool-warehouse#prepare-for-migration)

     <img width="1123" height="395" alt="image" src="https://github.com/user-attachments/assets/1479ea91-3cfa-48bd-ab75-2a190717e2b5" />

</details>

> Overall process: <br/>
> - Create a Fabric workspace and link it to your existing Azure Data Lake Storage account. <br/>
> - Import existing notebooks, Spark jobs into the Fabric workspace. <br/>
> - Update references to external tables or files using the OneLake syntax.

 ## Overview 
 
1. **Create a Fabric Workspace**
   - **Navigate to Microsoft Fabric**: Access the [Microsoft Fabric portal](https://app.fabric.microsoft.com/).

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/191672f9-e7b0-460b-aa23-886fa105f97e" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>

   - **Create Workspace**: Follow the steps to create a new workspace.

        https://github.com/user-attachments/assets/209f18fd-d14a-4e2f-aff2-d6cb7be13cc1

2. **Link ADLS Account**: Connect your existing Azure Data Lake Storage account to the new Fabric workspace.
      - **Set Up ADLS Connection**:
          - **Open Fabric Workspace**: Go to the workspace where you want to set up the connection.

              <img width="550" alt="image" src="https://github.com/user-attachments/assets/f4c87199-0d61-4db6-accd-27608d2257be" />

          - **Create a lakehouse**: Click on `New item`, search for `Lakehouse`:

              <img width="550" alt="image" src="https://github.com/user-attachments/assets/602b5d88-b1bc-44ff-9a0e-a3c6ddc15527">

              <img width="550" alt="image" src="https://github.com/user-attachments/assets/9b807c02-2111-4277-8e97-be0b08212ee6" />

          - **Get Data**: Select the option to get data from Azure Data Lake Storage Gen2.
          - **Enter ADLS URL**: Provide the URL to your Azure Data Lake Storage Gen2 account.
          - **Authentication**: Choose the authentication method (e.g., account key, organizational account, service principal, or shared access signature).
          - **Sign In**: Sign in to your Azure Data Lake Storage account using the selected authentication method.
          - **Configure Connection**: Complete the configuration by specifying any additional settings required for the connection.
      - **Create OneLake Shortcut**:
          - **Navigate to Lakehouse View**: In the Fabric workspace, go to the Lakehouse view.
          - **Create Shortcut**: Right-click and select "New Shortcut," then choose Azure Data Lake Storage Gen2 as the source.
          - **Enter Details**: Provide the URL of the ADLS Gen2 account, connection name, authentication method, shortcut name, and subpath pointing to the root of the data you want to reference.
          - **Create Shortcut**: Click "Create" and wait for the shortcut to appear in the Lakehouse view.
          - **Preview Data**: Preview the data from the shortcut to ensure it is virtualized from the source.
2. **Import Existing Notebooks and Spark Jobs**
   - **Export from Synapse**: Export your notebooks and Spark job definitions from Azure Synapse.
   - **Import to Fabric**: Use the import functionality in Fabric to bring these items into your new workspace.
3. **Update References**
   - **Identify External References**: Locate all references to external tables or files in your notebooks and Spark jobs.
   - **Modify Syntax**: Update these references to use the OneLake syntax, ensuring they point to the correct locations in Fabric.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
