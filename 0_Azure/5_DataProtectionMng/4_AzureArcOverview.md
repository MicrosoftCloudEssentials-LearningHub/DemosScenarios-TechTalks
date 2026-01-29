# Azure Arc Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Azure Arc enables you to manage and monitor resources across different environments using Azure's centralized tools and services

<img width="550" alt="image" src="https://github.com/user-attachments/assets/d7f3ccfc-b11a-4788-ab53-1d7b2ae3d216">

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Enabling hybrid solutions on any cloud, on any infrastructure](https://techcommunity.microsoft.com/t5/azure-arc-blog/enabling-hybrid-solutions-on-any-cloud-on-any-infrastructure/ba-p/2476120)
- [Azure Arc: Extending Azure management to any infrastructure](https://azure.microsoft.com/en-us/blog/azure-arc-extending-azure-management-to-any-infrastructure/)
- [Connect on-premises machines - Microsoft Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/quickstart-onboard-machines)
- [3 steps to secure your multicloud and hybrid infrastructure with Azure Arc](https://www.microsoft.com/en-us/security/blog/2022/03/29/3-steps-to-secure-your-multicloud-and-hybrid-infrastructure-with-azure-arc/)
- [Azure Arc-enabled server configurations](https://learn.microsoft.com/en-us/azure/architecture/hybrid/azure-arc-hybrid-config)
- [Configure Microsoft Defender for Cloud for Azure Arc-enabled servers](https://learn.microsoft.com/en-us/training/modules/configure-defender-cloud-azure-arc-enabled-servers/)
- [Overview of Azure Connected Machine agent](https://learn.microsoft.com/en-us/azure/azure-arc/servers/agent-overview)
- [What are Azure Arc-enabled data services?](https://learn.microsoft.com/en-us/azure/azure-arc/data/overview)
- [Create Azure Arc data controller from Azure portal - Direct connectivity mode](https://learn.microsoft.com/en-us/azure/azure-arc/data/create-data-controller-direct-azure-portal)
- [Create Azure Arc data controller in direct connectivity mode using CLI](https://learn.microsoft.com/en-us/azure/azure-arc/data/create-data-controller-direct-cli?tabs=windows)
  
</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Arc Agents](#arc-agents)
    - [Azure Connected Machine Agent](#azure-connected-machine-agent)
    - [Azure Arc Data Controller](#azure-arc-data-controller)

</details>

## Arc Agents 

> The table below provides a comparison of the two agents, highlighting their specific uses and the types of resources they manage:

| **Aspect** | **Azure Arc Data Controller** | **Azure Connected Machine Agent** |
|------------|-------------------------------|-----------------------------------|
| **Purpose** | Specifically for managing data services like SQL Server and PostgreSQL. | General-purpose management and monitoring of Windows and Linux machines. |
| **Key Features** | - Centralized management of SQL Server and PostgreSQL instances.<br>- Advanced data management, monitoring, and security.<br>- Integration with Azure Monitor, Azure Policy, and Azure Security Center. | - Extends Azure management capabilities to on-premises and multi-cloud VMs.<br>- Performance and health monitoring using Azure Monitor.<br>- Security and compliance management with Azure Security Center. |
| **Managed Resources** | - SQL Server instances.<br>- PostgreSQL instances.<br>- Azure Arc-enabled SQL Managed Instances.<br>- Azure Arc-enabled PostgreSQL Hyperscale. | - Windows VMs.<br>- Linux VMs.<br>- On-premises servers.<br>- VMs in other cloud environments (AWS, Google Cloud, etc.). |
| **Example Use Case** | - **Hybrid Cloud Deployment**: A company manages SQL Server instances across on-premises and other cloud environments using a single Azure Arc Data Controller. | - **Multi-Cloud Management**: An organization manages VMs running in AWS, Google Cloud, and on-premises by installing the Azure Connected Machine Agent on each VM. |
| **Setup Steps** | 1. Create an Azure Arc-enabled data services extension.<br>2. Create a custom location.<br>3. Deploy the data controller using the Azure CLI or Azure Portal. | 1. Install the Connected Machine agent on your VM.<br>2. Register the machine with Azure Arc.<br>3. Configure management and monitoring settings as needed. |

### Azure Connected Machine Agent

> The Azure Connected Machine agent allows you to manage both Windows and Linux machines that are hosted outside of Azure, whether on your corporate network or with other cloud providers. The agent package includes several logical components bundled together:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/0086c732-307e-4573-a529-8b5bde31e558">

### Azure Arc Data Controller

> **Azure Arc Data Controller** is a key component of Azure Arc-enabled data services. <br/>
> - **Centralized Management**: It provides a unified management experience for data services across on-premises, multi-cloud, and edge environments <br/>
> - **Deployment Modes**: You can deploy the data controller in either direct connectivity mode or indirect connectivity mode, depending on your network setup and requirements <br/>
> - **Data Services**: It supports running Azure data services like SQL Managed Instance and PostgreSQL Hyperscale on any Kubernetes cluster <br/>
> - **Monitoring and Security**: The data controller helps in monitoring, managing, and securing your data services with integrated dashboards for metrics and logs

Find below some general guides around:
- [How Arc works for SQL Server](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/3_ArcSQLServerOverview.md)
- [How to set up Arc for different SQL environments](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/1_AzureData/1_Databases/demos/5_ArcSQLHowtoSetup.md)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
