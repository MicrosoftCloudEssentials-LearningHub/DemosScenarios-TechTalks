#  Microsoft Fabric Community Conference (Las Vegas 2025) - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-07

----------

>  `Las Vegas from March 31 to April 2`. Showcased significant advancements and innovations across different domains of the Fabric platform.


<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Announcements from the Microsoft Fabric Community Conference](https://www.microsoft.com/en-us/microsoft-fabric/blog/2024/03/26/announcements-from-the-microsoft-fabric-community-conference/?msockid=38ec3806873362243e122ce086486339)
- [FabCon 2025: Fueling tomorrow’s AI with new agentic capabilities and security innovations in Fabric](https://www.microsoft.com/en-us/microsoft-fabric/blog/2025/03/31/fabcon-2025-fueling-tomorrows-ai-with-new-agentic-capabilities-and-security-innovations-in-fabric/)
- [OneLake security overview](https://learn.microsoft.com/en-us/fabric/onelake/security/get-started-security)
- [Best practices for OneLake security](https://learn.microsoft.com/en-us/fabric/onelake/security/best-practices-secure-data-in-onelake)

</details>

## Overview

| **Category**                | **Details**                                                                                                                                                                                                                                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Platform Enhancements**   | - **OneLake Security (Private Preview)**: Seamless security integration across Spark, SQL Endpoint, and Power BI in Direct Lake mode.<br/> - **Command Line Interface (CLI)**: Execute commands across Fabric using terminal prompts or pre-written scripts.<br/> - **Variable Library**: Efficiently manage variables at a workspace level. |
| **Data Integration**        | **Database Mirroring**: Supports sources behind firewalls such as Azure SQL Database and Snowflake, with Azure SQL MI coming soon. On-prem SQL Server, Oracle, and Dataverse support is also on the way.|
| **Data Engineering & Data Science** | - **Fabric Data Agents (Former AI Skills)**: Integrate Data Agents with Azure AI Foundry.<br/> - **Copilot & AI Features**: Available with all paid-SKU, starting with F2.<br/> - **Autoscale Billing for Spark**: Serverless, pay-as-you-go billing, no longer consuming your Fabric capacity when enabled.<br/> - **Copilot Improvements**: Copilot is now pre-installed, supports data-specific queries, and tracks historic interactions.<br/> - **AI Functions**: Apply LLM models for summarization, text generation, classification, sentiment analysis, and translation.<br/> - **Row-Level & Column-Level Security in Spark**. |
| **Data Warehouse**          | - **AI Functions**: Bring AI features to Data Warehouse, similar to Data Engineering & Data Science.<br/> - **User-Defined Functions (UDFs)**: Write custom Python functions and execute them directly through T-SQL.<br/> - **Migration Tool**: Public preview for migrating Azure Synapse Analytics warehouses to Fabric.                  |
| **Real-Time Intelligence**  | **Streaming & Event Connectors**: New integrations for MQTT, Solace, ADX, Real-Time Weather, and Azure Event Grid.|
| **Power BI**                | - **Direct Lake Semantic Models**: Create models directly in Power BI Desktop, and use data from multiple OneLake sources.<br/> - **Datapoint Annotations**: Add descriptive text to specific data points directly in PowerPoint presentations.<br/> - **Copilot Improvements**: Ask data questions from your model.<br/> - **Notebook Tools**: Quickly analyze semantic models with pre-built notebooks for best practices and memory optimization. |
| **Additional Highlights**   | - **Workshops and Sessions**: Over 200 expert-led sessions covering AI, databases, analytics, business intelligence, and more.<br/> - **Hands-On Workshops**: Pre- and post-conference workshops offering immersive, practical learning experiences.<br/> - **Keynote and Corenote Sessions**: Insights into the latest developments and roadmaps for Microsoft Fabric.<br/> - **Networking Opportunities**: Dedicated networking spaces like Ask the Experts and the Community Lounge. |

## Platform Enhancements

> Setting Up OneLake Security:

1. **Define Security Roles**: Create roles within OneLake to manage access to data tables or folders. These roles can include Admin, Member, Contributor, and Viewer, each with different levels of access.
2. **Assign Permissions**: Assign permissions at the workspace level to control access to all items within that workspace. Use the sharing feature to grant users direct access to specific items if they do not need access to the entire workspace
3. **Configure Item Permissions**: Use the Manage Permissions page to add or remove individual item permissions for users or groups. This allows for fine-grained control over who can access specific data items.
4. **Set Up Compute Permissions**:  Grant data access through the SQL compute engine by restricting access to specific tables and schemas. Implement row and column-level security to further refine access controls.
5. **Implement User Identity Mode**: Enable user identity mode for SQL Analytics Endpoints to ensure that security policies are enforced based on user roles and permissions

> Best Practices:

1. **Least Privilege Access**: Assign permissions at the appropriate level to ensure that users only have access to the data necessary for their tasks. Avoid over-provisioning to reduce security risks.
2. **Secure by Workload**: Grant users access to specific data workloads through item permissions, compute permissions, and OneLake data access roles. Configure access to the least privileged level required for the user's job.
3. **Use Data Access Roles**: Use OneLake data access roles to control access to folders and tables within a lakehouse. This allows for selective access to specific items in a lakehouse.
4. **Monitor and Audit Access**: Regularly review and audit access permissions to ensure compliance with security policies. Adjust permissions as needed to maintain a secure environment.

### OneLake Security (Private Preview)

> Here are the key aspects:

- **Granular Security Definitions**: OneLake Security enables defining `row and column-level` security directly within OneLake, ensuring consistent security rules across different Fabric engines.
- **Unified Security Management**: With OneLake Security, `roles can be created to grant access to specific data tables or folders`. These roles can further restrict access using row or column-level security.
- **Automatic Enforcement**: `Security roles` defined in OneLake `are automatically enforced when querying through Spark notebooks, SQL Analytics Endpoints, and Power BI in Direct Lake mode`.
- **User Identity Mode**: SQL Analytics Endpoints now support a `user identity` mode, ensuring that OneLake Security is the source of truth for all access through SQL endpoints. This `mode means` that `SQL Analytics Endpoints` can now operate based on individual user identities. This means that access and permissions `are managed at the user level rather than at a broader level (like application or service level)`.
- **Early Access**:  Customers can [sign up for early access](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_BIbobSVbtGoFFUDM3gfGJUNlBWWVpMNDU5NzY5U1NBQVFHOUJPNE5CNS4u) to provide feedback and experience these capabilities before the broad public preview

### Command Line Interface (CLI)

> The Microsoft Fabric Command Line Interface (CLI), also known as `fabric-cli` or `fab`, provides a powerful tool for executing commands across the Fabric platform using terminal prompts or pre-written scripts. Key features include:

- **Installation and Authentication**: The CLI can be installed using `pip` and supports different `authentication methods, including interactive, service principal, and managed identity authentication`.
- **Command Execution**: Users can execute a wide range of commands to manage Fabric resources, deploy applications, and automate workflows.
- **Interactive Mode**: The CLI supports an interactive mode, allowing users to execute commands in a more user-friendly environment.
- **Integration with CI/CD**: Fabric CLI can be integrated with `Azure DevOps pipelines and GitHub Actions for automated deployments and robust CI/CD pipelines`.

### Variable Library

> Allows users to define and manage variables at the workspace level. This feature enhances efficiency and consistency across various workspace items.

- **Workspace-Level Management**: `Variables can be defined and managed at the workspace level`, making them accessible `across different workspace items such as data pipelines, notebooks, and lakehouse shortcuts`.
- **Enhanced Data Pipelines**: The Variable Library is `already available for use in data pipelines, allowing for more streamlined and efficient data processing`.
- **Future Integrations**: Plans are in place to `expand the use of the Variable Library to other areas within the Fabric platform, further enhancing its utility`.



<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
