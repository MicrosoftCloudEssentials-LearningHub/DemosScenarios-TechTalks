# Azure Purview - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-19

----------

> `Microsoft Priva` is tailored for managing privacy risks and ensuring compliance with `privacy regulations`. It helps organizations automate privacy operations and manage consent and data subject requests. <br/>
> `Microsoft Purview` offers a broader range of `data governance and protection capabilities`, focusing on securing and managing data across the entire organization, including compliance and risk management.
> `Microsoft Priva integrates seamlessly with Microsoft Purview`, enhancing the overall data governance and compliance capabilities. `Together, they provide a comprehensive solution for managing data privacy and compliance` across your organization.


<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [What's new in Microsoft Purview](https://learn.microsoft.com/en-us/purview/whats-new)
- [What is the Microsoft Purview Data Catalog?](https://learn.microsoft.com/en-us/purview/what-is-data-catalog)
- [How to request access for a data asset](https://learn.microsoft.com/en-us/purview/how-to-request-access)
- [Data catalog development best practices](https://learn.microsoft.com/en-us/purview/data-catalog-best-practices)
- [Supported data sources and file types](https://learn.microsoft.com/en-us/purview/microsoft-purview-connector-overview)
- [Discover and govern Azure SQL Database](https://learn.microsoft.com/en-us/purview/register-scan-azure-sql-database)
- [Disaster recovery for Microsoft Purview](https://learn.microsoft.com/en-us/purview/disaster-recovery)
- [Query SQL Database with query editor in the Azure portal](https://learn.microsoft.com/en-us/azure/azure-sql/database/connect-query-portal?view=azuresql)

</details> 

## Overview 

> Microsoft Purview is a comprehensive set of solutions designed to help organizations govern, protect, and manage their data across their entire data estate.

| **Feature**                     | **Microsoft Priva**                                                                 | **Microsoft Purview**                                                                 |
|---------------------------------|-------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Primary Focus**               | Privacy management and compliance                                                   | Data governance, protection, and compliance                                          |
| **Key Capabilities**            | - Privacy Risk Management<br>- Subject Rights Requests<br>- Consent Management      | - Data Loss Prevention<br>- Information Protection<br>- Insider Risk Management      |
| **Data Handling**               | Focuses on personal data privacy and regulatory compliance                          | Manages and protects data across the entire data estate                              |
| **Integration**                 | Integrates with Microsoft Purview for data classification and labeling               | Integrates with Microsoft 365 and Azure for comprehensive data governance            |
| **Use Cases**                   | - Automating privacy assessments<br>- Managing consent<br>- Handling data subject requests | - Mapping data estate<br>- Classifying and protecting sensitive data<br>- Managing insider risks |
| **Compliance Tools**            | Privacy-specific compliance tools and assessments                                   | Broad compliance tools including audit, eDiscovery, and communication compliance     |
| **Target Users**                | Privacy officers, compliance teams                                                  | Data governance teams, security officers, compliance teams                           |

### Benefits of Microsoft Purview

| **Benefit**                       | **Description**                                                                 |
|-----------------------------------|---------------------------------------------------------------------------------|
| Visibility                        | Gain insights into data across your organization.                               |
| Security                          | Safeguard data throughout its lifecycle.                                        |
| Governance                        | Seamlessly govern data in new, comprehensive ways.                              |
| Compliance                        | Minimize compliance risks and meet regulatory requirements.                     |
| Sensitive Data Detection          | Identifies sensitive information using deep content analysis.                   |
| Policy Creation and Enforcement   | Allows creation and enforcement of DLP policies across various services.        |
| Machine Learning Integration      | Enhances detection accuracy with machine learning algorithms.                   |
| Comprehensive Monitoring          | Monitors actions on sensitive items and prevents unintentional sharing.         |
| Integration with Sensitivity Labels| Unifies data security and compliance with sensitivity labels from Microsoft Information Protection. |

### Key Features of Microsoft Purview

| **Category**           | **Feature**                        | **Description**                                                                 |
|------------------------|------------------------------------|---------------------------------------------------------------------------------|
| **Data Security**      | - Data Loss Prevention <br/> - Information Protection <br/> - Insider Risk Management <br/> - Privileged Access Management | - Protects sensitive information from risky and unauthorized access.<br/>- Identifies, classifies, and protects sensitive data.<br/>- Detects and acts on critical risks like data theft and leaks.<br/>- Manages and secures privileged access to sensitive data. |
| **Data Governance**    | - Data Map <br/> - Data Catalog <br/> - Unified Data Governance | - Registers and scans data sources to map the data estate and identify sensitive data.<br/>- Curates data sources, manages data integrity, and secures sensitive data.<br/>- Manages data services across on-premises, multicloud, and SaaS environments. |
| **Risk and Compliance**| - Audit <br/> - Communication Compliance <br/> - Compliance Manager <br/> - eDiscovery | - Supports forensic investigations and meets regulatory requirements.<br/>- Detects sensitive or inappropriate content in communication channels.<br/>- Translates regulatory requirements into specific improvement actions.<br/>- Manages data for internal or legal investigations. |


## Azure Cloud Services related with Microsoft Purview 

> These services work together with Microsoft Purview to `provide comprehensive data governance, protection, and management across your entire data estate`.

| **Service**                  | **Description**                                                                 |
|------------------------------|---------------------------------------------------------------------------------|
| **Azure Synapse Analytics**  | Integrates with Purview for data lineage and unified analytics.                  |
| **Azure SQL Database**       | Works with Purview for data classification and governance.                      |
| **Azure Data Factory**       | Connects with Purview for data integration and orchestration.                   |
| **Azure Blob Storage**       | Supports data storage and integrates with Purview for data governance.          |
| **Azure Data Lake Storage**  | Provides scalable storage and integrates with Purview for data management.      |
| **Power BI**                 | Integrates with Purview for data visualization and governance.                  |
| **Azure Cosmos DB**          | Works with Purview for managing and governing globally distributed data.        |
| **Azure SQL Managed Instance** | Supports data governance and classification with Purview.                      |
| **Azure HDInsight**          | Integrates with Purview for big data analytics and governance.                  |
| **Azure Databricks**         | Connects with Purview for advanced analytics and data governance.               |

## Demo Ideas 

| **Context**          | **Demo**                        | **Objective**                                      | **Setup**                                      | **Demo Steps**                                                                                                                                                                                                                     | **Outcome**                                                                                       |
|----------------------|---------------------------------|---------------------------------------------------|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| Microsoft 365        | Data Loss Prevention (DLP)      | Set up and enforce DLP policies                   | Configure DLP policies in the Purview portal    | 1. Navigate to the DLP section.<br>2. Create a new DLP policy.<br>3. Apply the policy to Microsoft 365 services.<br>4. Simulate data activities.<br>5. Review alerts and actions.                                                  | Show how Purview helps protect sensitive data across Microsoft 365 services.                     |
|                      | Information Protection          | Classify and label sensitive data                 | Configure sensitivity labels and policies       | 1. Access the Information Protection section.<br>2. Create and publish sensitivity labels.<br>3. Apply labels to documents and emails.<br>4. Demonstrate automatic labeling.<br>5. Review reports on labeled data.                | Highlight how Purview helps classify and protect sensitive information.                           |
| On-Premises          | Information Protection Scanner  | Use the Information Protection scanner            | Install and configure the scanner               | 1. Install the scanner on an on-premises server.<br>2. Configure the scanner to scan file shares and SharePoint libraries.<br>3. Set up sensitivity labels and policies.<br>4. Run the scanner.<br>5. Review scan results.         | Show how Purview extends data protection to on-premises environments.                             |
|                      | Data Classification and Labeling| Classify and label data in on-premises databases  | Configure data classification policies          | 1. Access the Data Classification section.<br>2. Connect to an on-premises SQL database.<br>3. Create and apply classification policies.<br>4. Run a scan.<br>5. Review classification results.                                    | Demonstrate how Purview helps classify and protect sensitive data in on-premises databases.       |
| Azure                | Data Map and Data Catalog       | Create and use a data map and data catalog        | Configure the Purview Data Map and Data Catalog | 1. Access the Data Map section.<br>2. Register and scan Azure data sources.<br>3. Create a data catalog.<br>4. Demonstrate data discovery and classification.<br>5. Show end-to-end data lineage.                                 | Highlight how Purview provides a comprehensive view of your data landscape in Azure.              |
|                      | Data Governance and Compliance  | Manage data governance and compliance             | Configure governance policies and compliance controls | 1. Access the Governance and Compliance section.<br>2. Create and apply governance policies.<br>3. Set up compliance controls.<br>4. Monitor data activities and compliance status.<br>5. Generate compliance reports.            | Demonstrate how Purview helps manage data governance and compliance in Azure.                     |
|                      | Data Lineage and Impact Analysis| Demonstrate data lineage and impact analysis      | Configure data lineage tracking                 | 1. Access the Data Lineage section.<br>2. Register Azure data sources.<br>3. Perform data operations.<br>4. Analyze data lineage.<br>5. Conduct impact analysis.                                                                  | Show how Purview provides insights into data flow and helps in impact analysis.                   |

## Setting Up Foundational Elements in Azure Purview

### **Data Cataloging**

| **Component**       | **Description**                                                                 | **Best Practices**                                                                 |
|---------------------|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Data Map**        | - Automated Metadata Scanning: Automate the scanning of metadata from various data sources. <br> - Data Lineage: Track the lineage of data to understand its flow from source to destination. | - Use built-in and custom classifiers for accurate data discovery and classification. <br> - Ensure comprehensive lineage tracking for compliance and auditing. |
| **Data Catalog**    | - Governance Domains: Create governance domains to distribute ownership and maintenance tasks. <br> - Glossary Terms: Define glossary terms to standardize data definitions across the organization. | - Distribute governance responsibilities to make data easily discoverable. <br> - Standardize data definitions to enhance understanding and usage. |

### **Handling Data Subject Requests**

| **Component**               | **Description**                                                                 | **Best Practices**                                                                 |
|-----------------------------|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Self-Service Access Requests** | - Access Workflow: Enable users to request access to data assets directly through the Purview catalog. <br> - Data Access Policies: Implement data access policies to ensure only authorized users can access sensitive data. | - Streamline access requests by automating workflows. <br> - Protect privacy and comply with regulations through strict access policies. |

### **Additional Best Practices**

| **Practice**                | **Description**                                                                 |
|-----------------------------|---------------------------------------------------------------------------------|
| **Federated Governance**    | Adopt a federated governance approach to distribute data governance responsibilities across the organization. |
| **Data Quality and Trust**  | Enhance data quality and trustworthiness by implementing governance-focused actions and creating source-of-truth data products. |
| **Business Value Creation** | Align data governance with business practices to unlock business value and make data more accessible and useful for decision-making. |

## Query an SQL database with Azure Purview

1. **Register the Data Source**:
   - Open the Microsoft Purview governance portal.
   - Register your Azure SQL Database as a data source. This involves providing the necessary credentials and permissions.
2. **Configure Access**: Ensure that the Purview managed identity has the required permissions on your SQL database. This typically involves creating a user in your SQL database and assigning the appropriate roles.
3. **Run a Scan**: In the Purview portal, create and run a scan on your registered SQL database. This will extract metadata and classify the data based on predefined or custom rules.
4. **Explore the Data**: Once the scan is complete, you can explore the data classifications, lineage, and other insights provided by Purview. This helps in understanding the structure and content of your data.
5. **Query the Data**: Use the query editor in the Azure portal to connect to your SQL database and run queries. Navigate to your SQL database in the Azure portal, select the query editor, and provide your credentials to start querying.

## How to remove data from Azure Purview

1. **Delete Individual Assets**:
   - Navigate to the asset you want to delete in the Purview portal.
   - Select the asset and click on the delete button. This will remove the asset and any child assets under its hierarchy. Find more information [here](https://learn.microsoft.com/en-us/purview/catalog-asset-details).
2. **Bulk Delete Assets**: Currently, the Purview user interface does not support bulk deletion of assets directly. However, you can use REST APIs to delete multiple assets. You will need to get the GUIDs of the assets you want to delete and use the `DELETE` method with the appropriate endpoint. Find more information about it [here](https://learn.microsoft.com/en-us/answers/questions/805790/delete-multiple-assets-in-purview).
3. **Remove Data Source**: If you want to remove an entire data source, you can unregister it from the Purview portal. This will remove all associated metadata and classifications. Find more information [here](https://learn.microsoft.com/en-us/purview/catalog-asset-details).
4. **Considerations**:
   - Ensure you have the necessary permissions to delete assets or data sources.
   - Be aware that deleting assets will also remove any associated metadata and lineage information.

## Restoring deleted information in Azure Purview 

| **Scenario**                | **Description**               |
|-----------------------------|-------------------------  |
| **Permanent Deletion**      | When you delete an asset using the delete button in Azure Purview, it is permanently deleted. This means that the asset and its metadata are removed from the catalog.  |
| **Reingestion**             | If the asset was ingested from a data source, you can run a full scan on that source again. This will reingest the asset into the Purview catalog, effectively restoring it.      |
| **Backup and Disaster Recovery** | Azure Purview does not currently support automated backup and disaster recovery (BCDR). However, you can manually create a secondary Purview account in another region to serve as a backup. This involves duplicating all activities performed on the primary account to the secondary account. |
| **Manual Restoration**      | For more complex scenarios, you might need to manually restore data using scripts or APIs. This requires maintaining a backup of your metadata and configurations.     |

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
