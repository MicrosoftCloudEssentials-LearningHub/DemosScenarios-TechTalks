# MySQL: Enabling Autoscale IOPS - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-05-09

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Storage IOPS in Azure Database for MySQL - Flexible Server](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-storage-iops#how-do-i-know-that-iops-have-scaled-up-and-scaled-down-when-the-server-is-using-the-autoscale-iops-feature-can-i-monitor-iops-usage-for-my-server)
- [Azure Database for MySQL - Flexible Server service tiers](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-service-tiers-storage#service-tiers-size-and-server-types)

</details>


<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

</details>


> When Autoscale IOPS is enabled for Azure Database for MySQL (Flexible Server), the IOPS (Input/Output Operations Per Second) automatically scale both up and down based on your workload demands. <br/>
> - During `high demand`, the system `increases IOPS` to maintain performance.
> - During `low demand`, it `scales down` to reduce resource usage and cost.

## How to provision 

1. Go to the [Azure Portal](https://portal.azure.com/)
2. Search for `Azure Database for MySQL Flexible Server` in the search bar.
3. Click `Create`.
4. Choose your subscription, resource group, and server name.
5. Select the region, MySQL version, and workload type (e.g., Development, Production).

     https://github.com/user-attachments/assets/5b500aea-538d-4ddb-88b6-e0717a2d0fbe

## How to enable IOPS

1. Go to the [Azure Portal](https://portal.azure.com/)
2. Select the server you want to configure.
3. In the left-hand menu, go to `Settings > Compute + Storage.`
4. In the IOPS section, select the option `Autoscale IOPS`
5. Click `Save` to apply the changes.

     https://github.com/user-attachments/assets/9e2983b3-3839-4ad3-8ab8-ccbb698f3228

## How to monitor 






<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

