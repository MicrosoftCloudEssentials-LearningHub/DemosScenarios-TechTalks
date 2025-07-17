# Fabric: Overview of Configuration Settings

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [What is the admin portal?](https://learn.microsoft.com/en-us/fabric/admin/admin-center)

</details>

## Fabric Admin Portal 

1. [Tenant settings (New)](#tenant-settings)
2. Usage metrics
3. Users
4. Premium Per User
5. Audit logs
6. Domains (New)
7. Workloads
8. Tags (preview) (New)
9. Capacity settings
   - Refresh summary
10. [Embed Codes](#embed-codes)
11. Organizational visuals
12. Azure connections
13. Workspaces
14. [Custom branding](#custom-branding)
15. Protection metrics
16. Fabric identities
17. Featured content
18. Help + support

## Tenant settings 

### Microsoft Fabric 

| **Configuration Setting** | **Description and Context** |
|---------------------------|-----------------------------|
| **Users can create Fabric items** | Turn on this setting to allow users to use production-ready features to create Fabric items, such as reports, dashboards, and datasets. Turning off this setting doesn't impact users’ ability to create Power BI items. This setting can be managed at both the tenant and the capacity levels. <br/> **Technical Context**: Fabric items are integral to the Microsoft Fabric ecosystem, enabling comprehensive data insights and business intelligence. |
| **Users can create and use ADLS Mount items (preview)** | Turn on this setting to allow users to create and utilize Azure Data Lake Storage (ADLS) mount points to connect and manage large-scale data storage. Users can also connect and test existing ADF pipelines in Microsoft Fabric. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: ADLS mount points facilitate seamless integration with Azure's scalable storage solutions, supporting big data analytics and machine learning workflows. |
| **Users can create Healthcare Cohort items (preview)** | Turn on this setting to allow users to explore and create healthcare cohorts using natural language from the multi-modal healthcare data estate provided by the Healthcare solutions item. The data may contain Protected Health Information (PHI). Collaborators with workspace access can view, build on, and modify the healthcare cohort items within that workspace. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Healthcare cohorts enable advanced analytics on patient groups, leveraging natural language processing (NLP) to interact with complex healthcare data. |
| **Retail dataflows (in preview)** | Turn on this setting to allow users to create dataflows specifically for retail data, automating data transformation and preparation processes. This setting helps manage and analyze retail data and can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Retail dataflows streamline the ETL (Extract, Transform, Load) process for retail data, ensuring data consistency and accuracy across various retail operations. |
| **Users can create and use data workflows (preview)** | Turn on this setting to allow users to create and manage data workflows powered by Apache Airflow. This setting offers an integrated Apache Airflow runtime environment, enabling users to author, execute, and schedule Python DAGs. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Apache Airflow is a powerful platform for orchestrating complex data workflows, providing robust scheduling and monitoring capabilities for Python-based Directed Acyclic Graphs (DAGs). |
| **API for GraphQL (preview)** | Using the API for GraphQL, your applications can leverage the standard GraphQL language to access a variety of data sources within Microsoft Fabric. Data Warehouses, Lakehouses, and operational databases like Azure SQL can be easily accessed from any application that uses a GraphQL client library. Turn on to allow users in your organization to create API for GraphQL items. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: GraphQL APIs enable precise data queries, reducing over-fetching and under-fetching of data, and improving performance and efficiency in data retrieval. |
| **Enable Real-Time Dashboards (previews)** | Turn on this setting to allow users to create Real-Time Dashboards that are natively integrated with KQL databases using Kusto Query Language (KQL). This fully integrated dashboard experience provides improved query and visualization performance, and easier data exploration. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Real-time dashboards leverage KQL for efficient data querying and visualization, enhancing the ability to monitor live data and make timely decisions. KQL integration ensures high performance and seamless data exploration. |
| **Users can edit and create org apps (preview)** | Turn on this setting to let users create org apps as items. Users with access will be able to view them. By turning on this setting, you agree to the Preview Terms. If turned off, any org app items created will be hidden until this setting is turned on again. The prior version of workspace apps will still be available. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Organizational apps can integrate various business processes and data sources, providing customized solutions that enhance operational efficiency and user engagement. |
| **Product Feedback** | Turn on this setting to allow Microsoft to prompt users for feedback through in-product surveys within Microsoft Fabric and Power BI. Microsoft will use this feedback to help improve product features and services. User participation is voluntary. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Collecting product feedback helps identify areas for improvement, prioritize feature development, and address user concerns, contributing to a better overall user experience. |
| **Copy Job (in preview)** | Turn on this setting to allow users to simply move data from any sources into any destinations without creating a pipeline or dataflow. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Copying jobs simplifies data transfer processes, enabling quick and efficient data movement without the need for complex pipeline configurations. This is particularly useful for straightforward data migration tasks. |
| **Users can share all Skill item types** | Turn on this setting to allow users to create natural language data question and answer (Q&A) experiences using generative AI and then save them as AI skill items. AI skill items can be shared with others in the organization. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: AI skill items leverage generative AI to create interactive Q&A experiences, enhancing knowledge sharing and collaboration within the organization. |
| **Discover and Use Metrics** | Turn on this setting to let users in the organization search for, view, and use metrics. They can use metrics to create new items, such as reports, across Fabric. By turning this setting on, you agree to the Preview Terms. If turned off, any metrics and metric sets created will be hidden until this setting is turned on again. Semantic models underlying metric sets and downstream items created from metrics will always be visible. <br/> **Technical Context**: Metrics provide quantifiable measures that can be used to track performance and outcomes. Enabling this setting allows users to leverage these metrics for creating insightful reports and dashboards, enhancing data-driven decision-making. |
| **Mirror Azure Databricks Catalogs** | Turn on this setting to allow users to add Azure Databricks catalogs, schemas, and tables to Fabric workspaces and explore data from Fabric without needing to move data. This setting ensures data availability and reliability by creating copies of data assets for redundancy or backup purposes. This setting can be managed at both the tenant and capacity levels. <br/> **Technical Context**: Mirroring involves creating an exact copy of a dataset or database in another location. This is crucial for data redundancy, ensuring that data is available even if the primary source fails. Enhances data reliability and availability, supports disaster recovery, and allows for seamless data exploration and analysis without data movement. |

### Help and support settings

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Publish "Get Help" information** | Turn on this setting to allow users in the tenant to access internal help and support resources directly from the Power BI help menu. This can be useful for providing customized support and guidance tailored to the organization's specific needs. <br/> **Technical Context**: Integrating internal help resources ensures that users have quick access to relevant support, reducing downtime and improving productivity. This can include links to internal documentation, support tickets, or contact information for the IT helpdesk. |
| **Receive email notifications for service outages or incidents** | Turn on this setting to ensure that administrators receive email notifications when there are service outages or incidents that impact their tenant. This helps in promptly addressing issues and minimizing disruption. <br/> **Technical Context**: Timely notifications about service outages or incidents enable administrators to take immediate action, ensuring continuity of service and reducing potential downtime. Administrators can stay informed about service disruptions through email notifications, allowing them to quickly address issues and communicate with affected users. |
| **Users can try Microsoft Fabric paid features** | Turn on this setting to allow users to sign up for a Microsoft Fabric trial, enabling them to try paid features for free for 60 days. After the trial period, users must upgrade to a paid license to continue using these features. <br/> **Technical Context**: Providing trial access to paid features allows users to evaluate the full capabilities of Microsoft Fabric, facilitating informed purchasing decisions. Offering a trial period for paid features allows users to explore advanced functionalities without immediate financial commitment, leading to higher adoption rates and better user engagement with the platform. |
| **Apply to: The entire organization / Specific security groups / Exclude specific security groups** | This option allows administrators to apply the settings to the entire organization, specific security groups, or exclude certain security groups. <br/> **Technical Context**: Granular control over settings application ensures that only relevant users or groups are affected, enhancing security and compliance. |
| **Show a custom message before publishing reports** | Turn on this setting to display a custom message to users attempting to publish a report in the tenant. This can be used to remind users of guidelines or policies before they publish their reports. <br/> **Technical Context**: Custom messages help enforce organizational policies and ensure that users are aware of important information before publishing reports, reducing the risk of non-compliance. Custom messages can serve as reminders for best practices, compliance requirements, or other important information that users need to consider before publishing their reports, helping maintain data quality and adherence to organizational standards. |


### Domain management settings

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Allow tenant and domain admins to override workspace assignments (preview)** | Turn on this setting to allow tenant and domain admins to reassign workspaces that were previously assigned to one domain to another domain. This setting applies to the entire organization. <br/> **Technical Context**: Enabling this setting provides flexibility in managing workspaces across different domains within the organization. It allows administrators to reassign workspaces as organizational structures or domain responsibilities change, ensuring that workspace assignments remain aligned with current administrative needs. This can be particularly useful in large organizations with multiple domains, where administrative control needs to be dynamic and adaptable. <br/> **Workspace Assignments**: Workspaces in Microsoft Fabric are collaborative environments where users can create, share, and manage content such as reports, dashboards, and datasets. Proper assignment of workspaces to domains ensures that the right administrative controls and access permissions are applied. <br/> **Domain Management**: Domains represent different administrative boundaries within an organization. They can be used to segment administrative responsibilities, manage access controls, and apply specific policies. Allowing admins to override workspace assignments helps maintain organizational efficiency and compliance with internal policies. <br/> **Flexibility and Adaptability**: This setting enhances the flexibility and adaptability of the organization's administrative structure. As teams and responsibilities evolve, admins can reassign workspaces to reflect these changes without disrupting ongoing work or access permissions. |

### Workspace settings

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Create workspaces** | Users in the organization can create app workspaces to collaborate on dashboards, reports, and datasets. This setting is disabled, meaning only an admin can create a workspace. <br/> **Technical Context**: Enabling this setting allows users to create collaborative environments where they can share and manage content. Disabling it centralizes control, ensuring that only administrators can create workspaces, which can help maintain governance and compliance. |
| **Use semantic models across workspaces** | Users in the organization can use semantic models across workspaces (build permission). This setting is disabled, meaning users cannot use semantic models across workspaces. <br/> **Technical Context**: Semantic models provide a unified view of data, enabling consistent data definitions and calculations across different reports and dashboards. Allowing their use across workspaces promotes data consistency and reusability, while disabling it can prevent unauthorized data access and modifications. |
| **Block users from reassigning personal workspaces (My Workspace)** | Block the ability for users to reassign their personal workspaces to other users. This setting applies to the entire organization. <br/> **Technical Context**: Personal workspaces are intended for individual use. Blocking reassignment ensures that personal data and configurations remain private and are not inadvertently shared or transferred to others, enhancing data security and privacy. |
| **Define workspace retention period** | Retain data stored in app workspaces for a specified retention period during which you can restore a deleted workspace and its contents. After this period expires, the workspace and its contents are permanently deleted and cannot be restored. Options include retaining data indefinitely or for a specified number of days (7-90). This setting applies to the entire organization. <br/> **Technical Context**: Defining a retention period helps manage storage and compliance requirements. It ensures that data is available for recovery within a specified timeframe, supporting business continuity and data governance. Indefinite retention can be useful for long-term projects, while a defined period helps manage storage costs and data lifecycle. |

### Power BI visuals

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Allow visuals created using the Power BI SDK** | This setting allows you to add new, uncertified custom visuals that are imported from files using the developer tools in Power BI Desktop. <br/> **Technical Context**: Enabling this setting allows developers to create and test custom visuals using the Power BI SDK, which can be useful for developing tailored visualizations that meet specific business needs. However, uncertified visuals may not have undergone rigorous testing for security and performance, so they should be used with caution. |
| **Add and use certified visuals only (block uncertified)** | This setting allows you to add only certified custom visuals from AppSource and prevents adding uncertified custom visuals from files or the organizational store. <br/> **Technical Context**: Certified visuals have been vetted for quality, security, and performance, ensuring they meet Microsoft's standards. Blocking uncertified visuals helps maintain a secure and stable environment by preventing the use of potentially untested or insecure visuals. |
| **Allow downloads from custom visuals** | Enabling this setting will enable visualizations that allow exporting information available in the visual for further analysis. Disabling this setting will prevent users from downloading data from any visualizations. <br/> **Technical Context**: Allowing downloads from custom visuals can facilitate deeper analysis by enabling users to export data for use in other tools or reports. However, it also poses a risk of data leakage, so organizations should carefully consider the implications of enabling this feature. |
| **AppSource Custom Visuals SSO** | This feature enables single sign-on (SSO) capabilities for AppSource custom visuals. When enabled, users can authenticate once and access multiple applications without needing separate logins for each one. <br/> **Technical Context**: Enabling SSO for custom visuals enhances user convenience and security by reducing the number of login credentials users need to manage. It also helps ensure that access to visuals is consistent with the organization's authentication policies. |
| **Allow access to the browser's local storage** | This feature allows certain custom visuals to store information on the user's browser's local storage. <br/> **Technical Context**: Allowing access to the browser's local storage can improve the performance and functionality of custom visuals by enabling them to store and retrieve data locally. However, it also raises security and privacy concerns, as sensitive data could be stored on the user's device. Organizations should evaluate the risks and benefits before enabling this feature. |

### Copilot and Azure OpenAI Service​

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Enable Copilot in Fabric** | Turn on this setting to allow users to use Copilot features and other features powered by Azure OpenAI. This includes accessing data from OneLake, Data Warehouse, and Real-Time Analytics in Fabric with Copilot in Power BI. <br/> **Technical Context**: Enabling this setting integrates advanced AI capabilities into Microsoft Fabric, enhancing data analysis and visualization through natural language processing and machine learning. Users can interact with data more intuitively using Copilot, which leverages Azure OpenAI to provide intelligent insights and recommendations. <br/> **Data Residency**: Note that data sent to Azure OpenAI may be processed outside your organization's geographic region or national cloud instance, which could have compliance implications depending on your organization's policies. Administrators should consider data residency requirements and potential compliance issues before enabling this setting. <br/> **Management**: This setting can be managed using PowerShell cmdlets or by typing "copilots" into the search box on the related admin center pages. By enabling this setting, you agree to the Preview Terms. |
| **Users can use Copilot features and other features powered by Azure OpenAI** | Users can use Copilot features and other features powered by Azure OpenAI if an administrator enables access, users have been assigned licenses that include Copilot, and users have appropriate security group assignments. <br/> **Technical Context**: Copilot in Microsoft Fabric uses AI to assist users in data exploration, report generation, and analytics. It can understand natural language queries and provide relevant data insights, making it easier for users to interact with complex datasets. <br/> **Azure OpenAI Integration**: Azure OpenAI provides the underlying AI capabilities for Copilot, including natural language processing and machine learning. This integration allows for advanced data analysis and visualization features within Microsoft Fabric. <br/> **Security Group Assignments**: Administrators can control access to Copilot features by assigning appropriate security groups. This ensures that only authorized users can utilize these advanced AI capabilities. |
| **Data Residency and Compliance** | Data sent to Azure OpenAI can be processed outside your organization's geographic region or national cloud instance if required for service availability. <br/> **Technical Context**: Organizations need to be aware of where their data is processed, especially if it involves sensitive or regulated information. Enabling Copilot may result in data being processed outside the organization's geographic region, which could impact compliance with data residency regulations. |

## Embed Codes

This section allows administrators to view embed codes that have been created by their organization. The interface includes options to refresh and export data, and it lists details such as the report name, workspace, publisher, status, and embed URL.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/8d70d3e8-2e05-4c68-9f40-dd7d31cc2a81">

## Custom branding

| **Setting** | **Description and Context** |
|-------------|------------------------------|
| **Logo** | Administrators can upload a logo with a recommended size of 190 x 30 pixels. <br/> **Technical Context**: Uploading a custom logo helps organizations maintain brand consistency across their Power BI environment. The logo appears in the Power BI service, providing a branded experience for users. Ensuring the logo meets the recommended size ensures it displays correctly without distortion. Custom branding features like logos help organizations create a consistent brand experience across all their tools and platforms, enhancing user recognition and trust. |
| **Cover Image** | Administrators can upload a cover image that is at least 1920 x 160 pixels and less than 1 MB in size. <br/> **Technical Context**: The cover image is displayed on the Power BI home page, enhancing the visual appeal and reinforcing the organization's brand identity. Ensuring the image meets the size and file requirements is important for optimal display quality. A high-resolution image that fits within the specified dimensions ensures a professional and polished appearance. Customizing the visual elements of Power BI can improve the user experience by making the interface more engaging and aligned with the organization's identity. |
| **Theme Color** | There is an option to set a theme color using a color picker or by entering a hex code. <br/> **Technical Context**: Setting a theme color allows organizations to align the Power BI interface with their corporate color scheme. This customization helps create a cohesive look and feel, making the Power BI environment more familiar and visually appealing to users. Using the correct hex code ensures that the chosen color is accurately represented in the interface, maintaining visual consistency. Adhering to the recommended sizes and file formats for logos and cover images ensures that these elements are displayed correctly and look professional. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-9-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-16</p>
</div>
<!-- END BADGE -->