# Migrating On-Premises SQL Server to Azure - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Discover and Assess SQL Server deployments for migration to Azure SQL with Azure Migrate - step by step](https://techcommunity.microsoft.com/blog/azuremigrationblog/discover-and-assess-sql-server-deployments-for-migration-to-azure-sql-with-azure/2365162)
- [SQL Server Discovery and Assessments now supports As on-premises assessments](https://techcommunity.microsoft.com/blog/azuresqlblog/sql-server-discovery-and-assessments-now-supports-as-on-premises-assessments/3988691)
- [Migration overview: From SQL Server](https://learn.microsoft.com/en-us/data-migration/sql-server/overview)
- [Migrate from SQL Server: Pre-migration](https://learn.microsoft.com/en-us/data-migration/sql-server/pre-migration?tabs=sqlmi)
- [Migrate SQL Server to Azure SQL Managed Instance at Scale](https://techcommunity.microsoft.com/blog/modernizationbestpracticesblog/migrate-sql-server-to-azure-sql-managed-instance-at-scale/3970683)
- [Migrate on-premises SQL Server or SQL Server on Azure VMs to Azure SQL Database using the Data Migration Assistant](https://learn.microsoft.com/en-us/sql/dma/dma-migrateonpremsqltosqldb?view=sql-server-ver16)
- [Deploy SharePoint Server with Azure SQL Managed Instance](https://learn.microsoft.com/en-us/SharePoint/administration/deploy-azure-sql-managed-instance-with-sharepoint-servers)

</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Step 1: Assess the Current Environment](#step-1-assess-the-current-environment)
    - [Determine the version of the on-premises SQL Server](#determine-the-version-of-the-on-premises-sql-server)
    - [Migration Methods Based on SQL Server Version](#migration-methods-based-on-sql-server-version)
- [Step 2: Options Based on Linked Servers](#step-2-options-based-on-linked-servers)
    - [If Linked Servers Exist](#if-linked-servers-exist)
    - [If No Linked Servers](#if-no-linked-servers)
- [Integration with SharePoint Online](#integration-with-sharepoint-online)

</details>

> [!IMPORTANT]
> 1. **Determine the version of the on-premises SQL Server**: This will guide the migration path. For example, SQL Server 2016 or newer has more migration options compared to older versions. <br/>
> 2. **Linked Servers**: Check if there are any linked servers <br/>
>     - **Azure SQL Database** does not support linked servers. <br/>
>     - **Azure SQL Managed Instance** supports linked servers. <br/> 
>     - **SQL Server on Azure Virtual Machines (IaaS)** supports linked servers.
> 3. **Plan Integration**: Use Azure Logic Apps, Power Automate, or custom APIs for integration with SharePoint Online.

## Step 1: Assess the Current Environment

> - **Determine the SQL Server Version**: This will guide the migration path and options available.
> - **Evaluate Migration Methods**: Based on the SQL Server version, choose the appropriate migration method.
> - **Consider High Availability**: If using AlwaysOn Availability Groups, ensure compatibility with SQL Server and Windows Server versions.

### Determine the version of the on-premises SQL Server

| SQL Server Version       | Support Status         | Migration Options                                                                 | Considerations                                                                 | High Availability Options                          |
|--------------------------|------------------------|----------------------------------------------------------------------------------|--------------------------------------------------------------------------------|---------------------------------------------------|
| **SQL Server 2008 and 2008 R2** | End of Support: These versions are no longer supported by Microsoft, which means no security updates or patches.         | - Azure SQL Managed Instance: Provides a fully managed instance with high compatibility.<br>- SQL Server on Azure Virtual Machines: Allows you to run older SQL Server versions in a VM. | Upgrading to a newer version before migration is recommended for better support and features. |   N/A                                              |
| **SQL Server 2012**      | Extended Support: Limited support with security updates.      | - Azure SQL Managed Instance: High compatibility with on-premises SQL Server.<br>- SQL Server on Azure Virtual Machines: Suitable for maintaining the same SQL Server version. | Evaluate the benefits of upgrading to a newer version for enhanced features and support. |                            N/A                       |
| **SQL Server 2014**      | Mainstream Support: Still within mainstream support but nearing end of life.     | - Azure SQL Managed Instance: High compatibility and managed service.<br>- SQL Server on Azure Virtual Machines: Full control over the SQL Server instance. | Consider upgrading to SQL Server 2016 or newer for better migration options.   |                     N/A                              |
| **SQL Server 2016 and Newer** | Full Support: These versions are fully supported with regular updates and patches.          | - Azure SQL Database: Suitable if no linked servers are required.<br>- Azure SQL Managed Instance: Supports linked servers and high compatibility.<br>- SQL Server on Azure Virtual Machines: Full control and flexibility. | These versions offer the most flexibility and features for migration.          | - AlwaysOn Availability Groups: Supported for seamless migration.<br>- Failover Cluster Instances: Supported for high availability. |

### Migration Methods Based on SQL Server Version

1. **Backup and Restore**
   - **Supported Versions**: All versions.
   - **Description**: Take a backup of the on-premises database and restore it in Azure SQL Managed Instance or SQL Server on Azure VM.
   - **Considerations**: Simple method but may involve downtime.

2. **Database Migration Service (DMS)**
   - **Supported Versions**: SQL Server 2005 and newer.
   - **Description**: Use Azure Database Migration Service to migrate databases with minimal downtime.
   - **Considerations**: Recommended for larger databases and mission-critical applications.

3. **Transactional Replication**
   - **Supported Versions**: SQL Server 2008 and newer.
   - **Description**: Set up transactional replication to synchronize data between on-premises SQL Server and Azure SQL Database or Managed Instance.
   - **Considerations**: Suitable for continuous data synchronization with minimal downtime.

4. **AlwaysOn Availability Groups**
   - **Supported Versions**: SQL Server 2012 and newer.
   - **Description**: Add an Azure VM to the availability group and perform a failover.
   - **Considerations**: Requires SQL Server 2016 or newer and Windows Server 2016 or later for multi-subnet configurations.

5. **BACPAC Files**
   - **Supported Versions**: SQL Server 2008 and newer.
   - **Description**: Export the database schema and data to a BACPAC file and import it into Azure SQL Database.
   - **Considerations**: Suitable for smaller databases but may not be reliable for large or complex databases.


## Step 2: Options Based on Linked Servers

| Scenario | Options | Description, Benefits, Considerations, and Integration |
| --- | --- | --- |
| **If Linked Servers Exist** | - **Azure SQL Managed Instance (PaaS)**<br/>- **SQL Server on Azure Virtual Machines (IaaS)** | - **Azure SQL Managed Instance**: Near 100% compatibility with on-premises SQL Server, minimal changes required, higher cost, use Azure Logic Apps or Power Automate for integration.<br/>- **SQL Server on Azure Virtual Machines**: Full control over the SQL Server instance, requires VM management, use custom APIs or Azure Logic Apps for integration. |
| **If No Linked Servers** | - **Azure SQL Database (PaaS)**<br/>- **Azure SQL Managed Instance (PaaS)**<br/>- **SQL Server on Azure Virtual Machines (IaaS)** | - **Azure SQL Database**: Fully managed, reduces management overhead, may require schema changes, use Azure Logic Apps or Power Automate for integration.<br/>- **Azure SQL Managed Instance**: Near 100% compatibility, minimal changes required, higher cost, use Azure Logic Apps or Power Automate for integration.<br/>- **SQL Server on Azure Virtual Machines**: Full control over the SQL Server instance, requires VM management, use custom APIs or Azure Logic Apps for integration. |


### If Linked Servers Exist

<details>
<summary><strong>Azure SQL Managed Instance (PaaS)</strong></summary>

> A fully managed instance of SQL Server that provides near 100% compatibility with the latest SQL Server on-premises.

- **Benefits**:
  - Minimal changes required to migrate.
  - Supports SQL Server Agent and other SQL Server features.
  - Reduces administrative overhead as Microsoft handles patching, backups, and monitoring.
  - Built-in high availability and disaster recovery options.
  - Easily scalable to meet growing data and performance needs.
- **Considerations**:
  - Higher cost compared to Azure SQL Database.
  - The migration process can be complex and may require careful planning and execution.
- **Integration with SharePoint Online**:
  - Use Azure Logic Apps to create workflows that automate data exchange.
  - Use Power Automate to create flows that connect Azure SQL Managed Instance with SharePoint Online.
  - Develop custom APIs to facilitate data exchange between the two services.
</details>

<details>
<summary><strong>SQL Server on Azure Virtual Machines (IaaS)</strong></summary>

>  Running SQL Server on a virtual machine in Azure, providing full control over the SQL Server instance.

- **Benefits**:
  - Full control over the database and OS.
  - Suitable for applications requiring specific SQL Server features.
  - Supports linked servers, SQL Server Agent, and other advanced SQL Server features.
  - Ability to customize the environment to meet specific requirements.
- **Considerations**:
  - Requires management of the VM, including patching, backups, and high availability.
  - More complex to manage compared to fully managed services like Azure SQL Database or Managed Instance.
  - Potentially higher operational costs due to the need for VM management and maintenance.
- **Integration with SharePoint Online**:
  - Develop custom APIs to facilitate data exchange between SQL Server on Azure VM and SharePoint Online.
  - Use Azure Logic Apps to create workflows that automate data exchange.
  - Use Power Automate to create flows that connect SQL Server on Azure VM with SharePoint Online.
</details>

### If No Linked Servers

<details>
<summary><strong>Azure SQL Database (PaaS)</strong></summary>

> `A fully managed relational database` service that handles most database management functions such as upgrading, patching, backups, and monitoring without user involvement.

- **Benefits**:
  - Reduces management overhead.
  - Built-in high availability and scalability.
  - Simplifies database management with automatic updates and scaling.
- **Considerations**:
  - May require some changes to your database schema or application code.
- **Integration with SharePoint Online**:
  - Use Azure Logic Apps to create workflows that automate data exchange.
  - Use Power Automate to create flows that connect Azure SQL Database with SharePoint Online.
</details>

<details>
<summary><strong>Azure SQL Managed Instance (PaaS)</strong></summary>

> `A fully managed instance of SQL Server` that provides near 100% compatibility with the latest SQL Server on-premises.

- **Benefits**:
  - Minimal changes required to migrate.
  - Supports SQL Server Agent and other SQL Server features.
  - Reduces administrative overhead as Microsoft handles patching, backups, and monitoring.
  - Built-in high availability and disaster recovery options.
  - Easily scalable to meet growing data and performance needs.
- **Considerations**:
  - Higher cost compared to Azure SQL Database.
  - The migration process can be complex and may require careful planning and execution.
- **Integration with SharePoint Online**:
  - Use Azure Logic Apps to create workflows that automate data exchange.
  - Use Power Automate to create flows that connect Azure SQL Managed Instance with SharePoint Online.
  - Develop custom APIs to facilitate data exchange between the two services.
</details>

<details>
<summary><strong>SQL Server on Azure Virtual Machines (IaaS)</strong></summary>

> Running SQL Server on a virtual machine in Azure, providing full control over the SQL Server instance.

- **Benefits**:
  - Full control over the database and OS.
  - Suitable for applications requiring specific SQL Server features.
  - Supports linked servers, SQL Server Agent, and other advanced SQL Server features.
  - Ability to customize the environment to meet specific requirements.
- **Considerations**:
  - Requires management of the VM, including patching, backups, and high availability.
  - More complex to manage compared to fully managed services like Azure SQL Database or Managed Instance.
  - Potentially higher operational costs due to the need for VM management and maintenance.
- **Integration with SharePoint Online**:
  - Develop custom APIs to facilitate data exchange between SQL Server on Azure VM and SharePoint Online.
  - Use Azure Logic Apps to create workflows that automate data exchange.
  - Use Power Automate to create flows that connect SQL Server on Azure VM with SharePoint Online.
</details>

## Integration with SharePoint Online

> - Azure Logic Apps: Automate workflows to facilitate data exchange between Azure SQL Database and SharePoint Online using built-in connectors and triggers. <br/> 
> - Power Automate: Create flows to connect Azure SQL Database with SharePoint Online using pre-built templates and connectors. <br/> 
> - Custom APIs: Develop custom APIs for tailored data exchange solutions, providing flexibility and control over the integration process.

<details>
<summary><strong>Azure Logic Apps</strong></summary>

> Azure Logic Apps is a cloud-based service that allows you to automate workflows and integrate apps, data, services, and systems.

- **Use Case**: Automate data exchange between Azure SQL Database and SharePoint Online.
- **How It Works**:
  1. **Create a Logic App**: Start by creating a new Logic App in the Azure portal.
  2. **Define Triggers**: Set up triggers that initiate the workflow. For example, a trigger could be a new item added to a SharePoint list or a new row inserted into an Azure SQL Database table.
  3. **Add Actions**: Define actions that the Logic App should perform. Actions can include reading data from Azure SQL Database, transforming the data, and then writing it to SharePoint Online.
  4. **Connectors**: Use built-in connectors for Azure SQL Database and SharePoint Online to facilitate the data exchange.
  5. **Error Handling**: Implement error handling and retries to ensure the workflow runs smoothly even if there are temporary issues.
- **Example**: A Logic App that triggers when a new row is added to an Azure SQL Database table, retrieves the data, and creates a new item in a SharePoint Online list.
</details>

<details>
<summary><strong>Power Automate</strong></summary>

> Power Automate (formerly Microsoft Flow) is a service that helps you create automated workflows between your favorite apps and services to synchronize files, get notifications, collect data, and more.

- **Use Case**: Create flows to connect Azure SQL Database with SharePoint Online.
- **How It Works**:
  1. **Create a Flow**: Start by creating a new flow in Power Automate.
  2. **Define Triggers**: Set up triggers that initiate the flow. For example, a trigger could be a new item added to a SharePoint list or a new row inserted into an Azure SQL Database table.
  3. **Add Actions**: Define actions that the flow should perform. Actions can include reading data from Azure SQL Database, transforming the data, and then writing it to SharePoint Online.
  4. **Connectors**: Use built-in connectors for Azure SQL Database and SharePoint Online to facilitate the data exchange.
  5. **Templates**: Utilize pre-built templates to quickly set up common workflows.
- **Example**: A flow that triggers when a new item is added to a SharePoint Online list, retrieves the data, and inserts it into an Azure SQL Database table.
</details>

<details>
<summary><strong>Custom APIs</strong></summary>

> Custom APIs allow you to develop tailored solutions for specific integration needs, providing flexibility and control over the data exchange process.

- **Use Case**: Develop custom APIs for data exchange between Azure SQL Database and SharePoint Online.
- **How It Works**:
  1. **Develop API**: Create a custom API using a programming language such as C# or Python. The API should handle data retrieval, transformation, and insertion.
  2. **Host API**: Host the API in a suitable environment, such as Azure App Service or Azure Functions.
  3. **Authentication**: Implement secure authentication mechanisms, such as OAuth, to ensure that only authorized users and applications can access the API.
  4. **Endpoints**: Define endpoints for the API that allow for CRUD (Create, Read, Update, Delete) operations on the data.
  5. **Integration**: Use the API to facilitate data exchange between Azure SQL Database and SharePoint Online. The API can be called from Logic Apps, Power Automate, or directly from client applications.
- **Example**: A custom API that retrieves data from an Azure SQL Database table, processes the data, and updates a SharePoint Online list.
</details>

> [!TIP]
> Summary of Options: 

| Option | Description | Key Features | Integration with SharePoint Online |
| --- | --- | --- | --- |
| **Azure SQL Database (PaaS)** | Suitable if no linked servers are required. | - Supports transactional replication.<br/>- Reduces management overhead.<br/>- Built-in high availability and scalability. | Use Azure Logic Apps or Power Automate for integration with SharePoint Online. |
| **Azure SQL Managed Instance (PaaS)** | Supports linked servers. | - Supports both availability group and transactional replication methods.<br/>- Near 100% compatibility with on-premises SQL Server.<br/>- Built-in high availability and disaster recovery options. | Use Azure Logic Apps or Power Automate for integration with SharePoint Online. |
| **SQL Server on Azure Virtual Machines (IaaS)** | Provides full control over the SQL Server instance. | - Supports linked servers and all SQL Server features.<br/>- Suitable for applications requiring OS-level access.<br/>- Full control over the database and OS. | Use custom APIs or Azure Logic Apps for integration with SharePoint Online. |


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
