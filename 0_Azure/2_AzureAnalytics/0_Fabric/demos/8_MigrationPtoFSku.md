# Migration from Power BI Premium (P-SKUs) to Fabric (F-SKUs) 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-12-24

----------

> [!IMPORTANT]
> 🔺 This approach is around `reassign workspaces without tenant migration`, if you decide to migrate the tenant in the future, you can do so with the workspaces already assigned to the new capacity.

> $${\color{red}Same\ geo\ but\ across\ region}$$ The `multi-geography setup` in Microsoft Fabric allows you to deploy content to data centers in regions other than the home region of your Fabric tenant. This feature is particularly useful for multinational customers who need to address regional, industry-specific, or organizational data residency requirements.` In your example, if you have the US as the geography with Central US and West US 2 as regions, you can set up a Fabric capacity reservation in one of these regions. Once a capacity is created, it remains in that region, and any workspaces created under it will have their content stored in that region`. This approach ensures that `you don't need to move the home region`, which can simplify management and compliance. Click [here for more information about it](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)

## Wiki 

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Important update to Power BI Premium licensing](https://www.microsoft.com/en-us/licensing/news/power-bi-premium-sku-retirement)
- [Important update coming to Power BI Premium licensing - Blog](https://powerbi.microsoft.com/en-us/blog/important-update-coming-to-power-bi-premium-licensing/)
- [Microsoft Fabric concepts and licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#per-user-licenses)
- [Moving Fabric (Power BI) Workspaces from Premium or Free Trial to new F SKUs](https://techcommunity.microsoft.com/t5/healthcare-and-life-sciences/moving-fabric-power-bi-workspaces-from-premium-or-free-trial-to/ba-p/4176482)
- [Deploying Microsoft Fabric Capacity Using Terraform](https://murggu.medium.com/deploying-microsoft-fabric-azure-capacity-using-terraform-8dfcbab16f64)
- [Announcing the availability of Trusted workspace access and Managed private endpoints in any Fabric capacity](https://blog.fabric.microsoft.com/en-us/blog/announcing-the-availability-of-trusted-workspace-access-and-managed-private-endpoints-in-any-fabric-capacity?ft=All)
- [Migrate to Data Factory - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/upgrade-paths)
- [Fabric F64 capacity vs. Power BI Premium P1 capacity](https://community.fabric.microsoft.com/t5/General-Discussion/Fabric-F64-capacity-vs-Power-BI-Premium-P1-capacity/m-p/3708411)
- [Solved: Power BI Premium migration to Fabric - Microsoft Fabric Community](https://community.fabric.microsoft.com/t5/Service/Power-BI-Premium-migration-to-Fabric/td-p/3975917)
- [Data Factory documentation in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/)
- [Microsoft Fabric changing the game: Exporting data and building the Lakehouse](https://blog.fabric.microsoft.com/en-US/blog/microsoft-fabric-changing-the-game-exporting-data-and-building-the-lakehouse/)
- [Export and sharing tenant settings - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/admin/service-admin-portal-export-sharing)
- [Load data into your lakehouse with a notebook - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-notebook-load-data)
- [How to copy data using copy activity - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/copy-data-activity)
- [Move and transform data with dataflow and data pipelines - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/transform-data)
- [Configure Multi-Geo support for Fabric](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)
  
</details>

## Overview 

| Update                          | Details                                                                                                                                                                                                 |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Retirement of P-SKUs**        | - **New Customers**: As of July 1, 2024, new customers will no longer be able to purchase Power BI Premium per capacity (P-SKUs).<br> - **Existing Customers**: Those without an Enterprise Agreement (EA) can renew their P-SKUs until January 1, 2025. After this date, they will need to transition to Fabric SKUs at the end of their agreement. |
| **Transition to Fabric SKUs**   | - **Flexibility**: Fabric SKUs offer more flexibility in terms of size and billing options, including pay-as-you-go.<br> - **Azure Integration**: Fabric SKUs provide access to Azure-only features and are eligible for Microsoft Azure Consumption Commitment (MACC).<br> - **Unified Platform**: Microsoft Fabric combines Power BI, Azure Synapse Analytics, and Azure Data Factory into a single SaaS platform, offering all the capabilities of Power BI Premium plus additional workloads. |
| **Impact on Different Agreements** | - **Enterprise Agreement (EA) Customers**: Can continue to renew their P-SKUs annually until the end of their EA agreement. If the agreement ends after January 1, 2025, they will need to transition to Fabric SKUs.<br> - **Sovereign Cloud Customers**: Not impacted by this change as they do not currently have access to Microsoft Fabric. |

> `P SKU`: Best for organizations focused solely on `Power BI` with fixed capacity needs and AutoScale. <br/>
> `F SKU`: Ideal for those looking for a `more integrated, flexible, and scalable solution` that leverages Azure’s full capabilities.

| Feature/Aspect                     | Power BI Premium (P SKU)                  | Fabric (F SKU)                              |
|------------------------------------|--------------------------------------------|---------------------------------------------|
| **Flexibility and Scalability**    | Fixed capacity with predefined resource limits. Suitable for organizations with stable, predictable workloads. | Offers flexible options, including pay-as-you-go and various sizes to better match dynamic needs. Ideal for organizations with fluctuating workloads. |
| **Integration with Azure**         | Primarily focused on Power BI capabilities. Limited integration with other Azure services. | Integrates Power BI with Azure Synapse Analytics and Azure Data Factory, providing a unified platform for comprehensive data analytics and processing. |
| **AutoScale Feature**              | Includes AutoScale, which automatically adjusts capacity based on demand, ensuring optimal performance during peak times. | AutoScale is currently not available but is planned for future updates, aiming to provide similar dynamic scaling capabilities. |
| **Azure-Only Features**            | Limited to Power BI features, with no access to exclusive Azure functionalities. | Provides access to additional Azure-only features, enhancing data processing, analytics, and integration capabilities. |
| **Microsoft Azure Consumption Commitment (MACC)** | Not eligible for MACC, meaning Azure consumption commitments cannot be applied towards purchasing P1 SKUs. | Eligible for MACC, allowing organizations to use their Azure consumption commitments towards purchasing Fabric SKUs, optimizing overall cloud spending. |
| **Usage and Workloads**            | Designed for enterprises needing a complete BI solution with fixed capacity. Suitable for stable, predictable BI workloads. | Supports a broader range of workloads, including those from Power BI, Azure Synapse, and Azure Data Factory. Ideal for organizations needing a versatile, integrated data analytics platform. |
| **Performance and Scalability**    | Fixed performance based on the purchased capacity. May require manual adjustments to handle increased demand. | Enhanced performance and scalability options, with the ability to scale resources dynamically based on actual usage and demand. |
| **Cost Management**                | Fixed cost based on the purchased capacity, with potential additional costs for overages. | Flexible cost management with pay-as-you-go options, allowing for better alignment with actual usage and budget optimization. |
| **Support and Maintenance**        | Standard support and maintenance as part of the Power BI Premium offering. | Enhanced support and maintenance options, leveraging the broader Azure ecosystem for comprehensive service management. |
| **Future-Proofing**                | Limited to the current capabilities of Power BI Premium. May require additional investments for future upgrades. | Future-proof with ongoing updates and enhancements as part of the Microsoft Fabric platform, ensuring access to the latest features and innovations. |

## Impact on Existing Reports and Dashboards

| Impact Area            | Details                                                                                                                                                                                                 |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Seamless Transition**| - **No Immediate Changes**: Your existing reports and dashboards will continue to function as they do now during the transition period.<br> - **Migration Support**: Microsoft provides tools and support to help migrate your content from P-SKUs to F-SKUs, ensuring a smooth transition. |
| **Enhanced Capabilities** | - **New Features**: Once migrated, you’ll have access to additional features and capabilities available in Microsoft Fabric, which can enhance your reports and dashboards.<br> - **Improved Performance**: Fabric SKUs are designed to offer better performance and scalability, which can improve the responsiveness and efficiency of your reports. |
| **Integration with Azure** | **Azure-Only Features**: You’ll gain access to Azure-only features that can be integrated into your existing reports and dashboards, providing more advanced analytics and data processing options. |
| **No Data Loss**       | **Data Integrity**: The migration process ensures that there is no loss of data or functionality in your existing reports and dashboards. |
| **Components needing recreation** | Since it's cross-region, `Fabric components` like lake houses, warehouses, and real-time analytics components `needs to be recreated` | 

> [!IMPORTANT]
> - Data Refresh Settings: After migrating a workspace to a new capacity, the data refresh settings should remain intact. However, please verify the settings post-migration to ensure they are configured as expected. <br/>
> - Scheduled Refreshes: Make sure that no manual or scheduled refreshes are running during the migration process to avoid any conflicts or interruptions. <br/>
> - Capacity-Specific Features: Some features, like automatic page refresh for DirectQuery sources, are specific to Premium capacities and need to be reconfigured if the capacity type changes. <br/>
> - If `errors`, you can switch back to the old capacity, and troubleshoot.

## How to transition 

> [!NOTE]
> If the resources are in the $${\color{red}same\ region}$$, it's just $${\color{red}reassigning\ the\ workspace\ compute\ ->\ Capacity}$$

> [!IMPORTANT]
> API Call for Bulk Migration: For multiple workspaces using an API call to get all workspaces in a capacity and then performing a bulk migration, could simplify the process and identify any workspaces that need manual intervention. Use this as reference [Solved: Re: Bulk Assign Workspace Capacity - Microsoft Fabric Community](https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html), and [Admin - Groups GetGroupsAsAdmin](https://learn.microsoft.com/en-us/rest/api/power-bi/admin/groups-get-groups-as-admin)

1. **Review Current Capacity and Usage**:
     - Review the current usage and performance metrics of your P1 capacity.
     - Identify the workspaces, datasets, reports, and dashboards that need to be migrated.
2. **Plan the Transition**:
   - **Set a Timeline**: Determine a timeline for the transition, considering your current agreement's renewal date.
   - **Communicate with Stakeholders**: Inform all relevant stakeholders about the upcoming changes and timeline.
3. **Create Fabric SKU**: `-> Compute`
      | Service                | Steps                                                                                       |
      |-----------------------|---------------------------------------------------------------------------------------------|
      | Pay-as-you-go | - Log in to the Azure portal.<br> - Navigate to the resource group where you want to create the Fabric capacity.<br> - Within the resource group, select the option to create a new resource.<br> - Search for and select the Fabric capacity option.<br> - Follow the prompts to configure and create the Fabric capacity. |
      | Fabric Reservations   |      [Click here](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/12_FabricReservation.md) |

4. **Migrate Workspaces**: `-> Compute`
    1. Access Power BI Admin Portal
       - **Log In**: Open your web browser and go to the Power BI Admin portal. Log in using your administrator credentials.
       - **Navigate to Admin Portal**: Once logged in, click on the gear icon (⚙️) in the top right corner and select `Admin Portal` from the dropdown menu.

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/ec0c32dc-17aa-46c5-9912-1f5920d7e0d3">

    2. Identify Workspaces: Identify the workspaces currently assigned to the P1 SKU that you want to migrate to the Fabric SKU
       - **Go to Workspaces**: In the Admin Portal, navigate to the `Workspaces` section. This will display a list of all the workspaces in your organization.

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/d9441ad8-1919-49c5-baf4-e0eaec050332">

    3. Reassign Capacity 
       - **Manual Approach**:
          - **Select Workspace**: Click on the workspace you want to migrate. This will open the workspace settings.
          - **Change Capacity**: In the workspace settings, look for the `Capacity` section. You will see an option to change the capacity assignment.
          - **Select Fabric SKU**: From the dropdown menu, select the new Fabric SKU that you have purchased.
          - **Save Changes**: Click "Save" to apply the changes. The workspace will now be reassigned to the new Fabric SKU.
   
               <img width="550" alt="image" src="https://github.com/user-attachments/assets/3587658e-50b8-484a-b048-07de018a15fe">

         - **Bulk Assignment**:
            - Use the bulk assignment feature in the Admin Portal to reassign multiple workspaces at once.

               <img width="550" alt="image" src="https://github.com/user-attachments/assets/4c517df9-c79a-41bd-a21d-f0fb1b425aad">
              
            - Verify that all workspaces are correctly reassigned.

               <img width="550" alt="image" src="https://github.com/user-attachments/assets/1a6cbfdf-cde3-4eb4-a7d8-f66a28094059">

> [!NOTE]
> If the $${\color{red}across\ region}$$, you need to $${\color{red}also\ export/import\ reports\ and\ semantic\ models,\ recreate\ dashboards}$$.

5. Data Export and Import: `-> Sematic Models/Dataset`
   - `For small Datasets`: Use Power BI’s export features to export datasets from the P1 capacity.
      1. **Identify Data Sources**: List all datasets you need to export from the P1 capacity.
      2. **Export Data Using Power BI**:
         - Go to the Power BI service.
         - Navigate to the workspace containing the datasets.
         - Select the dataset you want to export.
         - Click on the **Export** option and choose the desired format (e.g., CSV, Excel).
      3. **Import Data into F64 Capacity**:
         - Go to the Power BI service in the F64 capacity.
         - Navigate to the workspace where you want to import the datasets.
         - Click on **Upload** > **Upload a file** and select the exported files.
         - Verify that the data is correctly imported and update any data connections if necessary.
   - `For large Datasets`: Consider using scripts, Power BI XMLA or Data Factory to facilitate the export.
      - Backup and Restore requires using XMLA-based tools, such as SQL Server Management Studio (SSMS):
          - If not sure if small dataset or large dataset, click here: [Large semantic models in Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-large-models)
          - Detailed method: [Backup and restore semantic models with Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset)

          | **Step**                | **Description**                                                                                                                                                                                                 |
          |-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
          | **Requirements**        | - Power BI Premium or Premium Per User (PPU) license. Click here to see [What is Power BI Premium?](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-what-is) <br> - Use XMLA-based tools like SQL Server Management Studio (SSMS).   |
          | **Backup Process**      | - **Connect to Power BI**: Use SSMS to connect to your Power BI Premium workspace.<br>- **Backup Command**: Execute a backup command to save the dataset to an Azure Data Lake Storage Gen2 (ADLS Gen2) account. |
          | **Restore Process**     | - **Prepare Backup Files**: Ensure the backup files (.abf) are in the correct folder in your ADLS Gen2 account.<br>- **Restore Command**: Use SSMS to execute a restore command, specifying the backup file and target dataset. |
          | **Considerations**      | - **Storage Account Configuration**: Backup and Restore use an ADLS Gen2 storage account configured at the tenant or workspace level.<br>- **Permissions**: Only users with appropriate permissions (admin or contributor) can perform backup and restore operations.<br>- **Limitations**: Ensure your ADLS Gen2 account is accessible and not restricted by VNET or firewall settings. |

      - Using Data Factory:
          1. **Set Up Data Factory in Microsoft Fabric**:
             - Go to the Microsoft Fabric portal.
             - Navigate to `Data Factory`.
          2. **Create a Data Pipeline**:
             - In Data Factory, create a new `Data Pipeline`.
             - Add a **Copy Data** activity to the pipeline.
             - Configure the source to be your P1 capacity data source.
             - Configure the destination to be a storage account or directly to the F64 capacity.
    
                <img width="421" alt="image" src="https://github.com/user-attachments/assets/4e6b4bd6-c746-49c4-baeb-5da12d59afb5">
     
          3. **Run the Pipeline**:
             - Execute the pipeline to transfer the data.
             - Monitor the pipeline execution to ensure data is transferred successfully.
          4. **Import Data into F64 Capacity**:
             - If the data was copied to a storage account, use Data Factory to import it into the F64 capacity.
             - Create a new pipeline in Data Factory to copy data from the storage account to the F64 capacity.
             - Execute the pipeline and verify that the data is correctly imported.

6. Migrate `Reports and Dashboards`: 
   - Export Reports and Dashboards from P1 Capacity
      1. **Identify Reports and Dashboards**: List all reports and dashboards you need to migrate.
      2. **Export Reports**:
         - Go to the Power BI service.
         - Navigate to the workspace containing the reports.
         - Select the report you want to export.
         - Click on **File** > **Download this report** to download the .pbix file.
      3. **Export Dashboards**: Dashboards cannot be directly exported. Note the configuration and visuals used in each dashboard for recreation.
   - Import Reports and Dashboards into F64 Capacity
      1. **Import Reports**:
         - Go to the Power BI service in the F64 capacity.
         - Navigate to the workspace where you want to import the reports.
         - Click on **Upload** > **Upload a file** and select the .pbix file you downloaded.
         - Update data sources and connections to point to the new F64 capacity.
      2. **Recreate Dashboards**: Manually recreate the dashboards in the F64 capacity by pinning the necessary visuals from the imported reports.
         
> [!NOTE]
> Verify the $${\color{red}migration\ and\ documentation}$$ are steps recommended for $${\color{red}both\ approaches,\ same\ region\ migration\ or\ across\ region}$$.
         
7. **Verify Migration**:
   - **Check Functionality**:
      1. **Verify Data Integrity**:
         - Compare row counts, checksums, or other data validation techniques to ensure data integrity.
         - Check for any data loss or corruption during the migration.
      2. **Test Reports and Dashboards**:
         - Thoroughly test all reports and dashboards to ensure they function correctly.
         - Look for any broken links, missing data, or performance issues.
   - **Monitor Performance**: 
      - Use the monitoring tools in Microsoft Fabric to track usage and performance metrics.
      - Identify any performance bottlenecks and optimize as needed.
      - Based on the performance metrics, adjust the capacity settings to optimize performance.
8. **Documentation and Backups**:
   - **Backup Data and Reports**:
      - Keep backups of your data and reports before and after migration.
      - Store backups in a secure location.
   - **Update Internal Documentation**: Reflect the changes in your internal documentation.
      - Document each step of the migration process.
      - Note any issues encountered and how they were resolved for future reference.
   - **Train Users**: Provide training sessions for users to familiarize them with any new features and capabilities of the Fabric SKU.
     
<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
