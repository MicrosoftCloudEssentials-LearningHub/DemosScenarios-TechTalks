# MySQL: Enabling Autoscale IOPS - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-05-13

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Storage IOPS in Azure Database for MySQL - Flexible Server](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-storage-iops#how-do-i-know-that-iops-have-scaled-up-and-scaled-down-when-the-server-is-using-the-autoscale-iops-feature-can-i-monitor-iops-usage-for-my-server)
- [Azure Database for MySQL - Flexible Server service tiers](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-service-tiers-storage#service-tiers-size-and-server-types)
- [Autoscale IOPS for Azure Database for MySQL - Flexible Server - General Availability](https://techcommunity.microsoft.com/blog/adformysql/autoscale-iops-for-azure-database-for-mysql---flexible-server---general-availabi/3884602)

</details>


<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [How to provision](#how-to-provision)
- [How to enable IOPS](#how-to-enable-iops)
- [How to Monitor IOPS Scaling](#how-to-monitor-iops-scaling)

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

## How to Monitor IOPS Scaling

> How I know if the IOPS have scaled up or down when the server's using the autoscale IOPS feature? You can use the `metrics available in Azure Monitor`. 

1. **Use Azure Monitor Metrics**:
   - Go to your server in the [Azure portal](https://portal.azure.com/)
   - Go to the `Monitoring` section and select `Metrics`.
          
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/f08afb04-e271-4ac3-8594-e3e98a9bfd2e" />

   - Choose the ` Storage IO` metric (both percent and count).

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/ca585f55-e943-413d-9477-f26c099a1e66" />

   - Set a `custom time range` to observe trends over time.

     | Storage IO Count | Storage IO Percent |
     | --- | --- | 
     | <img width="550" alt="image" src="https://github.com/user-attachments/assets/9be08df9-3fe6-4010-9e75-487a325d0acb" /> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/c5f7f45d-303d-48ce-82a4-00685da29849" /> |

2. **Look for Scaling Patterns**:
   - If you see `sudden increases or decreases` in the IOPS metric that correlate with workload changes, this indicates that autoscale IOPS has adjusted the performance level.
   - You can also monitor `IO utilization percentage` to see how close your server is to its current IOPS limit.
3. **Enable Alerts (Optional)**: You can set up `alerts` in Azure Monitor to notify you when IOPS usage crosses certain thresholds, which can help you track scaling events in real time.

   https://github.com/user-attachments/assets/19b96128-e37f-40b4-8e23-8a5384bc6686


<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

