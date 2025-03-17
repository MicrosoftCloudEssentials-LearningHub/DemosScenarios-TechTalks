# Azure MySQL: <br/> Backup (BU) & Disaster Recovery (DR) - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-17

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Backup and restore in Azure Database for MySQL - Flexible Server](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-backup-restore)
- [Back up an Azure Database for MySQL flexible server by using Azure Backup (preview)](https://learn.microsoft.com/en-us/azure/backup/backup-azure-mysql-flexible-server)
- [Migrate your MySQL database to Azure Database for MySQL - Flexible Server using dump and restore](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-migrate-dump-restore)
- [Trigger on-demand backup of an Azure Database for MySQL - Flexible Server instance by using the Azure portal](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/how-to-trigger-on-demand-backup)
- [Same-zone HA architecture](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-high-availability#same-zone-ha-architecture)

</details>

## Content 

- [Overview](#overview)
- [Backup BU for MySQL on Azure](#backup-bu-for-mysql-on-azure)
  - [Automated Backups](#automated-backups)
      - [Change Backups Retention Policy and Redundancy](#change-backups-retention-policy-and-redundancy)
      - [Point-in-Time Restore PITR](#point-in-time-restore-pitr)
  - [Manual Backups](#manual-backups)
      - [On-Demand Backups](#on-demand-backups)
      - [Exporting Data](#exporting-data)
  - [Backup Storage](#backup-storage)
      - [Backup Redundancy Option](#backup-redundancy-option)
- [Disaster Recovery DR for MySQL on Azure](#disaster-recovery-dr-for-mysql-on-azure)
- [High Available HA Servers](#high-available-ha-servers)

## Overview

| **Feature** | **Description**| **Limit**| **Use Cases**|
|---------|---------------|--------| -------|
| **Read Replicas**    | Read replicas are copies of the primary MySQL server that are used to offload read operations and improve read scalability. They can be created in the same or different regions and can be promoted to standalone servers in case of a primary server failure. | Up to **10** read replicas can be created per primary server.| - **Scaling Read-Intensive Workloads**: Offload read operations to replicas to improve performance.<br/>- **Disaster Recovery**: Promote replicas to standalone servers in case of primary server failure.<br/>- **Global Distribution**: Improve data access speed by placing replicas closer to users in different regions. |
| **Manual Backups**   | Manual backups are on-demand backups that you can create at any time. These backups capture the current state of the database and are stored in geo-redundant storage (GRS) or locally redundant storage (LRS). | Up to **50** on-demand manual backups can be created per server.| - **Data Protection**: Ensure data protection by creating backups before major changes or updates.<br/>- **Quick Recovery**: Use manual backups as restore points to quickly recover from data corruption or accidental deletions.<br/>- **Compliance**: Maintain backups for compliance and auditing purposes. |

> [!NOTE]
> Quick reference on how to create an Azure Database for MySQL Flexible Server:

https://github.com/user-attachments/assets/1c6efd8a-987a-46ac-a81d-6d4ae74b07fd

## Backup (BU) for MySQL on Azure

- `Automated Daily Snapshot Backups` -> Geo-Redundant Storage (GRS)
- `Manual Backups` ->  Locally Redundant Storage (LRS) or Geo-Redundant Storage (GRS)

> [!IMPORTANT]
> The backup process includes `automated daily snapshot backups and frequent transaction log backups`. The `first snapshot backup is scheduled immediately after the server is created`, and `subsequent snapshots are taken daily. Transaction log backups occur every five minutes, capturing all changes made to the database since the last transaction log backup`. If a scheduled backup fails, the backup service retries every 20 minutes until a successful backup is taken. These backup failures might occur due to heavy transactional production loads on the server instance. In cases of high transaction loads, the backup service may perform multiple backups per day to ensure reliable and quicker restoration using these backups. For MySQL 5.7 servers, long-running or large transactions can prevent global instance-level lock acquisition, which is required for successful daily backups.

| **Category**          | **Description**                                                                                                                                                                                                                       |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Automated Backups** | - **Daily Backups**: Azure Database for MySQL automatically performs daily backups of your databases. These backups are stored in geo-redundant storage (GRS) to ensure high availability.<br/>- **Retention Period**: Configure the retention period for automated backups, typically ranging from 7 to 35 days.<br/>- **Point-in-Time Restore (PITR)**: Restore your database to any point within the retention period, providing flexibility in case of accidental data loss or corruption. |
| **Manual Backups**    | - **On-Demand Backups**: Create manual backups at any time. These backups are stored in GRS and can be used to restore your database to the state at the time of the backup.<br/>- **Exporting Data**: Export your MySQL database using the `mysqldump` utility, which can be stored in Azure Blob Storage or downloaded locally for additional safety. |
| **Backup Storage**    | - **Geo-Redundant Storage (GRS)**: By default, backups are stored in GRS, which replicates data to a secondary region to ensure durability and availability.<br/>- **Locally Redundant Storage (LRS)**: For cost savings, you can opt for LRS, which keeps multiple copies of your data within a single region. |

### Automated Backups

> `Automated Backups` for Azure Database for MySQL ensure that your data is regularly backed up without manual intervention.

#### Change Backups Retention Policy and Redundancy

> Azure Database for MySQL automatically performs daily snapshot backups of the data files and transaction logs. These backups are stored in geo-redundant storage (GRS) to ensure high availability and durability.

1. **Access the Azure Portal**: Navigate to the Azure Portal and sign in with your credentials.
2. **Navigate to Your MySQL Flexible Server**: In the Azure Portal, go to `All resources` and select your Azure Database for MySQL Flexible Server instance.
3. **Compute + Storage Settings**: In the left-hand menu, under `Settings`, select `Compute + storage`.
4. **Backup Retention**:
   - In the `Backups` section, you will find the slider labeled `Backup retention period in days`.
   - Use the slider to set the retention period for automated backups, which can range from 7 to 35 days.

   https://github.com/user-attachments/assets/769fa81a-450f-4cd9-a4d9-8f4f227c01c9

5. **Backup Redundancy**:
   - Below the retention slider, you will see options for backup redundancy, select the desired redundancy option based on your requirements:
     - **Locally-redundant**: Keeps multiple copies of your data within a single region.
     - **Geo-redundant**: Replicates data to a secondary region to ensure durability and availability.

    https://github.com/user-attachments/assets/ea53958a-ca3e-4100-a527-d0e46cdb992e

#### Point-in-Time Restore (PITR)

> This feature allows you to restore your database to any point within the retention period, providing flexibility in case of accidental data loss or corruption.

> [!NOTE]
> When you initiate a PITR, you specify the exact point in time to which you want to restore the database. <br/> 
> - The restore process uses the daily snapshots and transaction log backups to reconstruct the database state at the specified point in time.
> - The restore operation `creates a new MySQL Flexible Server instance with the restored data`. You need to provide a new server name for the restored instance during the restore process

1. **Access the Azure Portal**: Navigate to your Azure Database for MySQL instance.
2. **Restore**: Under the `Overview` section. Choose the `Restore` option and specify the point-in-time to which you want to restore your database.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/d3ddc0e7-331d-44ec-b9e1-a3a38e54c325" />

      https://github.com/user-attachments/assets/0eeb96cf-07c6-40f1-9921-64f2c775d228

### Manual Backups

> `Manual Backups` provide additional control over backup operations, allowing you to create backups on demand.

> [!IMPORTANT]
> These backup files cannot be exported. The backups can only be used for restore operations in Azure Database for MySQL Flexible Server. You can also use [mysqldump](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-migrate-dump-restore#dump-and-restore-using-mysqldump-utility) from a MySQL client to copy a database.

#### On-Demand Backups

> You can create manual backups at any time. These backups are stored in geo-redundant storage (GRS) and can be used to restore your database to the state at the time of the backup.

1. **Access the Azure Portal**: Navigate to your Azure Database for MySQL instance.
2. **Backup Settings**: Under the `Settings` section, select `Backup and Restore`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/e4aab7b9-4d16-4a5c-8817-6ccab7ec555e" />

3. **Backup Now**: Click on `Backup` and provide a custom name for the backup.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/756a6512-267e-47a4-a2c5-4b182f4f28bd" />

     https://github.com/user-attachments/assets/0f3743ca-9098-45a4-82c9-e67593e4ffcc

#### Exporting Data

> You can export your MySQL database using the `mysqldump` utility, which generates a logical backup of the database. This backup can be stored in Azure Blob Storage or downloaded locally for additional safety.

1. **Use `mysqldump` Command**: Open a terminal and run the following command. Click [here](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-migrate-dump-restore#dump-and-restore-using-mysqldump-utility) to get more information.

   ```bash
   mysqldump -u [username] -p[password] [database_name] > [dump_file.sql]
   ```

2. **Upload to Azure Blob Storage**: Use Azure CLI or Azure Portal to upload the dump file to Azure Blob Storage.

### Backup Storage

> [!IMPORTANT]
> By default Azure Database for MySQL Flexible Server backup storage is: <br/>
> - Locally redundant for servers with same-zone high availability (HA) or no high availability configuration.
> - Zone redundant for servers with zone-redundant HA configuration.

> [!NOTE]
> - `Zone-redundant High Availability` to support zone redundancy is current surfaced as a `create time operation only`.
> - `Zone-redundant High Availability server geo-redundancy` can only be `enabled/disabled at server create time`.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/56387aee-7f18-4ffa-984d-ecd1c959304c" />

#### Backup Redundancy Option

| **Backup Redundancy Option** | **Description**| **Characteristics**| **When to Use**|
|------------------------------|------------|------------------------|----------------------------|
| **Locally Redundant Storage (LRS)** | - Multiple copies of backups are stored in the same datacenter.<br/>- Protects against server rack and drive failures.<br/>- Provides at least `99.999999999%` (11 9's) durability of backup objects over a given year.<br/>- Default for servers with same-zone HA or no HA configuration. | - Data replication within a single data center.<br/>- High durability within the same region.<br/>- Cost-effective.<br/>- Suitable for non-critical applications. | - When cost savings are a priority.<br/>- When the risk of regional outages is acceptable.<br/>- For servers with same-zone HA or no HA configuration. |
| **Geo-Redundant Storage (GRS)** | - Multiple copies of backups are stored within the region and replicated to its geo-paired region.<br/>- Provides at least `99.99999999999999%` (16 9's) durability of backup objects over a given year.<br/>- Enabled at server create time for geo-redundant backup storage.<br/>- Can be moved from LRS to GRS post-creation.<br/>- Supported for servers in any Azure paired regions. | - Data replication across geo-paired regions.<br/>- Highest durability and availability.<br/>- Protection against regional disasters.<br/>- Ability to restore in a different region. | - For applications requiring the highest level of durability and availability.<br/>- When protection against regional disasters is critical.<br/>- When the ability to restore in a different region is needed. |
| **Zone-Redundant Storage (ZRS)** | - Multiple copies of backups are stored within the availability zone and replicated to another availability zone in the same region.<br/>- Provides at least `99.9999999999%` (12 9's) durability of backup objects over a given year.<br/>- Selected at server create time for zone-redundant HA.<br/>- Backup storage remains zone-redundant even if HA is disabled post-creation. | - Data replication across multiple availability zones.<br/>- Higher availability and resilience against zone-level failures.<br/>- Meets data residency requirements within a country/region. | - For mission-critical applications requiring high availability.<br/>- When protection against zone-level failures is needed.<br/>- When data residency requirements must be met. |

## Disaster Recovery (DR) for MySQL on Azure

| **Category**| **Description**| **Technical Details**|
|-----------------------|----------|--------------|
| **Geo-Replication**   | - **Read Replicas**: Azure Database for MySQL supports read replicas, which can be created in the same or different regions. These replicas can be promoted to standalone servers in case of a primary server failure.<br/>- **Cross-Region Replication**: This feature allows you to replicate your MySQL instance to a different Azure region, providing a robust DR solution. | - **Replication Method**: Uses MySQL's native binary log (binlog) file position-based replication.<br/>- **Creation**: Up to 10 replicas can be created.<br/>- **Promotion**: Replicas can be promoted to standalone servers.<br/>- **Cross-Region Replication Setup**: Requires primary and secondary servers in different regions. |
| **Failover Strategies** | - **Automatic Failover**: In the event of a failure, Azure Database for MySQL can automatically failover to a read replica or a secondary instance, minimizing downtime.<br/>- **Manual Failover**: You can manually initiate a failover to a read replica or a secondary instance if needed. | - **Automatic Failover Configuration**: Enabled during server creation.<br/>- **Process**: Standby replica is activated to become the primary server.<br/>- **Manual Failover Steps**: Initiate failover via Azure Portal.<br/>- **DNS Update**: DNS record is updated to point to the new primary server. |
| **High Availability (HA)** | - **Zone-Redundant HA**: Azure offers zone-redundant high availability, which ensures that your MySQL instance is replicated across multiple availability zones within a region. This setup provides resilience against zone-level failures.<br/>- **Regional HA**: For even greater resilience, you can configure your MySQL instance to be replicated across different regions. | - **Zone-Redundant HA Architecture**: Primary server in one availability zone, standby replica in another.`Uses zone-redundant storage (ZRS)`.<br/>- **Regional HA Architecture**: Primary server in one region, standby replica in another region. `Uses geo-redundant storage (GRS).` |

## High Available (HA) Servers

> Servers enabled with HA have a primary and secondary replica. The secondary replica can be in the same zone or zone redundant. You are billed for the provisioned compute and storage for both the primary and secondary replica. E.g, if you have a primary with 8 vCores of compute and 1,024 GB of provisioned storage, your secondary replica will also have 8 vCores and 1,024 GB of provisioned storage. Your zone redundant HA server will be billed for 16 vCores and 2,048 GB of storage. An extra 36 IOPS per node in addition to the configured IOPS on your servers will be added and reserved, so additional charges for the 72 IOPS per month would apply based on your Azure region for HA enabled servers. Depending on your backup storage volume, you may also be billed for backup storage. For instance, if your backup storage volume is 500 GB, you will be billed for the backup storage based on the configured redundancy option (LRS or GRS).

| Zone-redundant HA architecture | Same-zone HA architecture |
| ---- | ---- | 
| ![image](https://github.com/user-attachments/assets/9ae8fa67-be98-4b27-a835-288eae4096f4) | ![image](https://github.com/user-attachments/assets/f037651c-b29a-4fad-942a-ecf95f8ec3d5) |

[From Microsoft Official documentation](https://learn.microsoft.com/en-us/azure/mysql/flexible-server/concepts-high-availability)

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
