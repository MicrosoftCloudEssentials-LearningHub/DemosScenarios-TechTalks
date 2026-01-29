# Azure SQL Database - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Azure SQL Database is a relational database-as-a-service (DBaaS) that supports both standalone databases and elastic pools. It uses the latest stable version of the SQL Server Database Engine and offers features like T-SQL commands for creating tables, bulk loading data, and querying data

## Wiki 

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Azure SQL Database pricing](https://azure.microsoft.com/en-us/pricing/details/azure-sql-database/single/?msockid=38ec3806873362243e122ce086486339#pricing)
- [Azure princing calculator](https://azure.microsoft.com/en-gb/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)
- [Azure SQL Database documentation](https://learn.microsoft.com/en-us/azure/azure-sql/database/?view=azuresql)
- [Deployment tutorial](https://learn.microsoft.com/en-us/azure/azure-sql/database/saas-multitenantdb-get-started-deploy?view=azuresql)
- [Tutorial: Design a relational database in Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/design-first-database-tutorial?view=azuresql)
- [Microsoft Azure - Fault Tolerance Pitfalls and Resolutions in the Cloud](https://learn.microsoft.com/en-us/archive/msdn-magazine/2015/september/microsoft-azure-fault-tolerance-pitfalls-and-resolutions-in-the-cloud)
- [Availability through redundancy - Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/high-availability-sla-local-zone-redundancy?view=azuresql)
- [Availability through local and zone redundancy - Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/high-availability-sla-local-zone-redundancy?view=azuresql)
- [Disaster recovery guidance - Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/disaster-recovery-guidance?view=azuresql)
- [Cloud business continuity - disaster recovery - Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/business-continuity-high-availability-disaster-recover-hadr-overview?view=azuresql)
- [Authorize database access to SQL Database, SQL Managed Instance, and more](https://learn.microsoft.com/en-us/azure/azure-sql/database/logins-create-manage?view=azuresql)
- [Microsoft Entra authentication - Azure SQL Database & Azure SQL Managed Instance](https://learn.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-overview?view=azuresql)
- [Azure SQL Database security overview](https://learn.microsoft.com/en-us/azure/azure-sql/database/security-overview?view=azuresql)
- [Azure SQL Database performance best practices](https://learn.microsoft.com/en-us/azure/azure-sql/database/performance-best-practices?view=azuresql)

</details>

## Overview

| Topic                        | Description                                                                                                                                                                                                 |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Fault Tolerance**          | Azure SQL Database ensures fault tolerance through various redundancy options at physical, server, and database levels. SQL Database Hyperscale separates compute and storage layers for increased redundancy. Azure's infrastructure can handle hardware failures by moving virtual machines to other physical nodes. |
| **High Availability**        | Achieved through local and zone redundancy, allowing quick recovery from failures and minimal downtime. Supports active geo-replication and failover groups to enhance availability.                                                              |
| **Disaster Recovery**        | Provides automated backups, geo-redundant storage, and active geo-replication to ensure data protection and quick restoration in the event of a regional outage.                                                                                   |
| **Authentication and Authorization** | Supports both SQL authentication and Microsoft Entra ID (formerly Azure Active Directory) authentication for secure and centralized management of user identities and permissions. Entra ID enables multifactor authentication and conditional access controls. |

## Deploying MS SQL Server in Azure Tenant

1. **Sign in to Azure Portal**: Use your Azure account to sign in.
2. **Create a SQL Server/DB**:
   - Search for Azure SQL.
   - Click on `Create` to create a new SQL Service.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/ec41ae87-b441-4791-8b2a-b48cf9de8723">

   - Choose the deployment option:
     
       <img width="550" alt="image" src="https://github.com/user-attachments/assets/631f176f-2724-4f71-9ab7-e7edebe03587">

      | Deployment Option          | Description                                                                 | Features                                      | Use Case                                                                                   | Resource Type          |
      |----------------------------|-----------------------------------------------------------------------------|-----------------------------------------------|--------------------------------------------------------------------------------------------|------------------------|
      | **SQL Databases**          | Best for modern cloud applications.                                         | Hyperscale and serverless options available.  | Ideal for scalable, managed databases with minimal administrative overhead.                | - **Single database**: Isolated database with dedicated resources. <br> - **Elastic pool**: Multiple databases sharing a set of resources for cost efficiency. <br> - **Database server**: A logical server to manage multiple databases. |
      | **SQL Managed Instances**  | Best for most migrations to the cloud.                                      | Lift-and-shift ready.                         | Suitable for migrating existing SQL Server workloads to Azure with minimal changes.        | - **Single instance**: A fully managed instance of SQL Server in the cloud. <br> - **Single instance - Azure Arc**: Extends Azure management and services to any infrastructure, enabling hybrid cloud scenarios. |
      | **SQL Virtual Machines**   | Best for migrations and applications requiring OS-level access.             | Full control over OS and SQL Server settings. | Ideal for custom OS or SQL Server configurations, or applications requiring OS-level access. | - SQL Server 2022 on Windows Server 2022 <br> - Free SQL Server License: SQL Server 2022 Developer on Windows Server 2022 <br> - SQL Server 2022 Enterprise on Windows Server 2022 <br> - SQL Server 2022 Standard on Windows Server 2022 <br> - SQL Server 2022 Web on Windows Server 2022 <br> - SQL Server 2022 on RHEL 8 <br> - Free SQL Server License: SQL Server 2022 Developer on Red Hat Enterprise Linux HA 8.6 <br> - SQL Server Enterprise HA Edition: Red Hat Enterprise Linux HA <br> - SQL Server Standard Edition: Red Hat Enterprise Linux HA |


       - If you don't have a SQL server in place, please create one.
          - Fill in the required details like server name, admin login, and password.
       
             <img width="550" alt="image" src="https://github.com/user-attachments/assets/ecf6b6aa-e1d9-4e38-82ae-8664d4002b69">
             
             | Topic                        | Description                                                                                                                                                                                                 |
             |------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
             | **Availability of Services** | Not all Azure services and features are available in every region. It's important to check the [Azure Products by Region page](https://azure.microsoft.com/en-us/explore/global-infrastructure/products-by-region/) to see which services are available in your desired region.                     |
             | **Redundancy Options**       | Azure SQL Database supports local and zonal redundancy options. Local redundancy provides resiliency within a datacenter, while zonal redundancy improves resiliency by protecting against outages of an availability zone within a region. |
             | **Compliance and Data Residency** | Different regions have specific compliance and data residency requirements. Azure regions are designed to meet these requirements, ensuring that your data stays within the specified geographic boundaries. |
             | **Virtual Network Rules**    | For SQL Database, virtual network rules must reference subnets hosted in the same geographic region as the database. Each server can have up to 128 ACL entries for any virtual network.                     |
             | **Authentication Methods**   | - **SQL Authentication**: Users connect using a username and password. <br/> - **Microsoft Entra Authentication**: Users authenticate using their Microsoft Entra ID credentials, which supports enhanced security features like multifactor authentication and conditional access policies. |
             | **Microsoft Entra Admin**    | The Microsoft Entra admin center is a unified portal for managing Microsoft Entra products, including identity and access management solutions. It provides tools for user and group management, device management, application management, security and compliance, and identity governance. This centralized interface helps streamline administrative tasks and enhances security. |

   - Choose the pricing tier and performance level that suits your needs.
       
      <img width="370" alt="image" src="https://github.com/user-attachments/assets/26488350-7622-494e-8980-262f78b663e3">

      | Topic                          | Description                                                                                                                                                                                                 |
      |--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
      | **SQL Elastic Pool**           | SQL Elastic Pools are a cost-effective solution for managing and scaling multiple databases with varying and unpredictable usage demands. Databases in an elastic pool share a set number of resources on a single server, allowing for efficient resource utilization and cost savings. |
      | **Benefits of SQL Elastic Pool** | - **Cost Efficiency**: Aggregate resources in an elastic pool to leverage economies of scale. <br> - **Flexibility**: Databases within a pool can auto-scale within the limits of the pool. <br> - **Simplified Management**: Manage a group of databases as a single entity, reducing administrative overhead. |
      | **Workload Environment Differences** | - **Development**: Environment where developers write and test code. It's a sandbox for experimentation and initial testing. <br> - **Production**: Live environment where the final code is deployed for end-users. It must be stable and reliable. <br> **Key Differences from Azure Perspective**: <br> - **Development**: Typically uses lower-cost, lower-performance configurations. Suitable for testing and development purposes. <br> - **Production**: Uses higher-cost, higher-performance configurations. Optimized for reliability, performance, and security. |
      | **Backup Storage Redundancy**  | - **Locally Redundant Storage (LRS)**: Replicates data three times within a single physical location in the primary region. <br> - **Zone-Redundant Storage (ZRS)**: Replicates data synchronously across three Azure availability zones in the primary region. <br> - **Geo-Redundant Storage (GRS)**: Replicates data asynchronously to a secondary region, providing high durability across regions. |

      - Compute and Storage options:
   
         | Category              | Description                                                                                       | Options                                                                                     |
         |-----------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
         | **Region**            | The geographic location where your Azure SQL Database will be hosted. Choosing the right region can impact performance, compliance, and cost. | Examples: East US, West US, North Europe, Southeast Asia, Australia East, etc.              |
         | **Type**              | The deployment type for your database. This determines how the database is managed and scaled.    | - **Single Database**: Isolated database with dedicated resources. <br> - **Elastic Pool**: Multiple databases sharing a set of resources. <br> - **Managed Instance**: Fully managed instance with near 100% compatibility with on-premises SQL Server. |
         | **Purchase Model**    | The pricing model for your database. This affects how you are billed for compute and storage resources. | - **vCore**: Flexible model allowing independent scaling of compute, memory, and storage. <br> - **DTU**: Bundled model combining compute, memory, and I/O resources into pre-configured units. |
         | **Service Tier**      | The performance and availability level for your database.                                         | - **General Purpose**: Balanced and scalable compute and storage options. <br> - **Business Critical**: High performance and high availability with built-in HA and replication. <br> - **Hyperscale**: Suitable for large databases with dynamic scaling needs. |
         | **Compute Tier**      | The allocation method for compute resources.                                                      | - **Provisioned**: Resources are allocated and billed based on provisioned capacity. <br> - **Serverless**: Automatically scales compute resources based on workload demand and pauses during inactivity. |
         | **Hardware Type**     | The type of hardware used for the database server.                                                | - **Standard-series (Gen 5)**: Intel-based processors suitable for general-purpose workloads. <br> - **Fsv2-series**: Optimized for compute-intensive workloads with high CPU-to-memory ratio. <br> - **DC-series**: Provides confidential computing capabilities with hardware-based security. |
         | **Instance**          | The number of virtual cores (vCores) allocated to your database. More vCores provide higher compute power. | Examples: 2 vCore, 4 vCore, 6 vCore, 8 vCore, etc.                                          |
         | **Disaster Recovery** | Options for high availability and disaster recovery. This determines how your data is replicated and protected. | - **Primary or Geo Replica**: Main instance or a secondary instance in a different region for disaster recovery. <br> - **Standby Replica**: A secondary instance that can take over in case the primary instance fails. |
      
2. **Configure Networking**:
   - Set up firewall rules to allow access to your SQL Server.
   - Choose the appropriate network settings based on your security requirements.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa53de28-eba1-4214-bb81-e6e1420a458d">

      | Area                   | Options                                                                                       |
      |------------------------|-----------------------------------------------------------------------------------------------|
      | **Connectivity Method** | - **No access**: No public endpoint or private endpoint is configured. <br> - **Public endpoint**: Allows connectivity through a public endpoint. <br> - **Private endpoint**: Allows connectivity through a private endpoint. |
      | **Connection Policy**  | - **Default**: Uses Redirect policy for all client connections originating inside of Azure (except Private Endpoint connections) and Proxy for all client connections originating outside Azure. <br> - **Proxy**: All connections are proxied via the Azure SQL Database gateway. <br> - **Redirect**: Clients establish connections directly to the node hosting the database. |
      | **Encrypted Connections** | - **Minimum TLS version**: Specifies the minimum version of Transport Layer Security (TLS) required for encrypted connections. <br> - **TLS 1.0**: The first version of TLS, now considered outdated and insecure. <br> - **TLS 1.1**: An improvement over TLS 1.0, but also considered outdated. <br> - **TLS 1.2**: A widely used version that provides strong security features. It is recommended for most applications. |

3. **Configure Security**:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/1e0d9519-fd0c-43cb-a825-ceaaf27731be">
   
   | Option                                      | Description                                                                                       | Use Case                                                                                       |
   |---------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
   | **Microsoft Defender for SQL**              | Protects data using a unified security package including vulnerability assessments and advanced threat protection. | Use this to enhance the security of your SQL databases by identifying and mitigating potential vulnerabilities and threats. |
   | **Ledger**                                  | Helps maintain the integrity of data by providing cryptographic proof that it has not been tampered with. | Use this to ensure data integrity and provide tamper-evidence for critical data.               |
   | **Server Identity**                         | Allows assigning managed identities to enable central access management between the database and other Azure resources. | Use this to manage access and permissions centrally, simplifying identity management and enhancing security. |
   | **Transparent Data Encryption Key Management** | Encrypts databases, backups, and logs at rest without requiring changes to applications. <br> - **Server-level key**: Managed at the server level, providing a single key for all databases on the server. <br> - **Database-level key**: Managed individually for each database, allowing for more granular control. | Use this to protect data at rest by encrypting it, ensuring that it remains secure even if the physical media is compromised. |
   | **Elastic Resource Enclaves**               | Provides a high level of industry-leading data protection by creating a separation between the database engine process memory and the operating system or hypervisor processes. | Use this to enhance data protection by isolating the database engine process from other processes, reducing the risk of data breaches. |


4. **Configure Additional Settings**:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/6539e0ba-053d-4b9e-8b24-9a3e0d9c6e10">

   | Section                | Description                                                                                       | Options                                                                                     |
   |------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
   | **Data Source**        | Options to use an existing database.                                                              | - **None**: No existing data source. <br> - **Backup**: Use a backup of an existing database. <br> - **Sample**: Use a sample database provided by Azure. |
   | **Database Collation** | Defines rules that sort and compare data. The default database collation is SQL_Latin1_General_CP1_CI_AS. | - **Enter a collation**: Manually specify a collation. <br> - **Find a collation**: Use a search function to find and select a collation. |
   | **Maintenance Window** | Specifies the preferred maintenance window for database updates and maintenance tasks. The default is "System default (5pm to 8am)". | - **System default**: 5pm to 8am. <br> - **Custom window**: Select a preferred time window from the drop-down list. |


7. **Deploy and Manage**:
   - Use tools like SQL Server Management Studio (SSMS) or Azure Data Studio to manage your databases.
   - Implement backup and disaster recovery strategies.
   - Monitor performance and set up alerts for any issues.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
