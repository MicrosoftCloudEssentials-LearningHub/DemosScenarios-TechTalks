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

</details>

> [!NOTE]
> Quick reference on how to create an Azure Database for MySQL Flexible Server:

https://github.com/user-attachments/assets/1c6efd8a-987a-46ac-a81d-6d4ae74b07fd

## Backup (BU) for MySQL on Azure

| **Category**          | **Description**                                                                                                                                                                                                                       |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Automated Backups** | - **Daily Backups**: Azure Database for MySQL automatically performs daily backups of your databases. These backups are stored in geo-redundant storage (GRS) to ensure high availability.<br/>- **Retention Period**: Configure the retention period for automated backups, typically ranging from 7 to 35 days.<br/>- **Point-in-Time Restore (PITR)**: Restore your database to any point within the retention period, providing flexibility in case of accidental data loss or corruption. |
| **Manual Backups**    | - **On-Demand Backups**: Create manual backups at any time. These backups are stored in GRS and can be used to restore your database to the state at the time of the backup.<br/>- **Exporting Data**: Export your MySQL database using the `mysqldump` utility, which can be stored in Azure Blob Storage or downloaded locally for additional safety. |
| **Backup Storage**    | - **Geo-Redundant Storage (GRS)**: By default, backups are stored in GRS, which replicates data to a secondary region to ensure durability and availability.<br/>- **Locally Redundant Storage (LRS)**: For cost savings, you can opt for LRS, which keeps multiple copies of your data within a single region. |

### Automated Backups

> `Automated Backups` for Azure Database for MySQL ensure that your data is regularly backed up without manual intervention.

#### Daily Backups

> Azure Database for MySQL automatically performs daily snapshot backups of the data files and transaction logs. These backups are stored in geo-redundant storage (GRS) to ensure high availability and durability.

1. **Access the Azure Portal**: Navigate to your Azure Database for MySQL instance.
2. **Backup Settings**: Under the `Settings` section, select `Backup and Restore`.
3. **Configure Retention Period**: Set the retention period for automated backups, which can range from 7 to 35 days.
4. **Encryption**: Ensure that backups are encrypted using AES 256-bit encryption for data at rest.


### Manual Backups

### Backup Storage


## Disaster Recovery (DR) for MySQL on Azure

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
