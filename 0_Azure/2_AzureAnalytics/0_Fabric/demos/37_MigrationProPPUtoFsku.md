# Migration from Power BI Pro/PPU to Fabric (F-SKUs) - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-30

----------

> [!IMPORTANT]
> 🔺 This approach is around `reassign workspaces without tenant migration`, if you decide to migrate the tenant in the future, you can do so with the workspaces already assigned to the new capacity. 

> [!NOTE]
> Tenant migration is typically done if your current data region is not optimal for compliance, performance, or data residency requirements. `You cannot move your Power BI tenant to another region on your own. You must work with Microsoft Support to initiate and complete the process.` <br/> <br/>
> Please read [Move between regions](https://learn.microsoft.com/en-us/power-bi/support/service-admin-region-move#can-i-migrate-or-merge-my-power-bi-tenant-into-a-different-tenant-for-example-because-of-a-company-merger) to understand the process. Also, click here to learn how to [Request a tenant region move](https://learn.microsoft.com/en-us/power-bi/support/service-admin-region-move#request-a-region-move). <br/>
> - Microsoft Support will manage the actual migration process.  
> - However, **you are responsible** for backing up your data beforehand and restoring it afterward.  
> - If you encounter any issues during backup or restore, Microsoft Support can help troubleshoot.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/8b647468-75c5-4a5e-9a76-8c6a8cb64c8b" />

> $${\color{red}Same\ geo\ but\ across\ region}$$ The `multi-geography setup` in Microsoft Fabric allows you to deploy content to data centers in regions other than the home region of your Fabric tenant. This feature is particularly useful for multinational customers who need to address regional, industry-specific, or organizational data residency requirements.` In your example, if you have the US as the geography with Central US and West US 2 as regions, you can set up a Fabric capacity reservation in one of these regions. Once a capacity is created, it remains in that region, and any workspaces created under it will have their content stored in that region`. This approach ensures that `you don't need to move the home region`, which can simplify management and compliance. Click [here for more information about it](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)

https://github.com/user-attachments/assets/16fd8e90-22cc-48d3-8dce-e79e4ee9789b

