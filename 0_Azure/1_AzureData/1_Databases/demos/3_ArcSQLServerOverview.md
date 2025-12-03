# Arc SQL Server - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

<details>
<summary><b>Table of Wiki </b> (Click to expand)</summary>

- [Overview - SQL Server enabled by Azure Arc](https://learn.microsoft.com/en-us/sql/sql-server/azure-arc/overview?view=sql-server-ver16)
- [Benefit from Azure Arc-enabled SQL Managed Instance](https://techcommunity.microsoft.com/t5/azure-arc-blog/benefit-from-azure-arc-enabled-sql-managed-instance-even-without/ba-p/3259167)
- [Public preview: Bring enhanced manageability to your SQL Server](https://azure.microsoft.com/en-us/updates/public-preview-bring-enhanced-manageability-to-your-sql-server-anywhere-with-azure-arc/)
- [Best practices assessment for Azure Arc Enabled SQL Server](https://techcommunity.microsoft.com/t5/azure-arc-blog/evaluate-sql-server-configuration-using-best-practices/ba-p/3773382)
- [Prerequisites - SQL Server enabled by Azure Arc](https://learn.microsoft.com/en-us/sql/sql-server/azure-arc/prerequisites?view=sql-server-ver16&tabs=azure)
- [Understanding Azure Arc Enabled SQL Server](https://learn.microsoft.com/en-us/shows/data-exposed/understanding-azure-arc-enabled-sql-server)
- [Plan and deploy Azure Arc-enabled servers - Azure Arc](https://learn.microsoft.com/en-us/azure/azure-arc/servers/plan-at-scale-deployment)
- [SQL Managed Instance enabled by Azure Arc Overview](https://learn.microsoft.com/en-us/azure/azure-arc/data/managed-instance-overview)
- [Analyze metrics with Azure Monitor metrics explorer](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/analyze-metrics#pin-charts-to-dashboards)
- [Administer SQL Server with Azure Arc - Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/hybrid/azure-arc-sql-server)
- [SQL Server enabled by Azure Arc](https://learn.microsoft.com/en-gb/sql/sql-server/azure-arc/overview?view=sql-server-ver16#architecture)

</details>

## Overview 

> Once Azure Arc is connected, you can manage your SQL Server instances from the Azure portal, allowing you to view detailed inventory, run cross-SQL Server queries, and optimize configurations based on best practices

<img width="550" alt="image" src="https://github.com/user-attachments/assets/5ce51be3-d5e3-441f-b1ec-d7451b825320">

| **Component**                        | **Description**                                                                                   |
|--------------------------------------|---------------------------------------------------------------------------------------------------|
| **SQL Assets**                       | SQL Server instances enabled by Azure Arc, located on-premises, in multi-cloud, or at the edge.   |
| **Arc-enabled Data Services**        | Services that connect and manage the SQL Server instances, including automated backups, security updates, and monitoring. |
| **Arc SQL Extension**                |   - `Windows Local Package`: Package installed on Windows SQL Server instances for connectivity and management. <br/>   - `Linux Local Package`: Package installed on Linux SQL Server instances for connectivity and management. |
| **Arc Agent: Connected Machine Agent** | Agent facilitating communication between SQL Server instances and Azure.                          |
| **Enterprise Firewall and Proxy**    |   `Outbound Only on Port 443`: Ensures secure outbound communication from on-premises to Azure using port 443. |
| **Control Plane**                    | Managed by Azure Resource Manager (ARM) and includes Microsoft Entra Identity for authentication. |
| **Hybrid Connections**               | Managed through Microsoft Entra ID/Service Principal for secure connections.                      |
| **Azure Resource Manager (ARM)**     | Manages resources across various environments using ARM templates or other methods.               |
| **Microsoft.AzureData Resource Provider** | Manages data services enabled by Azure Arc, handling tasks like inventory management, billing, and licensing. |

## Where can it be enabled in SQL context

| Environment             | Description                                                                                                                       |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **On-Premises**         | You can connect your on-premises SQL Server instances to Azure Arc. This allows you to manage and monitor them through the Azure portal, providing a unified management experience. |
| **Azure**               | Azure Arc can also be used with SQL Server instances running on Azure Virtual Machines (VMs). This extends the capabilities of Azure Arc to your cloud-based SQL Servers, enabling centralized management and governance. |
| **Other Clouds**        | Azure Arc supports SQL Server instances running in other cloud environments, such as AWS or Google Cloud. This ensures you can manage your SQL Servers across different cloud providers from a single pane of glass. |
| **AKS**                 | Running SQL Server in Azure Kubernetes Service (AKS) allows for containerized deployment, scalability, resilience, and integration with other Azure services. This provides a robust, scalable, and flexible solution for managing SQL Server workloads. |
| **Edge Locations**      | SQL Server instances running in edge locations, such as retail stores or remote offices, can be connected to Azure Arc. This allows for centralized management and monitoring of these distributed instances. |
| **Azure VMware Solution** | SQL Server instances running on Azure VMware Solution can also be managed through Azure Arc. This provides a consistent management experience for SQL Servers running in a VMware environment. |
| **Azure Stack HCI**     | SQL Server instances running on Azure Stack HCI (Hyper-Converged Infrastructure) can be connected to Azure Arc. This enables hybrid cloud scenarios where you can manage on-premises resources alongside Azure resources. |

## Benefits 

| **Benefit**                     | **Description**                                                                                                                                       |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Unified Management**          | Manage all SQL Server instances from a single point of control in the Azure portal, including on-premises, multi-cloud, and edge environments.         |
| **Enhanced Security**           | Use Microsoft Entra ID for authentication, providing enhanced security features like multifactor authentication (MFA) and single sign-on (SSO).        |
| **Consistent Updates and Patching** | Receive frequent updates, including servicing patches and new features, ensuring SQL Server instances are always up-to-date with the latest enhancements. |
| **Scalability and Flexibility** | Deploy, manage, and monitor Azure SQL Managed Instance in various environments, including on-premises, edge locations, and public clouds using Kubernetes. |
| **Cloud Benefits in Any Environment** | Extend cloud benefits such as automated backups, high availability, and self-service provisioning to SQL Server instances, regardless of hosting location. |
| **Improved Operational Insights** | Gain comprehensive operational insights across all databases using tools like Azure Monitor, aiding in proactive management and troubleshooting.         |
| **Best Practices Assessment**   | Optimize the configuration of SQL Server instances for performance and security with best practices assessments offering specific recommendations.       |
| **Connectivity Modes**          | Supports both directly connected and indirectly connected modes, benefiting from most services even with intermittent or no internet connectivity.       |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
