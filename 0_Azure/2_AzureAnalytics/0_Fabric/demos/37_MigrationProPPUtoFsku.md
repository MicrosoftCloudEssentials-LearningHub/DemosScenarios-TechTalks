# Migration from Power BI Pro/PPU to Fabric (F-SKUs) - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Microsoft Fabric concepts and licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses)
- [Microsoft Fabric features parity](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [What Makes It Straightforward?](#what-makes-it-straightforward) (How it works)
- [Key Considerations](#key-considerations)


</details>


>  If your workspaces currently `contain only Power BI items`, migrating from Power BI Pro or Premium Per User (PPU) to Microsoft Fabric (F-SKUs) can be relatively straightforward, but there are a few important considerations please read below.

| Pro Workspace | PPU workspace |
| --- | --- | 
| <img width="550" alt="image" src="https://github.com/user-attachments/assets/9419ee70-3fe6-4676-b94b-b2a080bc5aea" /> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/20ebbca1-d1e5-446c-b713-2474dba714e6" /> |

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

## What Makes It Straightforward? 

> - Power BI items are fully supported in Fabric capacities (F-SKUs), so you don’t need to refactor or convert the content itself. <br/>
> - You can assign Fabric capacity to existing workspaces, and they will continue to function with enhanced performance and scalability. <br/>
> - No re-licensing of content is needed—users with Pro or PPU licenses can still access content in Fabric workspaces, depending on the SKU size. 

https://github.com/user-attachments/assets/69891a7f-2777-44f7-853b-0afa74d5614e

## Key Considerations

| **Consideration**              | **Details** |
|------------------------|-------------|
| **SKU Size Matters**   | - SKUs below F64 require users to have Power BI Pro or PPU licenses to view content.<br>- SKUs F64 and above support broader Fabric features and allow free users to view Power BI content if configured properly. |
| **Capacity Assignment**| You’ll need to assign the Fabric capacity to each workspace manually or via script. |

> Reassign Capacity (Manual Approach):

1. **Select Workspace**: Click on the workspace you want to migrate. This will open the workspace settings.
2, **Change Capacity**: In the workspace settings, look for the `Capacity` section. You will see an option to change the capacity assignment.
3. **Select Fabric SKU**: From the dropdown menu, select the new Fabric SKU that you have purchased.
 4. **Save Changes**: Click "Save" to apply the changes. The workspace will now be reassigned to the new Fabric SKU.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/3587658e-50b8-484a-b048-07de018a15fe">

> Reassign Capacity (Bulk Assignment):

1. Use the bulk assignment feature in the Admin Portal to reassign multiple workspaces at once.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/4c517df9-c79a-41bd-a21d-f0fb1b425aad">
    
2. Verify that all workspaces are correctly reassigned.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/1a6cbfdf-cde3-4eb4-a7d8-f66a28094059">

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-366-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
