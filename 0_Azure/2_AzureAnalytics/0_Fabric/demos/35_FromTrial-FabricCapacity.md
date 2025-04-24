# Migrate from Trial Workspace to Fabric (Paid) - Overview 

 Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-08

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>


</details>

> Many users encounter this error when attempting to reassign a workspace that was on trial or located in a different region:

```
workspace cannot be reassigned because it includes Fabric items or you're attempting to move them
across regions. This is not supported currently. Remove the Fabric items, or move the workspace
within the same region, and then try again.
```

<img width="951" alt="image" src="https://github.com/user-attachments/assets/86aa9c42-5c66-4751-94d6-2afb6ab24b4e" />


> Overall:
> - **Migrating workspace with only Power BI items** (`within the same region`): If the workspace contains only Power BI items (and no Fabric items), you can move the workspace to a different capacity within the same region. This process is supported and straightforward. <br/>
> - **Migrating workspace with only Power BI items** (`to a different region`): If the workspace contains only Power BI items (and no Fabric items), moving it to another region is not supported directly. However, you can perform a backup and restore of semantic models using Power BI Premium. For detailed steps, refer to the  [Backup and restore semantic models with Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset) documentation. Also, review the [Considerations and limitations](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset#considerations-and-limitations) before proceeding. <br/>
> - **Migrating workspace with both Fabric and Power BI items** (`within the same region)`: If the workspace contains both Fabric and Power BI items, you can move it from one capacity to another within the same region. This migration is supported and can be done without any special considerations.
> - **Migrating workspace with both Fabric and Power BI items** (`to a different region`): Moving workspaces that contain Fabric items to a different region is not supported. If you need to migrate such workspaces, you must first delete all Fabric artifacts. Once the workspace contains only Power BI items, you can then follow the migration process for workspaces with only Power BI items. <br/> <br/>
> If you want to read more about it please find this quick overview about [Migration from Power BI Premium (P-SKUs) to Fabric (F-SKUs)](./demos/8_MigrationPtoFSku.md)





<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
