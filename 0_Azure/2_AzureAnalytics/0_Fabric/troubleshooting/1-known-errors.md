# Fabric known errors - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!IMPORTANT]
> Here is a brief overview of error messages and their solutions.

<details>
<summary><b>List of References </b> (Click to expand)</summary>
  
- [What is the Microsoft Fabric Capacity Metrics app?](https://learn.microsoft.com/en-us/fabric/enterprise/metrics-app)
- [Manage workspaces - Admin portal](https://learn.microsoft.com/en-us/fabric/admin/portal-workspaces)
- [Manage your Fabric capacity](https://learn.microsoft.com/en-us/fabric/admin/capacity-settings?tabs=power-bi-premium)
- [Install the Microsoft Fabric capacity metrics app](https://learn.microsoft.com/en-us/fabric/enterprise/metrics-app-install?tabs=1st)
- [Ways to collaborate and share in Power BI](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-how-to-collaborate-distribute-dashboards-reports)
- [Interact with the Power BI service as a Free user](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-features)

</details>

<details>
<summary><b>List of Errors </b> (Click to expand)</summary>
  
- [Don't have access](#dont-have-access)
- [Cannot load model](#cannot-load-model)
- [Could not connect to the data source](#could-not-connect-to-the-data-source)
- [Upgrade your Power BI license](#upgrade-your-power-bi-license)
- [Sporadic Access Error in Premium Workspace with Free Users](#sporadic-access-error-in-premium-workspace-with-free-users)

</details>

## Don't have access 

```
You don't have access to this content
Please try again later or contact support. If you contact support, please provide these details
```

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/8ad0d196-d4ee-4b47-8345-01d9c71dccdd" />
</p>

> [!TIP]
> Please ensure that the user is granted the appropriate permissions, whether it be for the workspace, app, or the report itself.

## Cannot load model

```
Couldn't load the model schema associated with this report. Make sure you have a connection to the server, and try again.
Please check the technical details for more information. If you contact support, please provide these details.
```

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/7b824ef0-f4b1-4cfa-af32-89864751bdff" />
</p>

> [!TIP]
> Please ensure your Fabric capacity is on.

## Could not connect to the data source 

```
There was an error communicating with Analysis Services. Please verify that the data source is available and your credentials are correct.

If you contact support, please provide these details.
```

> [!TIP]
> If you encounter these errors, it's necessary to grant the appropriate `(semantic model, sql analytics endpoint, and the app` permissions for access.

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/7361815f-7a53-4ae7-80f9-5bd6e3033b59" />
</p>

<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/05fac487-647a-48c2-b2b9-d9f1f0b172ea" />
</p>

Let's say you want only `viewer` permissions:

1. Need to give access to the lakehouse/sql analytics endpoint:
  
    <img width="436" alt="image" src="https://github.com/user-attachments/assets/814f831f-19b8-4939-a3e2-618385c4827b">
  
    > `Read All SQL Endpoint Data` permission allows users to access and read data from SQL endpoints within the Fabric environment. This permission is typically required for users who need to: <br/>
    > - Query Data: Execute SQL `queries against the data stored in the Fabric environment`. <br/>
    > - Access Reports: `View and interact with reports and dashboards that rely on SQL data sources`. <br/>
    > - Data Analysis: `Perform data analysis and generate insights` using SQL-based data.
  
      <img width="550" alt="image" src="https://github.com/user-attachments/assets/b87137f1-b464-43df-a04d-593a41b3131a">

2. Make sure the person already have access to the semantic model:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/f5344f85-53f3-48dc-b0b1-6b3c5995bbd6">
  
> - Granting `Read, ReadData` access to the `semantic model, sql analytics endpoint` <br/>
> - Grating `App audience` will enable the assigned identity to view it.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/353d88ad-a4a7-4aef-aff4-d584901c29d8">

## Upgrade your Power BI license

```
To use Power BI Premium Per User features, upgrade your license.
```
<p align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/317b8012-5ae3-4e6d-84bb-367602bdf179" />
</p>

> [!TIP]
> This means that the workspace is supported by a `Premium per-user` license. You are attempting to access content with either a `Pro` user license or a `Free` user license. To resolve this issue, it is recommended to either purchase the necessary PPU license for the user or support the workspace with an F64 capacity, allowing free users to view the content. If editing permissions are still needed, those users will require a Pro license.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/15b972bb-0c55-4f00-9f65-4aabb34cfa32" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/f2250cdc-8377-4403-b50f-f0ee39428812">

## Sporadic Access Error in Premium Workspace with Free Users

> User experiencing sporadic access errors when trying to access content in a Premium workspace. The error message indicates that the content is only available to Power BI Pro users, even though the workspace is hosted on Premium capacity.

> [!TIP]
> - `Licensing Confusion`: Power BI Pro and Power BI Premium are different licenses. Pro is for individual users, while Premium is for capacity. `Free users can view reports in a Premium workspace, but they cannot manage or edit content without a Pro license`. <br/>
> - `User Permissions`: If a user is an admin, member, or contributor in a workspace, `they need a Pro license to edit or modify reports, even in a Premium workspace`. <br/>
> - `Intermittent Connectivity Issues`: Network issues or temporary connectivity problems can cause licensing checks to fail, resulting in access errors. <br/>

> [!IMPORTANT]
> If all previous tips do not work, please consider the following steps

1. `Create a New Capacity in Microsoft Fabric`:
   - Go to the [Fabric](https://app.fabric.microsoft.com/) and select the gear icon (⚙) to open the Admin portal.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b0e026e4-89f2-4c5d-b1d4-37887e0a2bc3" />

   - In the Admin portal, select `Capacity settings`/`Fabric Capacity`:
   - Click on `Set up new capacity`.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/d23d1ca9-7911-40d6-bc26-b2e9dba964bf" />


   - Enter the required details such as capacity name, region, and size.
   - Select `Create` to set up the new capacity.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/d5664583-0a82-4b32-afb0-144aa4b05e32" />

2. `Reassign Workspaces to the New Capacity`:
   - In the Admin portal, go to the `Workspaces` tab.
   - Select the workspace you want to move.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b0e026e4-89f2-4c5d-b1d4-37887e0a2bc3" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/eb576045-6099-478d-b3a1-6606da9e71c3" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/bb7e86c7-a8b5-4486-97fb-c89b87ed6f00" />

3. `Monitor the New Capacity`: Please click here to see more information about [Fabric Capacity Metrics + Monitoring Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/20_FabricCapacityMetrics.md)
   - Install the Microsoft Fabric Capacity Metrics app from AppSource.
   - Go to the Power BI service, select `Apps`, and search for `Microsoft Fabric Capacity Metrics`.
   - Install and configure the app to monitor your capacity consumption and performance.
   - Use the app to identify any issues and make informed decisions on scaling or adjusting your capacity

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
