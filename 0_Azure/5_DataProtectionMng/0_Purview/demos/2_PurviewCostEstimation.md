# Azure Purview Cost Estimation - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-19

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>
  
- [Microsoft Purview pricing](https://azure.microsoft.com/en-us/pricing/details/purview/)

</details>

## Overview

Estimating the cost for Azure Purview requires consideration of the following components:

| Component | Description |
| --- | --- | 
| Data Map Population | This component includes scanning and classification of data. The cost is calculated based on the serverless compute power needed for a scan. Each scan is provisioned with a 32 vCore compute cluster by default. The more data you scan and the more frequently you scan it, the higher the cost will be | 
| Resource Set | This component involves the storage of metadata and lineage information. The cost is based on the amount of metadata stored and the frequency of scans. Essentially, this means that the more metadata you store and the more often you scan your data, the higher the cost will be | 
| Managed Virtual Network Charges | Customers using the latest version of Microsoft Purview Managed Virtual Network will be charged at 1/8 vCore hour for the running time of the Managed VNet Integration Runtime, in addition to the charges on scan and ingestion jobs | 
| Data Transfers and API Calls |  Customers using Microsoft Purview to govern data in other clouds (e.g., AWS, GCP) may incur additional charges due to data transfers and API calls associated with the publishing of metadata into the Microsoft Purview Data Map. This charge varies by region | 


The general formula to keep in mind for estimating the cost of Microsoft Purview is:

> - **Cost of Data Map**: Calculated based on the number of capacity units and the price per capacity unit per hour. <br/>
> - **Cost of Scanning**: Calculated based on the total duration (in minutes) of all scans in a month, divided by 60 minutes per hour, multiplied by the number of vCores per scan, and the price per vCore per hour. <br/>
> - **Cost of Resource Set**: Calculated based on the total duration (in hours) of processing resource set data assets in a month, multiplied by the price per vCore per hour.


 $$ \text{Total Cost per Month} = \text{Cost of Data Map} + \text{Cost of Scanning} + \text{Cost of Resource Set} 
 $$ 

1. Data Map (Always on):
  - Number of Capacity Units: Typically 1
  - Total Hours in a Month: 730 hours
  - Price per Capacity Unit per Hour: \$0.411

  $$
  \text{Total Cost for Data Map} = \text{Number of Capacity Units} \times \text{Total Hours in a Month} \times \text{Price per Capacity Unit per Hour}
  $$

2. Scanning (Pay as you go):
  - Total Minutes of Scanning in a Month: [M] minutes
  - Number of vCores per Scan: 32
  - Price per vCore per Hour: \$0.63

  $$
  \text{Total Cost for Scanning} = \left( \frac{\text{Total Minutes of Scanning in a Month}}{60} \right) \times \text{Number of vCores per Scan} \times \text{Price per vCore per Hour}
  $$

3. Resource Set:
  - Total Hours of Processing in a Month: [H] hours
  - Price per vCore per Hour: \$0.21

  $$
  \text{Total Cost for Resource Set} = \text{Total Hours of Processing in a Month} \times \text{Price per vCore per Hour}
  $$

## Average Example Calculation

> - The total duration of all scans in a month is 600 minutes. <br/>
> - The total duration of processing Advanced Resource Set data assets in a month is 50 hours.

1. Total Cost for Data Map (Always on): 

  $$
  1 \text{ Capacity Unit} \times 730 \text{ hours} \times \$0.411 = \$299.03
  $$

2. Total Hours of Scanning (Pay as you go):

  $$
  \frac{600 \text{ minutes}}{60 \text{ minutes per hour}} = 10 \text{ hours}
  $$

  $$
  10 \text{ hours} \times 32 \text{ vCores} \times \$0.63 = \$201.60
  $$

3. Total Cost for Resource Set:

  $$
  50 \text{ hours} \times \$0.21 = \$10.50
  $$

Total Monthly Cost: Combining the costs for Data Map, Scanning, and Resource Set

- **Total Cost for Data Map**: \$299.03
- **Total Cost for Scanning**: \$201.60
- **Total Cost for Resource Set**: \$10.50

- **Total Monthly Cost**: 

$$
\$299.03 + \$201.60 + \$10.50 = \$511.13
$$

## Average Scan Frequency for Different Use Cases

| **Scenario**                           | **Description**                                                                                     | **Frequency**            |
|----------------------------------------|-----------------------------------------------------------------------------------------------------|--------------------------|
| **Compliance and Regulatory Requirements** | Organizations that need to comply with strict regulatory requirements may perform daily or weekly scans to ensure data is up-to-date and compliant. | Daily or Weekly          |
| **Data Governance and Management**     | For general data governance and management, organizations may perform weekly or bi-weekly scans to keep track of data changes and maintain data quality. | Weekly or Bi-weekly      |
| **Data Analytics and Reporting**       | Organizations that rely heavily on data analytics and reporting may perform monthly scans to ensure that the data used for analysis is accurate and up-to-date. | Monthly                  |
| **Ad-hoc Scans**                       | In some cases, organizations may perform ad-hoc scans as needed, based on specific events or requirements. | As Needed                |

## Additional Considerations

- **Optimize Scan Frequency**: Reduce the frequency of scans to lower the overall cost by customizing Scan Rule Sets to control cost.This enable sto fine-tune the time scans take. Find below the steps to create and customize scan rule sets:
   1. From the Microsoft Purview portal, select the `Data Map` solution.
   2. Under the Source management section, select `Scan rule sets`, and then select New.
   3. From the New scan rule set page, select the data sources that the catalog scanner supports from the Source Type drop-down list. You can create a scan rule set for each type of data source you intend to scan.
   4. Give your scan rule set a Name and optionally enter a Description.
   5. On the Select file types page, enable or disable file types for schema and classification by selecting or clearing their checkboxes. For certain data source types, you can also create a custom file type.
   6. On the Select classification rules page, select or clear the System rules classification rule checkboxes globally by category or individually.
- **Efficient Data Management**: Use incremental loads and data partitioning to minimize scan duration.
- **Monitor Usage**: Regularly monitor your usage and costs using Azure Cost Management tools to identify areas for optimization.

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
