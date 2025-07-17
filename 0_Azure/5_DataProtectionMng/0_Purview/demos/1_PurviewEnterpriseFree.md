# Microsft Purview Enterprise - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------


<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [What's new in Microsoft Purview](https://learn.microsoft.com/en-us/purview/whats-new)
- [Pricing - Microsoft Purview](https://azure.microsoft.com/en-us/pricing/details/purview/)
- [Pricing guidelines for classic Microsoft Purview data governance](https://learn.microsoft.com/en-us/purview/concept-guidelines-pricing)
- [Purview how to upgrade from free to enterprise](https://learn.microsoft.com/en-us/purview/upgrade)
- [What's available in the free version of Microsoft Purview governance solutions?](https://learn.microsoft.com/en-us/purview/free-version)
- [Applications available in free vs enterprise](https://learn.microsoft.com/en-us/purview/free-version#applications-available-in-free-vs-enterprise)
- [Set up authentication using service principal](https://learn.microsoft.com/en-us/purview/tutorial-using-rest-apis#set-up-authentication-using-service-principal)
- [How to get lineage from Airflow into Microsoft Purview (Preview)](https://learn.microsoft.com/en-us/purview/how-to-lineage-airflow)
- [Microsoft Purview Data Catalog lineage user guide](https://learn.microsoft.com/en-us/purview/catalog-lineage-user-guide)

</details>

## Content 

- [Free vs Enterprise](#free-vs-enterprise)
- [Overview](#overview)
- [Microsoft Purview Pricing Model](#microsoft-purview-pricing-model)
    - [Key Differences](#key-differences)
- [How Microsoft Purview can be used](#how-microsoft-purview-can-be-used)
    - [Scenario 1: Data Governance for a Financial Institution](#scenario-1-data-governance-for-a-financial-institution)
    - [Scenario 2: Data Protection for a Healthcare Provider](#scenario-2-data-protection-for-a-healthcare-provider)
    - [Scenario 3: Data Analytics for an E-commerce Company](#scenario-3-data-analytics-for-an-e-commerce-company)
    - [Scenario 4: Compliance Management for a Global Enterprise](#scenario-4-compliance-management-for-a-global-enterprise)
- [Examples of use cases](#examples-of-use-cases)
- [Collect metadata information from Apache Airflow](#collect-metadata-information-from-apache-airflow)

## Free vs Enterprise

> `Purview Free`: Provides basic data governance capabilities, suitable for small-scale or initial exploration of Purview’s features. It includes basic cataloging, limited data discovery, and basic compliance tools. <br/>
> `Purview Enterprise`: Offers comprehensive data governance, protection, and compliance features. It supports a wide range of data sources, advanced classification, full DLP, information protection, compliance management, and seamless integration with Azure services.

| **Feature**                        | **Purview Free**                                                                                       | **Purview Enterprise**                                                                                       |
|------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Data Catalog**                   | Basic cataloging capabilities. <br> Limited to 1,000 annotated assets.                            | Full cataloging capabilities. <br> No limit on the number of annotated assets.                         |
| **Data Discovery**                 | Limited to Azure and Microsoft Fabric resources. <br> Auto discovery of Azure data sources.                                                  | Supports a wide range of data sources, including on-premises, multicloud, and SaaS applications. <br> Automated scans for the hybrid data estate.       |
| **Data Lineage**                   | Basic lineage tracking for a limited set of data sources.                                         | Comprehensive lineage tracking across all supported data sources.                                      |
| **Data Classification**            | Basic classification capabilities. <br> Definition and manual application of classifications and terms.                                                                | Advanced classification with automatic labeling and sensitivity labels. <br> Automated application of classifications and terms.                                |
| **Data Loss Prevention (DLP)**     | Not included.                                                                                     | Full DLP capabilities to prevent unauthorized sharing of sensitive information.                        |
| **Information Protection**         | Not included.                                                                                     | Includes encryption and access controls to protect sensitive data.                                     |
| **Compliance Management**          | Basic compliance tools.                                                                           | Comprehensive compliance management, including Compliance Manager and audit capabilities.              |
| **Data Quality**                   | Basic data profiling.                                                                             | Advanced data quality features, including quality rules and continuous monitoring.                     |
| **Insider Risk Management**        | Not included.                                                                                     | Full insider risk management capabilities to detect and respond to potential data leaks.               |
| **eDiscovery**                     | Not included.                                                                                     | Full eDiscovery capabilities for legal and compliance investigations.                                  |
| **Integration with Azure Services**| Limited integration with Azure services.                                                          | Seamless integration with a wide range of Azure services, including Synapse Analytics, SQL, and Power BI. |
| **Data Map**                       | Basic data map capabilities. <br> Manual creation of assets using the data map APIs.                                                                      | Full data map with detailed visualizations and relationship tracking. <br> Full use of Microsoft Purview's REST APIs.                                  |
| **Monitoring and Reporting**       | Basic monitoring and reporting.                                                                   | Advanced monitoring and reporting, including Data Estate Insights.                                     |
| **User Access**                    | Limited to data curators. <br> Role group access control to platform and apps.                                                                         | Full access for all users, including data stewards and analysts. <br> Fine-grained, collection-level access control to platform and apps.                                       |
| **Support and SLA**                | Community support.                                                                                | Enterprise-grade support and SLA.                                                                      |
| **Workflows**                      | Not included.                                                                                     | Included.                                                                                              |
| **Business Rules**                 | Not included.                                                                                     | Included.                                                                                              |
| **Support for Business Assets and Managed Attributes** | Not included.                                                                                     | Included.                                                                                              |
| **Descriptions, Tags, and Contacts** | Manual descriptions, tags, and contacts.                                                                                     | Manual and bulk descriptions, tags, and contacts.                                                                                              |

## Overview 

> Keypoints of Microsoft Purview: <br/>
> 1. `Integration with Microsoft Ecosystem`: Purview offers deep integration with Azure, Power BI, and Microsoft 365, providing a seamless experience for organizations already using these tools. <br/>
> 2. `Advanced Governance and Compliance`: Purview provides robust governance and compliance features, ensuring your data management practices meet regulatory standards. <br/>
> 3. `AI-Powered Search and Discovery`: With AI-driven capabilities, Purview enhances data discovery and classification, making it easier to find and manage data assets. <br/>
> 4. `Enterprise-Grade Security`: Leveraging Azure's security infrastructure, Purview offers top-notch security features to protect your data. <br/>
> 5. `Cost-Effective`: For organizations using Azure, Purview can be a more cost-effective solution due to its deep integration with Azure services. <br/>

| Feature/Tool          | Microsoft Purview         | Atlan                      | Alation                    | Collibra                   | Informatica               |
|-----------------------|---------------------------|----------------------------|----------------------------|---------------------------|---------------------------|
| **Data Lineage**      | End-to-end lineage, integrates with Azure Data Factory, supports column-level and cross-system lineage | Visual lineage maps, supports column-level lineage, tracks data transformations and dependencies | Column-level lineage, impact analysis, automated lineage extraction | End-to-end lineage, automated data flow tracking, supports both technical and business lineage | Comprehensive lineage with data transformation tracking, supports column-level lineage |
| **Integration**       | Deep integration with Azure services, Power BI, Microsoft 365, supports various data sources and ETL tools | Integrates with Snowflake, Databricks, AWS, GCP, BI tools, and more | Integrates with BI tools, databases, cloud services, and data lakes | Extensive integrations with enterprise systems, cloud platforms, and BI tools | Broad integration support including cloud and on-premises systems, supports ETL tools |
| **Data Governance**   | Advanced governance, integrates with Azure Policy, Microsoft Information Protection, role-based access control, compliance tracking | Role-based access control, data quality rules, policy management | Policy management, data stewardship, role-based access control, data quality monitoring | Data stewardship, policy management, data quality rules, compliance tracking | Data quality management, policy enforcement, role-based access control, compliance tracking |
| **Data Discovery**    | AI-powered search and discovery, integrates with Azure Cognitive Services, metadata tagging, data profiling | AI-powered search with NLP, metadata tagging, data profiling | Advanced search with ML, metadata tagging, data profiling | Comprehensive search with metadata tagging, data profiling, and classification | AI-driven data discovery, metadata management, data profiling |
| **Collaboration**     | Integrated collaboration tools, supports Microsoft Teams, data annotations, and sharing | Collaborative workspace, supports team-based projects, data annotations | Collaborative features, data stewardship workflows, data annotations | Collaboration tools, data sharing, annotations, and workflows | Collaborative environment, data sharing, version control, data annotations |
| **Security**          | Enterprise-grade security, integrates with Azure Security Center, encryption, access controls, compliance certifications | Encryption, access controls, audit logs, compliance certifications | Strong security features, audit trails, compliance certifications | Robust security, data masking, encryption, compliance certifications | High security standards, data masking, encryption, audit logs |
| **Scalability**       | Highly scalable with Azure, supports large-scale data environments, elastic scaling | Cloud-native architecture, supports large-scale deployments | Scalable architecture, supports large datasets | Distributed architecture, supports large-scale deployments | Cloud and on-premises support, highly scalable |
| **Cost**              | Cost-effective for Azure users, pay-as-you-go model, subscription-based options | Competitive pricing, flexible plans, usage-based pricing | Premium pricing, enterprise features, subscription-based | Premium pricing, extensive features, subscription-based | Premium pricing, comprehensive support, subscription-based |

## Microsoft Purview Pricing Model

> Microsoft Purview offers a flexible pricing model based on several components:

| Pricing Aspect              | Description                                                                 | Details                                                                                           |
|-----------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Data Map Population**     | Charges based on the number of data assets scanned and classified           | - **Cost Basis**: Number of data assets scanned<br>- **Usage**: Suitable for organizations with varying data volumes<br>- **Example**: Scanning 10,000 data assets may incur different costs compared to 50,000 data assets |
| **Data Map Enrichment**     | Costs associated with processing information to optimize storage and generate insights | - **Cost Basis**: Processing and enrichment activities<br>- **Usage**: Enhances data quality and insights<br>- **Example**: Enriching metadata for better searchability and classification |
| **Subscription-Based Licensing** | Some capabilities offered as subscription-based, with costs varying based on usage and specific features | - **Cost Basis**: Subscription fees based on selected features<br>- **Usage**: Predictable costs for budgeting<br>- **Example**: Subscribing to advanced governance features or AI-powered search capabilities |
| **Pay-As-You-Go**           | Pricing is scalable and depends on the number of data assets scanned        | - **Cost Basis**: Actual usage<br>- **Usage**: Flexible and scalable, suitable for businesses of all sizes<br>- **Example**: Paying for the exact number of data assets scanned each month |

### Key Differences

> - `Scalability`: Purview's pay-as-you-go model allows for cost-effective scaling based on actual usage, which can be more economical for organizations with fluctuating data needs. <br/>
> - `Integration with Azure`: For organizations already using Azure, Purview can offer additional cost savings due to its deep integration with Azure services.

| Aspect                  | Microsoft Purview         | Atlan                      | Alation                    | Collibra                   | Informatica               |
|-------------------------|---------------------------|----------------------------|----------------------------|---------------------------|---------------------------|
| **Pricing Structure**   | Pay-As-You-Go, Subscription-Based | Tiered Pricing (Starter, Premier, Enterprise) | Subscription-Based, Custom Pricing | Subscription-Based, Annual Licensing | Consumption-Based, IPU (Informatica Processing Unit) Pricing |
| **Cost**                | Scalable based on usage   | Starts at $500/month for Starter Plan | Starts at $60,000/year. [Click here for more information](https://data.world/blog/alation-pricing/) | Starts at $170,000/year. [Click here for more information](https://data.world/blog/collibra-pricing/) | Flexible, based on usage. [Click here for more information](https://www.informatica.com/products/cloud-integration/pricing.html) |
| **Customization**       | Flexible, based on data assets scanned | Custom pricing for Enterprise Plan | Custom pricing based on features and usage | Custom pricing based on contract term | Customizable based on IPU consumption. [Click here for more information](https://www.informatica.com/blogs/the-truth-about-informatica-pricing.html) |
| **Trial Options**       | Free trial available      | Free trial for Starter and Premier Plans. [Click here for more information](https://syncari.com/blog/what-is-informatica/) | Free trial available upon request | Free demo available. [Click here for more information](https://www.selecthub.com/p/business-intelligence-tools/collibra/) | Free trial available. [Click here for more information](https://www.informatica.com/products/cloud-integration/pricing.html) |

## How Microsoft Purview can be used 

Find below different scenarios to manage data governance, protection, and compliance:

| **Scenario**                             | **Description**                                                                                       | **Steps**                                                                                                                                                                                                                       |
|------------------------------------------|-------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Data Governance for a Financial Institution** | Demonstrates how Purview can be used to discover, catalog, and manage data assets, ensuring data quality and compliance in a financial setting. | 1. Data Discovery: Scan all data sources (e.g., SQL databases, Azure Blob Storage) to discover and catalog data assets. <br> 2. Metadata Collection: Collect metadata and classify data based on sensitivity (e.g., PII, financial data). <br> 3. Data Cataloging: Register discovered data assets in the Purview Data Catalog for easy search and access. <br> 4. Data Lineage: Capture and visualize data lineage to understand data flow and transformations. <br> 5. Data Stewardship: Assign data stewards to manage and curate data assets, ensuring data quality and compliance. <br> 6. Compliance Management: Implement governance policies and use compliance tools to meet regulatory requirements (e.g., GDPR, CCPA). <br> 7. Monitoring and Reporting: Continuously monitor data quality and generate compliance reports. |
| **Data Protection for a Healthcare Provider** | Shows how Purview helps classify and protect sensitive healthcare data, implement data loss prevention policies, and ensure compliance with healthcare regulations. | 1. Data Classification: Automatically classify sensitive data (e.g., patient records) using Purview's classification tools. <br> 2. Data Loss Prevention (DLP): Implement DLP policies to prevent unauthorized sharing of sensitive information. <br> 3. Information Protection: Apply encryption and access controls to protect sensitive data throughout its lifecycle. <br> 4. Insider Risk Management: Monitor and manage insider risks by detecting and responding to potential data leaks or policy violations. <br> 5. Audit and Compliance: Use audit tools to track user activities and changes, ensuring compliance with healthcare regulations (e.g., HIPAA). |
| **Data Analytics for an E-commerce Company** | Highlights how Purview supports data ingestion, processing, and analytics, while maintaining data lineage, quality, and governance in an e-commerce environment. | 1. Data Ingestion: Ingest data from various sources (e.g., web servers, sales databases) into Azure Synapse Analytics. <br> 2. Data Processing: Use Azure Synapse to process and transform data for analytics. <br> 3. Data Lineage: Capture data lineage to understand the flow and transformations of data from source to analytics. <br> 4. Data Cataloging: Register processed data assets in the Purview Data Catalog for easy discovery and access. <br> 5. Data Quality: Profile data to assess its quality and define quality rules to maintain high standards. <br> 6. Reporting and Visualization: Use Power BI to create reports and dashboards, ensuring data governance and security. |
| **Compliance Management for a Global Enterprise** | Illustrates how Purview can be used to manage compliance across a global organization, including data discovery, classification, policy implementation, and continuous monitoring. | 1. Data Discovery: Scan and catalog data assets across on-premises and cloud environments. <br> 2. Data Classification: Classify data based on sensitivity and regulatory requirements. <br> 3. Compliance Assessments: Use Purview Compliance Manager to perform assessments and identify compliance gaps. <br> 4. Policy Implementation: Implement data governance and compliance policies to address identified gaps. <br> 5. Continuous Monitoring: Continuously monitor compliance status and generate reports for regulators and stakeholders. <br> 6. Incident Response: Use audit and investigation tools to respond to compliance incidents and mitigate risks. |

### Scenario 1: Data Governance for a Financial Institution

1. **Set Up Microsoft Purview Account**
    - **Sign Up**:
      - Go to the Microsoft Purview portal.
      - Click on `Start free` or `Get started` to sign up for an account.
    - **Create Purview Account**:
      - In the Azure portal, search for `Purview`.
      - Click on `Create` to set up a new Purview account.
      - Fill in the required details such as subscription, resource group, and account name.
      - Choose the region and pricing tier.
      - Review and create the account.
2. **Data Domain**:
    - Create a domain that match your org key business
      - Create collections:
        - Go to the `Collections` section.
        - Click on `New Collection` and provide a name and description.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/369a6a03-be3a-46d2-8246-806bf7b26f4b">

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/2ab92b29-75d1-482f-afd8-7c99d3ffbed6">

> [!NOTE]
> Remember to add purview identity with required RBAC (e.g admin) within the data source desired:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/5f7b5e29-6e36-4a38-9a51-26d43451bf41">

> Also add the required roles within the Purview portal, for each collection>

<img width="550" alt="image" src="https://github.com/user-attachments/assets/afc237d3-3765-4ecb-a56b-23dd04eb1a46">

3. **Data Discovery**

    - **Navigate to Purview Portal**: Access the Purview portal from the Azure portal by selecting your Purview account.
    - **Register Data Sources**:
      - Go to the `Data Map` section.
      - Click on `Register` and select the data source type (e.g., Azure SQL Database, Azure Blob Storage).
      - Provide connection details:
        - For Azure SQL Database: Enter the server name, database name, and authentication details.
        - For Azure Blob Storage: Enter the storage account name and access key.
        
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/db0de8c7-d5fb-4c21-8a36-753225f8a737">

    - **Configure Scan Settings**:
      - Set the scan scope: Select specific databases, tables, or containers to scan.
      - Schedule the scan frequency: Choose how often the scan should run (e.g., daily, weekly).
      - Configure advanced settings: Set up filters to include or exclude specific data assets.
    - **Initiate Scan**:
      - Click on `Start Scan` to begin the discovery process.
      - Monitor the scan progress and review the results once completed.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/9c5d6070-84d8-47f4-a5a5-5509d68da579">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/1b377ccc-21ed-4bfe-8360-e253bced4f16">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/9c8445ba-e662-4a2c-81c4-fee17402094a">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/59fde3a4-471d-4106-b9aa-71ace7b7cb69">

4. **Metadata Collection**
    - **Review Discovered Assets**: Go to the `Data Map` section and review the list of discovered data assets.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/bb514fe4-1d44-40d6-809a-b1e3d578a05d">

    - **Automatic Classification**:
      - Go to the `Classifications` section.
      - Enable automatic classification:
        - Select the classifiers you want to apply (e.g., PII, financial data).
        - Configure classification rules if needed.
    - **Manual Metadata Addition**:
      - Edit metadata for specific data assets:
        - Click on a data asset to view its details.
        - Add custom tags, descriptions, and contact information for data stewards.

5. **Data Cataloging**
    - **Register Data Assets**: Ensure all scanned assets are listed in the `Data Catalog` section.
    - **Organize Data Assets**:
        - Add relevant data assets to the collection.
      - Define glossary terms:
        - Go to the `Glossary` section.
        - Click on `New Term` to create glossary terms.
        - Link glossary terms to data assets.
    - **Add Descriptions, Tags, and Contacts**:
      - Edit each asset:
        - Click on a data asset to view its details.
        - Add detailed descriptions, relevant tags, and contact information for data stewards.

6. **Data Lineage**
    - **Enable Lineage Tracking**:
      - Go to the `Lineage` section.
      - Ensure lineage tracking is enabled for the registered data sources.
    - **Visualize Data Flow**:
      - Use lineage visualization tools:
        - Navigate to the `Lineage` section.
        - Select a data asset to view its lineage.
        - Explore the data flow and transformations.
    - **Analyze Lineage**:
      - Identify upstream and downstream dependencies:
        - Use the lineage graph to trace data dependencies.
        - Analyze the impact of changes to data assets.
7. **Data Stewardship**
    - **Assign Data Stewards**:
      - Go to the `Roles` section.
      - Assign data steward roles:
        - Select a collection or data asset.
        - Assign users as data stewards.
    - **Monitor Data Quality and Governance**:
      - Set up dashboards:
        - Go to the `Monitoring` section.
        - Create dashboards to track data quality metrics and governance activities.
    - **Curate Data Assets**:
      - Regularly review and update metadata, classifications, and lineage information:
        - Schedule periodic reviews.
        - Make necessary updates to ensure data accuracy and compliance.
8. **Compliance Management**
    - **Implement Governance Policies**:
      - Go to the `Policies` section.
      - Define and apply data governance policies:
        - Create new policies for data retention, access controls, and usage.
        - Apply policies to relevant data sources.
    - **Configure Data Retention and Access Policies**:
      - Set up policies to manage data lifecycle and access permissions:
        - Define retention periods for different data types.
        - Configure access controls to restrict data access based on roles.
    - **Use Compliance Manager**:
      - Perform compliance assessments:
        - Go to the `Compliance Manager` section.
        - Select relevant compliance templates (e.g., GDPR, CCPA).
        - Run assessments and review the results.
      - Generate compliance reports: Create reports to document compliance status and actions taken.
9. **Monitoring and Reporting**
    - **Set Up Monitoring Dashboards**:
      - Go to the `Monitoring` section.
      - Create dashboards:
        - Select metrics to monitor (e.g., data quality, compliance status).
        - Configure visualizations and alerts.
    - **Continuous Monitoring**:
      - Use real-time alerts and notifications:
        - Set up alerts for data quality issues and compliance risks.
        - Configure notifications to inform relevant stakeholders.
    - **Generate and Review Compliance Reports**:
      - Regularly generate reports:
        - Go to the `Reports` section.
        - Create and schedule reports to review compliance status and governance effectiveness.

### Scenario 2: Data Protection for a Healthcare Provider

1. **Data Classification**
    - **Navigate to the Microsoft Purview portal**:
      - Access the Purview portal from the Azure portal by selecting your Purview account.
    - **Set up a new data source connection**:
      - Go to the `Data Map` section.
      - Click on `Register` and select the data source type (e.g., Azure SQL Database, Azure Blob Storage).
      - Provide connection details:
        - For Azure SQL Database: Enter the server name, database name, and authentication details.
        - For Azure Blob Storage: Enter the storage account name and access key.
    - **Configure the scan settings and initiate the scan**:
      - Set the scan scope: Select specific databases, tables, or containers to scan.
      - Schedule the scan frequency: Choose how often the scan should run (e.g., daily, weekly).
      - Configure advanced settings: Set up filters to include or exclude specific data assets.
      - Click on `Start Scan` to begin the discovery process.
      - Monitor the scan progress and review the results once completed.
    - **Automatically classify sensitive data**:
      - Go to the `Classifications` section.
      - Enable automatic classification:
        - Select the classifiers you want to apply (e.g., PII, patient records).
        - Configure classification rules if needed.
2. **Data Loss Prevention (DLP)**
    - **Navigate to the DLP section in the Purview portal**:
      - Access the DLP section from the main menu.
    - **Create and configure DLP policies**:
      - Click on `Create Policy`.
      - Define the policy name and description.
      - Specify the conditions for the policy (e.g., detecting sensitive information in emails or documents).
      - Set the actions to be taken when a policy violation is detected (e.g., block sharing, notify admin).
    - **Apply DLP policies to relevant data sources**:
      - Select the data sources to which the DLP policy should apply.
      - Save and activate the policy.
    - **Monitor for policy violations**:
      - Go to the `DLP Reports` section.
      - Review the reports to monitor for any policy violations and take necessary actions.
3. **Information Protection**
    - **Navigate to the Information Protection section in the Purview portal**:
      - Access the Information Protection section from the main menu.
    - **Apply encryption and access controls**:
      - Click on `Create Label`.
      - Define the label name and description.
      - Configure encryption settings (e.g., specify who can access the data and what actions they can perform).
      - Apply the label to sensitive data.
    - **Monitor and manage access to sensitive data**:
      - Go to the `Label Activity Explorer` section.
      - Review the activity logs to monitor access to sensitive data and ensure compliance with policies.
4. **Insider Risk Management**
    - **Navigate to the Insider Risk Management section in the Purview portal**:
      - Access the Insider Risk Management section from the main menu.
    - **Configure policies to detect and respond to potential data leaks or policy violations**:
      - Click on `Create Policy`.
      - Define the policy name and description.
      - Specify the conditions for the policy (e.g., detecting unusual data access patterns).
      - Set the actions to be taken when a policy violation is detected (e.g., alert admin, restrict access).
    - **Monitor insider activities and investigate potential risks**:
      - Go to the `Risk Activity Explorer` section.
      - Review the activity logs to monitor insider activities and investigate any potential risks.
5. **Audit and Compliance**
    - **Navigate to the Audit section in the Purview portal**:
      - Access the Audit section from the main menu.
    - **Configure audit settings to track user activities and changes**:
      - Click on `Create Audit Log`.
      - Define the log name and description.
      - Specify the activities to be tracked (e.g., data access, modifications).
      - Set the retention period for the audit logs.
      - Save and activate the audit log.
    - **Generate audit reports to ensure compliance with healthcare regulations (e.g., HIPAA)**:
      - Go to the `Audit Reports` section.
      - Create and schedule audit reports to review user activities and ensure compliance with regulations.

### Scenario 3: Data Analytics for an E-commerce Company

1. **Data Ingestion**
    - **Set up data ingestion pipelines**:
      - Use Azure Data Factory or Azure Synapse Analytics.
      - Create a new pipeline:
        - In Azure Data Factory, go to the `Author` section and click on `New pipeline`.
        - In Azure Synapse Analytics, go to the `Integrate` section and click on `New pipeline`.
      - Add data source connectors:
        - For web servers: Use the HTTP connector to ingest web server logs.
        - For sales databases: Use the Azure SQL Database connector to ingest sales data.
    - **Ingest data from various sources**:
      - Configure the data source settings:
        - For HTTP connector: Enter the URL and authentication details.
        - For Azure SQL Database connector: Enter the server name, database name, and authentication details.
      - Set up data sinks:
        - Choose Azure Synapse Analytics as the destination.
        - Configure the destination settings (e.g., database, table).
    - **Monitor the data ingestion process**:
      - Go to the `Monitor` section in Azure Data Factory or Azure Synapse Analytics.
      - Check the pipeline runs to ensure data is being ingested correctly.
2. **Data Processing**
    - **Use Azure Synapse Analytics to process and transform the ingested data**:
      - Go to the `Data` section in Azure Synapse Analytics.
      - Create a new SQL script or Spark notebook to process the data.
    - **Apply necessary transformations and aggregations**:
      - Write SQL queries or Spark code to clean, transform, and aggregate the data.
      - Example transformations:
        - Remove duplicates.
        - Aggregate sales data by product category.
        - Enrich web server logs with geolocation data.
    - **Store the processed data**:
      - Save the processed data in a data warehouse or data lake:
        - Use Azure Synapse Analytics to create tables in a dedicated SQL pool.
        - Use Azure Data Lake Storage to store the processed data in Parquet or CSV format.
3. **Data Lineage**
    - **Enable lineage tracking in Azure Synapse Analytics**:
      - Go to the `Manage` section in Azure Synapse Analytics.
      - Enable data lineage tracking for the workspace.
    - **Capture data lineage**:
      - Ensure that all data processing activities are logged.
      - Use built-in lineage tracking features to capture the flow and transformations of data.
    - **Visualize the data lineage in the Purview portal**:
      - Go to the `Lineage` section in the Purview portal.
      - Select a data asset to view its lineage.
      - Explore the data flow and transformations.
4. **Data Cataloging**
    - **Register processed data assets in the Purview Data Catalog**:
      - Go to the `Data Map` section in the Purview portal.
      - Ensure that all processed data assets are listed.
    - **Organize data assets**:
      - Create collections:
        - Go to the `Collections` section.
        - Click on `New Collection` and provide a name and description.
        - Add relevant data assets to the collection.
      - Define glossary terms:
        - Go to the `Glossary` section.
        - Click on `New Term` to create glossary terms.
        - Link glossary terms to data assets.
    - **Add descriptions, tags, and contacts**:
      - Edit each asset:
        - Click on a data asset to view its details.
        - Add detailed descriptions, relevant tags, and contact information for data stewards.
5. **Data Quality**
    - **Profile data to assess its quality**:
      - Go to the `Data Quality` section in the Purview portal.
      - Select a data asset to profile.
      - Review the data quality metrics (e.g., completeness, accuracy).
    - **Define and enforce data quality rules**:
      - Create data quality rules:
        - Go to the `Data Quality Rules` section.
        - Click on `New Rule` and define the rule conditions (e.g., no null values, valid email format).
      - Apply the rules to relevant data assets.
    - **Continuously monitor data quality**:
      - Set up data quality dashboards:
        - Go to the `Monitoring` section.
        - Create dashboards to track data quality metrics.
      - Address any data quality issues:
        - Review the data quality reports and take corrective actions as needed.
6. **Reporting and Visualization**
    - **Use Power BI to create reports and dashboards**:
      - Connect Power BI to Azure Synapse Analytics or Azure Data Lake Storage.
      - Create new reports and dashboards:
        - Use Power BI Desktop to design reports.
        - Publish the reports to the Power BI service.
    - **Ensure data governance and security**:
      - Integrate Power BI with Purview:
        - Go to the `Power BI` section in the Purview portal.
        - Enable data governance features for Power BI datasets.
    - **Share reports and dashboards with stakeholders**:
      - Configure access controls:
        - Set up roles and permissions in Power BI to control access to reports and dashboards.
      - Share the reports and dashboards:
        - Use the Power BI service to share reports with stakeholders while maintaining data security.

### Scenario 4: Compliance Management for a Global Enterprise

1. **Data Discovery**
    - **Scan and catalog data assets across on-premises and cloud environments using Purview**:
      - Navigate to the Microsoft Purview portal.
      - Go to the `Data Map` section.
    - **Set up data source connections and configure scan settings**:
      - Click on `Register` and select the data source type (e.g., Azure SQL Database, Azure Blob Storage, on-premises SQL Server).
      - Provide connection details:
        - For Azure SQL Database: Enter the server name, database name, and authentication details.
        - For Azure Blob Storage: Enter the storage account name and access key.
        - For on-premises SQL Server: Use the self-hosted integration runtime to connect.
      - Configure scan settings:
        - Set the scan scope: Select specific databases, tables, or containers to scan.
        - Schedule the scan frequency: Choose how often the scan should run (e.g., daily, weekly).
        - Configure advanced settings: Set up filters to include or exclude specific data assets.
    - **Initiate scans to discover and catalog data assets**:
      - Click on `Start Scan` to begin the discovery process.
      - Monitor the scan progress and review the results once completed.
2. **Data Classification**
    - **Classify data based on sensitivity and regulatory requirements using Purview's classification tools**:
      - Go to the `Classifications` section.
      - Enable automatic classification:
        - Select the classifiers you want to apply (e.g., PII, financial data, health data).
        - Configure classification rules if needed.
    - **Apply sensitivity labels and classifications to discovered data assets**:
      - Review the automatically classified data.
      - Manually apply or adjust sensitivity labels and classifications as needed.
    - **Review and refine classifications as needed**:
      - Regularly review the classifications to ensure accuracy.
      - Update classification rules and labels based on new regulatory requirements or business needs.
3. **Compliance Assessments**
    - **Use Purview Compliance Manager to perform compliance assessments**:
      - Navigate to the `Compliance Manager` section in the Purview portal.
      - Select relevant compliance templates (e.g., GDPR, CCPA, HIPAA).
      - Configure the assessment settings and scope.
    - **Identify compliance gaps and areas for improvement**:
      - Run the compliance assessments.
      - Review the assessment results to identify compliance gaps and areas for improvement.
    - **Generate compliance reports and review assessment results**:
      - Go to the `Reports` section.
      - Create and schedule compliance reports to document assessment results and actions taken.
4. **Policy Implementation**
    - **Implement data governance and compliance policies using Purview's policy management tools**:
      - Go to the `Policies` section.
      - Click on `Create Policy` and define the policy name and description.
      - Specify the policy conditions (e.g., data retention, access controls, usage).
    - **Configure data retention, access, and usage policies**:
      - Define retention periods for different data types.
      - Configure access controls to restrict data access based on roles.
      - Set usage policies to ensure data is used in compliance with regulations.
    - **Apply policies to relevant data sources and monitor for compliance**:
      - Select the data sources to which the policies should apply.
      - Save and activate the policies.
      - Monitor the policies to ensure compliance.
5. **Continuous Monitoring**
    - **Set up monitoring dashboards in the Purview portal**:
      - Go to the `Monitoring` section.
      - Create dashboards to track compliance status and data quality metrics.
    - **Continuously monitor compliance status and data quality**:
      - Use real-time alerts and notifications:
        - Set up alerts for compliance issues and data quality risks.
        - Configure notifications to inform relevant stakeholders.
    - **Generate and review compliance reports regularly**:
      - Go to the `Reports` section.
      - Create and schedule reports to review compliance status and governance effectiveness.
6. **Incident Response**
    - **Use Purview's audit and investigation tools to respond to compliance incidents**:
      - Navigate to the `Audit` section in the Purview portal.
      - Configure audit settings to track user activities and changes.
      - Use the `Investigation` tools to analyze audit logs and identify incidents.
    - **Investigate potential compliance violations and take corrective actions**:
      - Review the audit logs to investigate potential compliance violations.
      - Take corrective actions to address the violations.
    - **Document incident responses and review for continuous improvement**:
      - Document the incident responses and actions taken.
      - Review the incident responses to identify areas for improvement and update policies as needed.

## Examples of use cases

<img width="550" alt="image" src="https://github.com/user-attachments/assets/cdbc5769-ea4a-402f-89fb-7a812e14e501">

## Collect metadata information from Apache Airflow

> This capability is currently in public preview and is achieved through integration with **OpenLineage**, an open framework for data lineage collection and analysis.

How it works:
1. **Enable OpenLineage in Airflow**: By enabling OpenLineage in your Airflow instance, metadata and lineage information about jobs and datasets are automatically tracked as Directed Acyclic Graphs (DAGs) execute.
2. **Azure Event Hubs**: The tracked metadata and lineage information are sent to an Azure Event Hubs instance that you configure.
3. **Microsoft Purview**: Purview subscribes to the events from Azure Event Hubs, parses them, and ingests the metadata and lineage into the data map.

This integration supports capturing metadata such as:
- Airflow workspace
- Airflow DAG
- Airflow task

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-354-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
