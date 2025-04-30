# Migration from Power BI Pro/PPU to Fabric (F-SKUs) - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-30

----------

> [!IMPORTANT]
> 🔺 This approach is around `reassign workspaces without tenant migration`, if you decide to migrate the tenant in the future, you can do so with the workspaces already assigned to the new capacity.

> $${\color{red}Same\ geo\ but\ across\ region}$$ The `multi-geography setup` in Microsoft Fabric allows you to deploy content to data centers in regions other than the home region of your Fabric tenant. This feature is particularly useful for multinational customers who need to address regional, industry-specific, or organizational data residency requirements.` In your example, if you have the US as the geography with Central US and West US 2 as regions, you can set up a Fabric capacity reservation in one of these regions. Once a capacity is created, it remains in that region, and any workspaces created under it will have their content stored in that region`. This approach ensures that `you don't need to move the home region`, which can simplify management and compliance. Click [here for more information about it](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)

https://github.com/user-attachments/assets/16fd8e90-22cc-48d3-8dce-e79e4ee9789b

