# Fabric region availability - Overview \&  Considerations

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!IMPORTANT]
>  Please check: <br/>
> - [Fabric region availability](https://learn.microsoft.com/en-us/fabric/admin/region-availability) for any updates. <br/>
> - [Microsoft Fabric features by SKU](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features).


<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Fabric region availability](https://learn.microsoft.com/en-us/fabric/admin/region-availability)
- [Limitations in Microsoft Fabric mirrored databases from Azure SQL Managed Instance (Preview)](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-sql-managed-instance-limitations)
- [Overview of managed private endpoints for Fabric](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [West Regions](#west-regions)
- [Copilot Workload](#copilot-workload)
- [Pricing consideration](#pricing-consideration)
- [Azure Pricing Calculator](#azure-pricing-calculator)

</details>

## West Regions 

> As today, please click here to read more about [Fabric region availability](https://learn.microsoft.com/en-us/fabric/admin/region-availability)

| **Region**   | **Available Copilot Workloads**                     | **Unavailable Features**                                                                 | 
|--------------|-----------------------------------------------------|-------------------------------------------------------------------------------------------|
| **West US**  | - Dataflows<br>- Exploration<br>- Synapse Notebook  | - Mirroring for Azure SQL Managed Instance<br>- User Data Functions<br>- [Managed Private Endpoints](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview) |
| **West US 2**| - Dataflows<br>- Exploration<br>- Synapse Notebook  | - Mirroring for Azure SQL Managed Instance<br>- User Data Functions<br>- Dataflow Gen2 with CI/CD |
| **West US 3**| - Dataflows<br>- Synapse Notebook                   | - User Data Functions<br>- Dataflow Gen2 with CI/CD               | 

## Copilot Workload

| **Copilot Workload**     | **What it is**                                                                 | **Copilot's Role**                                                                                                                                                                                                 | **Use Case**                                                                                          |
|--------------------------|--------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Dataflows (Copilot)**  | A low-code/no-code tool for data transformation and preparation.              | Helps build and transform data pipelines using natural language. Copilot generates transformation steps based on user instructions like:<br>• "Clean this column"<br>• "Merge these tables"<br>• "Remove nulls"     | Ideal for business analysts or data engineers who want to automate ETL processes without coding.       |
| **Exploration (Copilot)**| A feature that allows users to explore datasets interactively.                | Assists in understanding data by:<br>• Answering questions<br>• Generating summaries<br>• Suggesting visualizations or queries<br>• Highlighting trends, outliers, and patterns                                   | Great for data analysts or business users seeking quick insights without writing queries.              |
| **Synapse Notebook (Copilot)** | A notebook environment (like Jupyter) for data science and engineering tasks. | Acts as an AI assistant that:<br>• Suggests code snippets (Python, Spark, SQL)<br>• Helps with data exploration and visualization<br>• Recommends ML models<br>• Offers debugging tips and documentation          | Perfect for data scientists and engineers working with large datasets, machine learning, or analytics. |

## Pricing consideration 

> Microsoft Fabric pricing is based on capacity units (CUs), region, and usage patterns. Costs can vary significantly depending on
> whether you use pay-as-you-go or reserved pricing, and whether your workloads span multiple regions. Click here to see [Microsoft Fabric pricing](https://azure.microsoft.com/en-us/pricing/details/microsoft-fabric/?msockid=38ec3806873362243e122ce086486339).

<details>
  <summary><strong>Capacity-Based Billing</strong></summary>

  > **Fabric uses Capacity Units (CUs)** to meter compute usage. You can choose between flexible or committed pricing models depending on your workload needs.

  1. Pay-as-you-go: No commitment, higher cost.
  2. Reserved capacity: 1-year commitment, up to ~41% savings.
  3. Example (F64 capacity):
     - Pay-as-you-go: ~$8,409.60/month
     - Reserved: ~$5,002.67/month
</details>

<details>
  <summary><strong>Regional Price Differences</strong></summary>

  > **Fabric pricing varies by Azure region** due to infrastructure, currency, and tax differences.

  1. Influencing factors:
     - Local infrastructure costs
     - Currency exchange rates
     - Regional taxes (e.g., IOF in Brazil)
  2. Always use the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339) to check region-specific pricing.
</details>

<details>
  <summary><strong>Egress Charges</strong></summary>

  > **Data transfer between Azure regions incurs egress fees**, which are not included in Fabric capacity pricing.

  1. Applies when moving data across regions (e.g., West US to East US).
  2. Example: Transferring data from OneLake in West US 2 to another region may cost $0.02–$0.09 per GB, depending on the destination.
</details>

<details>
  <summary><strong>Reservation Notes</strong></summary>

  > **Reservations apply only to compute (CUs)** and require upfront configuration.

  1. Storage and networking are billed separately.
  2. Reservations do not auto-renew unless explicitly configured.
  3. You must specify:
     - Region
     - Billing frequency (monthly or upfront)
     - Number of CUs
</details>

<details>
  <summary><strong>Cost Optimization Tips</strong></summary>

  > **Strategies to reduce your Microsoft Fabric costs** while maintaining performance and flexibility.

  1. Use reservations for stable, predictable workloads.
  2. Avoid cross-region data movement to reduce egress charges.
  3. Right-size your capacity based on actual usage.
  4. Use the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339) to simulate and compare configurations.
</details>

## Azure Pricing Calculator

> [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339) will calculate storage costs if you exceed the included limit for your selected SKU. If your usage stays within the included storage capacity, you shouldn’t see additional charges for storage. <br/> <br/> 
> The included storage in Microsoft Fabric primarily applies to **mirroring** across all F SKUs. This means that the free storage provided (e.g., 64 TB for F64) is specifically allocated for creating mirrored copies of your data to ensure redundancy and high availability. <br/> <br/>
> For other types of storage, such as general data storage or storage used by Data Factory and AI capabilities, you will be billed if you exceed the included storage or if compute capacity is paused.This applies to all F SKUs, from F2 to F2048.

https://github.com/user-attachments/assets/83447901-2227-4cf3-a89c-c8ee57d50009


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
