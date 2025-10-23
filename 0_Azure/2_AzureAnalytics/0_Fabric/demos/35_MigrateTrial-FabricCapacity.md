# Migrate from Trial Workspace to Fabric (Paid) - Overview 

 Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Backup and restore semantic models with Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset)
- [REST API - Reports Export To File](https://learn.microsoft.com/en-us/rest/api/power-bi/reports/export-to-file)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Overview](#overview)
- [How to Remove All Fabric Items and Move the Workspace](#how-to-remove-all-fabric-items-and-move-the-workspace)
    - [Step 1: Identify Fabric Items](#step-1-identify-fabric-items)
    - [Step 2: Remove Fabric Items](#step-2-remove-fabric-items)
    - [Step 3: Verify Workspace Contents](#step-3-verify-workspace-contents)
    - [Step 4: Migrate the Workspace](#step-4-migrate-the-workspace)
    - [Step 5: Final Verification](#step-5-final-verification)    

</details>

## Overview 

> Many users encounter this error when attempting to reassign a workspace that was on trial or located in a different region:

```
workspace cannot be reassigned because it includes Fabric items or you're attempting to move them
across regions. This is not supported currently. Remove the Fabric items, or move the workspace
within the same region, and then try again.
```


<div align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/86aa9c42-5c66-4751-94d6-2afb6ab24b4e" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

https://github.com/user-attachments/assets/b515273a-b134-4d5c-b906-1a97c510939a

> [!NOTE]
> The region for the trial account was specified at the beginning of the sign-up process.

<div align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/e8cedea0-9769-4439-a849-ed8b097a1167" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

> Overall:
> - **Migrating workspace with only Power BI items** (`within the same region`): If the workspace contains only Power BI items (and no Fabric items), you can move the workspace to a different capacity within the same region. This process is supported and straightforward. <br/>
> - **Migrating workspace with only Power BI items** (`to a different region`): If the workspace contains only Power BI items (and no Fabric items), moving it to another region is not supported directly. However, you can perform a backup and restore of semantic models using Power BI Premium. For detailed steps, refer to the  [Backup and restore semantic models with Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset) documentation. Also, review the [Considerations and limitations](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset#considerations-and-limitations) before proceeding. <br/>
> - **Migrating workspace with both Fabric and Power BI items** (`within the same region)`: If the workspace contains both Fabric and Power BI items, you can move it from one capacity to another within the same region. This migration is supported and can be done without any special considerations.
> - **Migrating workspace with both Fabric and Power BI items** (`to a different region`): Moving workspaces that contain Fabric items to a different region is not supported. If you need to migrate such workspaces, you must first delete all Fabric artifacts. Once the workspace contains only Power BI items, you can then follow the migration process for workspaces with only Power BI items. <br/> <br/>
> If you want to read more about it please find this quick overview about [Migration from Power BI Premium (P-SKUs) to Fabric (F-SKUs)](./8_MigrationPtoFSku.md)

## How to Remove All Fabric Items and Move the Workspace

### Step 1: Identify Fabric Items

1. **Access the Workspace**: Open the workspace you want to migrate.
2. **List Fabric Items**: Identify all Fabric items within the workspace. These may include datasets, notebooks, data pipelines, lakehouses, and other artifacts created using Fabric.

> For example:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/3fab43b2-893c-4f89-a58b-d73cb5d9f090" />

### Step 2: Remove Fabric Items

1. **Backup Data**: If necessary, back up any data or reports you need to retain.

    > Also, depending on the object, each item has a specific method to extract its code or configuration details. For example a `Copy Job`:
 
      https://github.com/user-attachments/assets/7871a6de-405b-4a02-a8f8-c3ab8aaf5511

    > E.g `data pipeline`:

     https://github.com/user-attachments/assets/e5616aeb-3594-4324-97c4-0975d03bf81a

3. **Delete Fabric Items**: 
   - Navigate to each Fabric item.
   - Select the item and choose the delete option.
   - Confirm the deletion.

      https://github.com/user-attachments/assets/b805728c-a7ba-4b0b-b0f4-f14a9130aee7

### Step 3: Verify Workspace Contents

1. **Check Remaining Items**: Ensure that only Power BI items remain in the workspace.
2. **Double-Check**: Verify that no Fabric items are left to avoid migration issues.

### Step 4: Migrate the Workspace

1. **Within the Same Region**:
   - **Move to Different Capacity**: If you are migrating within the same region, you can move the workspace to a different capacity directly.
   - **Steps**:
     - Go to the workspace settings. Under license.
     - Select the new capacity.
     - Save the changes.

2. **To a Different Region**:
   - **Backup and Restore**: If you are migrating to a different region, follow these steps:
     - **Backup Semantic Models**: Use Power BI Premium to back up the semantic models.
     - **Restore in New Region**: Restore the backed-up models in the new region.
     - **Steps**:
       - Refer to the [Backup and restore semantic models with Power BI Premium documentation](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset) for detailed instructions.
       - Review the [Considerations and limitations](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-backup-restore-dataset#considerations-and-limitations) before proceeding.
       - Go to the workspace settings. Under license.
       - Select the new capacity.
       - Save the changes.

           https://github.com/user-attachments/assets/b25c0b7b-ec83-471a-bc0c-010ca28d5f7c

### Step 5: Final Verification
1. **Check Migration**: Ensure that all items have been successfully migrated.
2. **Test Functionality**: Verify that all reports and dashboards are functioning correctly in the new capacity or region.



<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
