# Connecting SharePoint lists to Power BI - Overview 

 Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-08

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Understand Microsoft Fabric licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses)
- [Power BI embedding scenarios](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#power-bi-embedding-scenarios)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

 - [General process](#general-process)
 - [How to refresh?](#how-to-refresh)
     - [Manual approach](#manual-approach)
     - [Schedule refresh](#schedule-refresh)
</details>

## General process 

1. Select the list of assets; for this scenario, please choose the SharePoint list:

    <img width="1905" height="995" alt="image" src="https://github.com/user-attachments/assets/113ed3d7-1004-4256-9d5f-a752c1d2678c" />

2. Select the 'Export to Power BI' option:

   <img width="1907" height="998" alt="image" src="https://github.com/user-attachments/assets/7118b05c-5879-41a6-929e-641ee13b1f01" />

   > Initial list:
   
   <img width="814" height="234" alt="image" src="https://github.com/user-attachments/assets/c9a58ee2-78d7-4871-85bb-97a8a8a9549e" />

3. Select the `name for the data set` that will be created as a copy of your information from SharePoint. It can be refreshed manually or
automatically depending on the configuration. Choose the `workspace `where it will be published, as viewing and creating content in Fabric/Power BI requires the appropriate licenses. You can find more details about this
[Power Bi Licensing - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/DemosScenarios-TechTalks/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/33_PowerBi_Licensing.md). Finally, click `continue`

      <img width="1897" height="843" alt="image" src="https://github.com/user-attachments/assets/668c681d-d85f-4270-9083-3f1d2f4fab85" />

> [!NOTE]
> If you have previously been connected to this List, this message will appear. Please feel free to select the option that best suits your needs.

<img width="697" height="431" alt="image" src="https://github.com/user-attachments/assets/ffe66b2f-cd27-4708-89b4-53eea6409e91" />


> You will receive a notification indicating that the dataset is being created: 

<img width="1907" height="275" alt="image" src="https://github.com/user-attachments/assets/3169c011-a29c-4bbd-9034-b38c71d6301c" />

> [!TIP]
> If you need to modify the dataset, such as removing the summarization type from a column, please follow these steps:

https://github.com/user-attachments/assets/9f28c491-bf2c-407b-83ff-7a2171c5c063

4. Please create a Power BI report using the provided dataset. There are several approaches you can take to accomplish this:
   
   > In the semantic model view, please select `Export` and then choose `Create a blank report`.
   
   <img width="1907" height="786" alt="image" src="https://github.com/user-attachments/assets/a1a82d61-b65e-4727-b294-1cacd0efa35a" />
   
   > For instance, when accessing it from the workspace view:
   
   <img width="1891" height="987" alt="image" src="https://github.com/user-attachments/assets/47e78f0b-2b09-4338-b678-a97aa8f99b21" />
   
   For example, this is how it looks:
   
   https://github.com/user-attachments/assets/832d492a-3538-4730-8ada-f811a4f09d1e

## How to refresh?

> Now, let's consider a scenario where the information from SharePoint is refreshed, `how to update the report.`

### Manual approach 

`Refresh now`

> Here is the process for manually refreshing the data.

> [!NOTE]
> This can also be done automatically or scheduled as needed.

| Initial list | Power Bi | 
| --- | --- | 
| <img width="814" height="234" alt="image" src="https://github.com/user-attachments/assets/c9a58ee2-78d7-4871-85bb-97a8a8a9549e" /> | <img width="538" height="302" alt="image" src="https://github.com/user-attachments/assets/1853a761-2239-4e09-9be9-98d110264949" /> | 

> How to update the dataset?

https://github.com/user-attachments/assets/e858dc17-176a-4836-bbed-f80e03e670eb

| Updated list | Updated Power Bi | 
| --- | --- | 
| <img width="872" height="271" alt="image" src="https://github.com/user-attachments/assets/b4bdf493-c81f-46bf-8412-86ce27de3864" /> | <img width="368" height="187" alt="image" src="https://github.com/user-attachments/assets/2fa47954-6e64-467f-a63f-be8a0582447b" /> | 

### Schedule refresh  

`Daily, Weekly, time set`

https://github.com/user-attachments/assets/910fce13-df61-4172-a273-24e35c36be8e

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
