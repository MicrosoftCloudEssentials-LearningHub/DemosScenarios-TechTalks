# Power Bi Licensing - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Interact with the Power BI service as a Free user](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-features)
- [Power Bi Free User Feature List](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-features#feature-list)
- [Power BI pricing Free, Pro, PPU, Embedded, Fabric](https://www.microsoft.com/en-us/power-platform/products/power-bi/pricing?msockid=38ec3806873362243e122ce086486339#tabs-pill-bar-oca31b12_tab0)
- [Save costs with Microsoft Fabric Capacity reservations](https://learn.microsoft.com/en-us/azure/cost-management-billing/reservations/fabric-capacity)
- [Comparision Table between Fabric, Power Bi and vcores](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#capacity)
- [Table - Workspace license mode](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#workspace)
- [Table - Per user licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#per-user-licenses)
- [Fabic -Features parity list](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features#features-parity-list)
- [Embedded - prerequisites](https://learn.microsoft.com/en-us/power-bi/developer/embedded/embed-organization-app#prerequisites)
- [Embedded - Which SKU should I use?](https://learn.microsoft.com/en-us/power-bi/developer/embedded/embedded-capacity#which-sku-should-i-use)
- [Distribute Power BI content to external guest users with Microsoft Entra B2B](https://learn.microsoft.com/en-us/power-bi/enterprise/service-admin-azure-ad-b2b#guest-users-who-can-edit-and-manage-content)
- [External data sharing in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/governance/external-data-sharing-overview)
- [Pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)
- [Power BI Premium Per User](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-per-user-faq)
- [Power BI service per-user and capacity-based licenses](https://learn.microsoft.com/en-us/power-bi/fundamentals/service-features-license-type)
- [Permission model](https://learn.microsoft.com/en-us/fabric/security/permission-model)
- [Roles in workspaces in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/fundamentals/roles-workspaces)

</details>

> [!IMPORTANT]
> *SKUs that are smaller than F64 require a Pro or Premium Per User (PPU) license, or a Power BI individual trial to consume Power BI content. `To distribute content through Power BI apps, we require Premium capacity (F64 or higher) so that free users can access the content without needing a Pro license.`

| **Capacity**          | **Description**                                                                 | **Usage** | **Capabilities** | **User Types** | **When to Use** |
|-----------------------|---------------------------------------------------------------------------------|-----------|------------------|----------------|-----------------|
| **Power BI Embedded (A)** | A solution for embedding Power BI reports and dashboards into applications.     | External users | - Embedding interactive reports and dashboards<br>- APIs for embedding control<br>- Scalable with pay-as-you-go pricing | - ISVs (Independent Software Vendors)<br>- Developers integrating analytics into applications without requiring users to have a Power BI license <br/> - Embedding Power BI reports into SharePoint is a common practice. | Use when you need to integrate interactive reports and dashboards directly into your applications for a seamless user experience. |
| **Microsoft Fabric (F)**  | A comprehensive solution integrating various Microsoft analytics services.      | Internal users | - Integration of data engineering, warehousing, real-time analytics, data science, and BI<br>- Unified governance and security | - Organizations seeking an end-to-end data platform for diverse workloads<br>- Companies needing a unified ecosystem from data ingestion to insights | Use when you need a unified analytics platform that integrates multiple Microsoft services for enhanced data governance and seamless workflow. |
| **Power BI Premium (P)**  | Provides advanced analytics capabilities and larger data capacity.              | Internal users | - Advanced features like AI, paginated reports, dataflows<br>- Dedicated cloud resources<br>- Incremental refreshes and enhanced data security | - Enterprise users needing advanced analytics across the organization<br>- Organizations requiring large-scale deployments with dedicated capacity | Use when you require advanced analytics, larger data capacity, and AI integration for comprehensive data analysis and insights. |

> [!NOTE]
> The embedding option is not available for sharing content with internal users. We need to use the F SKU license (Fabric) option. 

## Embedding Power BI reports into SharePoint

> [!IMPORTANT]
> External users can access SharePoint Online content `if they are invited and authenticated.` External users `do not need a SharePoint license if they are accessing content shared with them.` <br/>
> Types of External Users: <br/>
> - Authenticated External Users: These users are invited to your SharePoint site and have a Microsoft account or an organizational account. They can access shared content without needing a SharePoint license. <br/>
> - Anonymous Users: These users can access content if it is shared via anonymous links. However, `this method is less secure and should be used cautiously. Not recommended` <br/> 
> If you are embedding Power BI reports into SharePoint, external users accessing these reports do not need a Power BI license. The embedding is handled through Power BI Embedded, which allows access without individual licenses.

1. **Publish the Report to Power BI Service**: Ensure your report is published to the [Fabric/Power BI](https://app.fabric.microsoft.com) service.
2. **Get the Embed Code**:
   - In Power BI service, open the report you want to embed.
   - Click on the `File` menu and select `Embed report`.
   - Choose your prefered option.
  
      <img width="949" alt="image" src="https://github.com/user-attachments/assets/9232bd3a-577e-450c-8df8-d5389b0fcf1a" />

> Embedding Options:

| **Option** | **Description** |
|------------|-----------------|
| **SharePoint Online** | Allows embedding the report directly into SharePoint Online pages. |
| **Website or Portal** | Provides options to embed the report into websites or portals. |
| **Developer Playground** | Offers tools and resources for developers to test and embed reports in various applications. |

### How Developer Playground looks like 

https://github.com/user-attachments/assets/87ccb8e4-f959-481e-8287-6efb6e0603da

## Embedding Pricing Calculator

https://github.com/user-attachments/assets/ccf99d57-bf1e-4267-afb7-c5a6bc539789


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
