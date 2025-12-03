# Microsoft Fabric: Power Bi How to Manage Accesss - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

## References 

<details>
<summary><b>Table of References </b> (Click to expand)</summary>

- [Roles in workspaces in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/roles-workspaces#-workspace-roles)
- [Permission model](https://learn.microsoft.com/en-us/fabric/security/permission-model)
- [Row-level security (RLS) with Power BI](https://learn.microsoft.com/en-us/fabric/security/service-admin-row-level-security)
  
</details>


## Overview 

> Power BI offers a comprehensive suite of analytics tools for organizational insights. You can connect to hundreds of data sources, simplifies data preparation, and facilitates ad hoc analysis. Power BI allows you to produce beautiful reports, then publish them for your organization to consume on the web and across mobile devices.

Types of Access in Power BI:

| **Product**           | **Description**                                                                 |
|-----------------------|---------------------------------------------------------------------------------|
| Power BI Desktop      | A Windows application for creating reports and data visualizations on your local computer. |
| Power BI Service      | An online SaaS (Software as a Service) where you can share and view dashboards and reports. |
| Power BI Mobile Apps  | Available on Windows, iOS, and Android devices for viewing reports and dashboards on the go. |


Roles and Permissions:

- **Admin**: Full control over the Power BI tenant, including user management and tenant settings.
- **Member**: Can edit and manage content within a workspace.
- **Contributor**: Can add and edit content, but cannot manage workspace settings.
- **Viewer**: Can only view content within a workspace.

Licensing:

| **License Type**     | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| Power BI Free        | Limited to individual use with no sharing capabilities.                         |
| Power BI Pro         | Allows sharing and collaboration, required for both creators and consumers of content. |
| Power BI Premium     | Provides dedicated capacity and advanced features, does not require Pro licenses for content consumers. |

Data Connectivity:

| **Category**         | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| Files                | Excel, CSV, XML, JSON                                                           |
| Databases            | SQL Server, Oracle, MySQL, PostgreSQL                                           |
| Online Services      | SharePoint, Dynamics 365, Google Analytics, Salesforce                          |
| Other Sources        | Web, OData, Active Directory                                                    |

Creating and Publishing Reports:

| **Step**             | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| Connect to Data      | Use Power BI Desktop to connect to your data source.                            |
| Transform Data       | Clean and transform your data using Power Query.                                |
| Create Visuals       | Build reports with interactive visuals.                                         |
| Publish              | Publish your reports to the Power BI service for sharing.                       |

Sharing and Security:
- **Row-Level Security (RLS)**: Restricts data access for given users, defined within roles.
- **Content Packs**: A way to share datasets, reports, and dashboards with other users.
- **Apps**: A collection of dashboards and reports bundled together and shared with users.

Consuming Reports:

| **Method**           | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| Power BI Service     | View and interact with reports in a web browser.                                |
| Power BI Mobile Apps | Access reports on mobile devices.                                               |
| Embedded             | Integrate reports into your own applications using Power BI Embedded.           |


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
