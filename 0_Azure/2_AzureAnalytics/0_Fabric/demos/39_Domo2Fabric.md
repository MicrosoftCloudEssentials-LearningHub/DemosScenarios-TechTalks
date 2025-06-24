# From Domo to Microsoft Fabric - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-06-24

------------------------------------------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Microsoft Fabric documentation](https://learn.microsoft.com/en-us/fabric/)
- [Domo Official Site](https://www.domo.com/)
- [Dataflows in Microsoft Fabric](https://learn.microsoft.com/en-us/power-bi/transform-model/dataflows/dataflows-introduction-self-service)
- [Time intelligence functions (DAX)](https://learn.microsoft.com/en-us/dax/time-intelligence-functions-dax)
- [Star schema guidance](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
- [Conditional formatting in Power BI](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-conditional-table-formatting)
- [Optimization guide for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/power-bi-optimization)
- [Power BI sharing and collaboration](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-share-dashboards)

</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Overview](#overview)
- [Migration Considerations](#migration-considerations)
- [Lifecycle Comparison](#lifecycle-comparison)
- [Data Ingestion](#data-ingestion)
    - [Essentials for Developers](#essentials-for-developers)
    - [Data Connection Types](#data-connection-types)
- [Data Transformation](#data-transformation)
- [Data Modelling](#data-modelling)
- [How to create visualizations](#how-to-create-visualizations)
    - [Recreate Simple Visuals](#recreate-simple-visuals)
    - [Custom Visuals](#custom-visuals)
    - [Bookmarks and Interactivity](#bookmarks-and-interactivity)
- [Optimization](#optimization)
- [Sharing Platform](#sharing-platform)
- [Admin](#admin)
- [Governance](#governance)
- [Migration Approach](#migration-approach)
    - [How to migrate a report](#how-to-migrate-a-report)
    - [Migrate End Users](#migrate-end-users)
</details>

## Overview

```mermaid
graph TD
    A[Data Analytics and Visualization Tools] --> B[Domo]
    A --> C[Microsoft Fabric]
    B --> D[Cards & Dashboards]
    B --> E[Dataflows]
    B --> F[Connectors]
    B --> G[Beast Modes]
    B --> H[Appstore]
    C --> I[Unified Platform]
    C --> J[Power BI Integration]
    C --> K[Data Factory, Synapse, AI]
    C --> L[Role-based Experiences]
```

<details>
<summary><b>Data Visualization</b> – Click to expand</summary>

> Domo uses cards, dashboards, and stories for visualizations. Microsoft Fabric leverages Power BI for advanced, interactive, and customizable visuals.

- **Benefits:** Power BI supports rich interactivity, custom visuals, and AI-driven insights.<br/>
- **Differentiators:** Power BI integrates with DAX, Copilot, and supports embedding in apps and portals.<br/>
- **Use Cases:** Executive dashboards, operational reporting, embedded analytics.<br/>
- **Related Tools:** Power BI Desktop, Power BI Service, Visuals Marketplace.<br/>

</details>

<details>
<summary><b>Dashboards</b> – Click to expand</summary>

> Domo provides a drag-and-drop dashboard builder. Fabric offers a unified reporting and dashboard experience through Power BI.

- **Benefits:** Power BI dashboards aggregate visuals from multiple reports and datasets.<br/>
- **Differentiators:** Supports live tiles, cross-report pinning, and integration with Teams and SharePoint.<br/>
- **Use Cases:** Real-time monitoring, cross-functional reporting, executive summaries.<br/>
- **Related Tools:** Power BI Apps, Power BI Service, Microsoft Teams.<br/>

</details>

<details>
<summary><b>Data Connectivity</b> – Click to expand</summary>

> Domo supports 1000+ connectors and Workbench. Fabric uses Azure Data Factory, Synapse, and Power Query for scalable, enterprise-grade connectivity.

- **Benefits:** Enables hybrid data access, real-time ingestion, and lakehouse integration.<br/>
- **Differentiators:** Native support for Direct Lake, Delta Lake, and Parquet formats.<br/>
- **Use Cases:** ETL/ELT pipelines, streaming data, hybrid cloud access.<br/>
- **Related Tools:** Azure Data Factory, Power Query, Synapse Pipelines, OneLake.<br/>

</details>

<details>
<summary><b>Ease of Use</b> – Click to expand</summary>

> Domo emphasizes ease with Magic ETL and Appstore. Fabric offers a SaaS model with low-code/no-code experiences via Power Query.

- **Benefits:** Power Query provides a familiar, Excel-like interface for data transformation.<br/>
- **Differentiators:** Unified UX across roles, reusable queries, and parameterization.<br/>
- **Use Cases:** Self-service data prep, rapid prototyping, business user reporting.<br/>
- **Related Tools:** Power Query Editor, Dataflows, Power BI Desktop.<br/>

</details>

<details>
<summary><b>Advanced Analytics</b> – Click to expand</summary>

> Domo includes Beast Modes and AI/ML apps. Fabric integrates built-in AI, DAX, Python/R, and Copilot for advanced analytics.

- **Benefits:** Supports predictive modeling, natural language queries, and embedded AI insights.<br/>
- **Differentiators:** Copilot enables natural language report creation and data exploration.<br/>
- **Use Cases:** Forecasting, anomaly detection, NLP-driven insights, data science collaboration.<br/>
- **Related Tools:** Power BI Copilot, Azure ML, Python/R scripts, DAX Studio.<br/>

</details>

<details>
<summary><b>Unified Platform</b> – Click to expand</summary>

> Domo focuses on business intelligence and apps. Fabric delivers end-to-end analytics from ingestion to visualization in a single platform.

- **Benefits:** Reduces tool sprawl and improves governance and collaboration.<br/>
- **Differentiators:** Combines Power BI, Synapse, Data Factory, and OneLake in one SaaS experience.<br/>
- **Use Cases:** Enterprise data platforms, centralized analytics, cross-functional workflows.<br/>
- **Related Tools:** Microsoft Fabric, OneLake, Synapse Data Warehouse, Data Factory.<br/>

</details>

<details>
<summary><b>Role-Specific Experiences</b> – Click to expand</summary>

> Domo supports business users, analysts, and data scientists. Fabric offers tailored experiences for engineers, scientists, and business users.

- **Benefits:** Each role gets a customized interface and toolset, from no-code to pro-code.<br/>
- **Differentiators:** Fabric provides role-based hubs (e.g., Data Engineering, Data Science, BI) within a single platform.<br/>
- **Use Cases:** Data engineering pipelines, BI reporting, data science notebooks, business dashboards.<br/>
- **Related Tools:** Fabric Experiences (BI, Data Engineering, Data Science), Power BI, Notebooks, Pipelines.<br/>

</details>

| Feature                | Domo                                                                 | Microsoft Fabric                                                                 |
|------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **Data Visualization** | Cards, dashboards, and stories                                       | Power BI for advanced, interactive visualizations                                |
| **Dashboards**         | Drag-and-drop dashboard builder                                      | Unified reporting and dashboard experience                                       |
| **Data Connectivity**  | 1000+ connectors, Domo Workbench                                    | Azure Data Factory, Synapse, Power Query, and more                              |
| **Ease of Use**        | Intuitive UI, Appstore, Magic ETL                                   | SaaS model, low-code/no-code, Power Query                                       |
| **Advanced Analytics** | Beast Modes, Data Science tools, AI/ML apps                         | Built-in AI, DAX, Python/R integration, Copilot                                 |
| **Unified Platform**   | Focused on business intelligence and apps                           | End-to-end analytics: ingestion, transformation, modeling, visualization         |
| **Role-Specific**      | Business users, analysts, IT, data scientists                       | Tailored experiences for engineers, scientists, business users                   |


## Migration Considerations

<details>
<summary><b>Data Ingestion</b> – Click to expand</summary>

> Domo uses connectors, Workbench, and Dataflows for ingestion. Microsoft Fabric supports ingestion via Data Factory, Power Query, Dataflows, and Direct Lake.

- **Benefits:** Fabric enables scalable, hybrid ingestion with support for real-time and batch pipelines.<br/>
- **Differentiators:** Direct Lake allows high-performance access to data in OneLake without import or duplication.<br/>
- **Use Cases:** Streaming data, hybrid cloud ingestion, enterprise ETL/ELT pipelines.<br/>
- **Related Tools:** Azure Data Factory, Power Query, Synapse Pipelines, OneLake.<br/>

</details>

<details>
<summary><b>Data Modelling</b> – Click to expand</summary>

> Domo uses Dataflows, Joins, and Beast Modes. Fabric supports Dataflows, DAX, Star Schema, and Relationships for robust modeling.

- **Benefits:** Fabric promotes reusable, scalable models with semantic layers and time intelligence.<br/>
- **Differentiators:** DAX enables complex calculations, and star schema improves performance and maintainability.<br/>
- **Use Cases:** Enterprise semantic models, KPI dashboards, time-based analytics.<br/>
- **Related Tools:** Power BI Desktop, DAX Studio, Dataflows, Tabular Editor.<br/>

</details>

<details>
<summary><b>Visualizations</b> – Click to expand</summary>

> Domo offers Cards, Stories, and Appstore Visuals. Fabric uses Power BI visuals, custom visuals, and themes for rich reporting.

- **Benefits:** Power BI supports interactive visuals, drillthrough, bookmarks, and custom themes.<br/>
- **Differentiators:** Power BI Visuals Marketplace allows importing or developing custom visuals.<br/>
- **Use Cases:** Executive dashboards, operational reports, embedded analytics.<br/>
- **Related Tools:** Power BI Desktop, Visuals Marketplace, Report Builder.<br/>

</details>

<details>
<summary><b>Optimization</b> – Click to expand</summary>

> Domo uses DataFusions, Magic ETL, and DataSet Views. Fabric optimizes with query folding, aggregations, and Performance Analyzer.

- **Benefits:** Fabric enables performance tuning at the query and model level.<br/>
- **Differentiators:** Query folding pushes transformations to the source, reducing load times.<br/>
- **Use Cases:** Large datasets, complex models, performance-critical dashboards.<br/>
- **Related Tools:** Performance Analyzer, DAX Studio, Power BI Optimizer.<br/>

</details>

<details>
<summary><b>Lifecycle</b> – Click to expand</summary>

> Domo follows a lifecycle of import, transform, visualize, and share. Fabric extends this with connect, transform, model, visualize, and share.

- **Benefits:** Fabric supports a more modular and governed lifecycle with reusable components.<br/>
- **Differentiators:** Modeling is a distinct phase, enabling semantic consistency and reuse.<br/>
- **Use Cases:** Enterprise BI workflows, governed self-service analytics.<br/>
- **Related Tools:** Power BI Desktop, Dataflows, Deployment Pipelines.<br/>

</details>

<details>
<summary><b>Sharing & Collaboration</b> – Click to expand</summary>

> Domo uses Groups, Buzz, Appstore, and Publication Groups. Fabric enables collaboration via Workspaces, Apps, Power BI Service, and Teams.

- **Benefits:** Fabric integrates with Microsoft 365 for seamless sharing and collaboration.<br/>
- **Differentiators:** Power BI Apps allow packaging and distributing reports across audiences.<br/>
- **Use Cases:** Cross-team collaboration, secure sharing, embedded analytics.<br/>
- **Related Tools:** Power BI Service, Microsoft Teams, SharePoint, OneDrive.<br/>

</details>

<details>
<summary><b>Licensing</b> – Click to expand</summary>

> Domo offers per user, per instance, and enterprise licensing. Fabric supports per user, Premium, and Fabric Capacity models.

- **Benefits:** Fabric offers flexible scaling with capacity-based pricing for enterprise workloads.<br/>
- **Differentiators:** Fabric Capacity allows shared resources across services like Power BI, Synapse, and Data Factory.<br/>
- **Use Cases:** Small teams to large enterprises, cost-optimized scaling.<br/>
- **Related Tools:** Microsoft 365 Admin Center, Fabric Capacity Metrics App.<br/>

</details>

<details>
<summary><b>Governance & Admin</b> – Click to expand</summary>

> Domo provides Admin Center and Data Governance Toolkit. Fabric includes Admin Portal, Sensitivity Labels, and Compliance tools.

- **Benefits:** Fabric supports enterprise-grade governance with audit logs, data classification, and policy enforcement.<br/>
- **Differentiators:** Integration with Microsoft Purview and Microsoft 365 compliance center.<br/>
- **Use Cases:** Regulated industries, data protection, audit readiness.<br/>
- **Related Tools:** Admin Portal, Microsoft Purview, Power BI Audit Logs.<br/>

</details>

<details>
<summary><b>End Users</b> – Click to expand</summary>

> Domo supports users through Domo University, Community, and Support. Fabric offers Microsoft Learn, Community, and Support resources.

- **Benefits:** Microsoft Learn provides structured, role-based learning paths and certifications.<br/>
- **Differentiators:** Deep integration with Microsoft ecosystem and global community support.<br/>
- **Use Cases:** Onboarding, upskilling, certification, community-driven learning.<br/>
- **Related Tools:** Microsoft Learn, Power BI Community, Fabric Documentation.<br/>

</details>

<details>
<summary><b>Migration Approach</b> – Click to expand</summary>

> Domo migration involves manual rebuilds, Domo API, and export options. Fabric migration also requires manual rebuilds, guided by best practices.

- **Benefits:** Fabric provides structured migration guidance and tooling for rebuilding reports and models.<br/>
- **Differentiators:** Fabric supports Git integration and deployment pipelines for managing migrated content.<br/>
- **Use Cases:** BI modernization, platform consolidation, phased migration strategies.<br/>
- **Related Tools:** Power BI Desktop, Deployment Pipelines, Migration Playbooks.<br/>

</details>

| Category               | Domo Approach | Microsoft Fabric Approach |
|------------------------|---------------|--------------------------|
| **Data Ingestion**     | Connectors, Workbench, Dataflows | Data Factory, Power Query, Dataflows, Direct Lake |
| **Data Modelling**     | Dataflows, Joins, Beast Modes    | Dataflows, DAX, Star Schema, Relationships        |
| **Visualizations**     | Cards, Stories, Appstore Visuals | Power BI visuals, custom visuals, themes          |
| **Optimization**       | DataFusions, Magic ETL, DataSet Views | Query folding, aggregations, Performance Analyzer |
| **Lifecycle**          | Import, transform, visualize, share | Connect, transform, model, visualize, share      |
| **Sharing & Collaboration** | Groups, Buzz, Appstore, Publication Groups | Workspaces, Apps, Power BI Service, Teams        |
| **Licensing**          | Per user, per instance, enterprise | Per user, Premium, Fabric Capacity               |
| **Governance & Admin** | Admin Center, Data Governance Toolkit | Admin Portal, Sensitivity Labels, Compliance     |
| **End Users**          | Domo University, Community, Support | Microsoft Learn, Community, Support              |
| **Migration Approach** | Manual rebuild, Domo API, export options | Manual rebuild, migration guidance, best practices |

## Lifecycle Comparison

<details>
<summary><b>Prepare Stage</b> – Click to expand</summary>

> In Domo, preparation is done using Dataflows and Workbench. In Microsoft Fabric, preparation is handled through Data Factory and Power Query.

- **Benefits:** Fabric supports both low-code (Power Query) and pro-code (Data Factory) for data preparation.<br/>
- **Differentiators:** Fabric enables scalable, reusable pipelines with support for parameterization, scheduling, and monitoring.<br/>
- **Use Cases:** Data cleansing, transformation, ingestion from multiple sources, scheduled refreshes.<br/>
- **Tools (Domo):** Dataflows, Workbench.<br/>
- **Tools (Fabric):** Power Query, Data Factory, Dataflows.<br/>
- **Definition:** Connect to data sources, clean and transform data for modeling and visualization.<br/>

</details>

<details>
<summary><b>Visualize Stage</b> – Click to expand</summary>

> Domo uses Cards and Stories for visualization. Fabric uses Power BI to build interactive reports and dashboards.

- **Benefits:** Power BI supports advanced visuals, interactivity, and AI-driven insights.<br/>
- **Differentiators:** Power BI allows drillthrough, bookmarks, custom visuals, and integration with Copilot for natural language insights.<br/>
- **Use Cases:** KPI dashboards, operational reports, executive summaries, embedded analytics.<br/>
- **Tools (Domo):** Cards, Stories.<br/>
- **Tools (Fabric):** Power BI Desktop, Power BI Service.<br/>
- **Definition:** Build visual representations of data to support decision-making and storytelling.<br/>

</details>

<details>
<summary><b>Share Stage</b> – Click to expand</summary>

> Domo shares content via Buzz, Publication Groups, and links. Fabric uses Workspaces, Apps, and Microsoft Teams for sharing and collaboration.

- **Benefits:** Fabric integrates with Microsoft 365, enabling seamless sharing, collaboration, and governance.<br/>
- **Differentiators:** Power BI Apps allow packaging and distributing content to different audiences with role-based access.<br/>
- **Use Cases:** Cross-team collaboration, secure sharing, enterprise distribution, embedded reporting.<br/>
- **Tools (Domo):** Buzz, Publication Groups.<br/>
- **Tools (Fabric):** Workspaces, Apps, Teams, SharePoint.<br/>
- **Definition:** Distribute reports and dashboards to stakeholders through secure, scalable channels.<br/>

</details>

| Stage                  | Prepare (Domo) | Prepare (Fabric) | Visualize (Domo) | Visualize (Fabric) | Share (Domo) | Share (Fabric) |
|------------------------|----------------|------------------|------------------|--------------------|--------------|----------------|
| **Tool**               | Dataflows, Workbench | Data Factory, Power Query | Cards, Stories | Power BI | Buzz, Publication Groups | Workspaces, Apps, Teams |
| **Definition**         | Connect, clean, transform | Connect, clean, transform | Build cards, dashboards | Build reports, dashboards | Share via groups, links | Share via workspaces, apps |


## Data Ingestion

### Essentials for Developers

<details>
<summary><b>Dataflows</b> – Click to expand</summary>

> Both Domo and Microsoft Fabric support Dataflows for reusable ETL logic and data transformation.

- **Benefits:** Enables modular, reusable data preparation across multiple reports or datasets.<br/>
- **Differentiators:** Fabric Dataflows integrate with Power BI, Excel, and OneLake, and support parameterization and incremental refresh.<br/>
- **Use Cases:** Shared transformation logic, centralized data prep, multi-report consistency.<br/>
- **Related Tools:** Power BI Dataflows, Power Query, OneLake.<br/>

</details>

<details>
<summary><b>Custom Connectors</b> – Click to expand</summary>

> Both platforms support building custom connectors to integrate with non-native or proprietary data sources.

- **Benefits:** Extends platform capabilities to connect with any API or data service.<br/>
- **Differentiators:** Fabric supports custom connectors via Power Query SDK and M language, with Git-based development workflows.<br/>
- **Use Cases:** Connecting to internal APIs, legacy systems, or third-party services.<br/>
- **Related Tools:** Power Query SDK, Visual Studio Code, GitHub.<br/>

</details>

<details>
<summary><b>ETL/ELT</b> – Click to expand</summary>

> Domo uses Magic ETL and SQL for data transformation. Fabric uses Data Factory and Power Query for ETL/ELT processes.

- **Benefits:** Fabric supports both visual and code-based pipelines, with scheduling, monitoring, and parameterization.<br/>
- **Differentiators:** Data Factory enables scalable, enterprise-grade ELT with integration across Azure services.<br/>
- **Use Cases:** Batch processing, data lake ingestion, transformation pipelines.<br/>
- **Related Tools:** Azure Data Factory, Power Query, Synapse Pipelines.<br/>

</details>

<details>
<summary><b>Scripting</b> – Click to expand</summary>

> Domo supports Python/R and Beast Modes. Fabric supports Python/R, DAX, and M for scripting and calculations.

- **Benefits:** Fabric allows advanced analytics, custom calculations, and automation using multiple scripting languages.<br/>
- **Differentiators:** DAX enables powerful, in-memory calculations; M is used for data transformation in Power Query.<br/>
- **Use Cases:** Custom KPIs, statistical modeling, data transformation, automation.<br/>
- **Related Tools:** Power BI Desktop, DAX Studio, Power Query Editor, Notebooks.<br/>

</details>

<details>
<summary><b>Row-Level Security</b> – Click to expand</summary>

> Domo uses PDP (Personalized Data Permissions). Fabric uses Row-Level Security (RLS) to restrict data access.

- **Benefits:** Ensures users only see data relevant to their role or region.<br/>
- **Differentiators:** Fabric RLS integrates with Azure AD and supports dynamic security rules using DAX.<br/>
- **Use Cases:** Multi-tenant reporting, departmental dashboards, compliance-driven access control.<br/>
- **Related Tools:** Power BI Desktop, RLS Roles, Azure AD Groups.<br/>

</details>

<details>
<summary><b>Collaboration</b> – Click to expand</summary>

> Domo uses Buzz and Groups for collaboration. Fabric uses Workspaces and Microsoft Teams for integrated collaboration.

- **Benefits:** Fabric enables real-time collaboration, commenting, and sharing within Microsoft 365 tools.<br/>
- **Differentiators:** Deep integration with Teams, SharePoint, and OneDrive for seamless collaboration.<br/>
- **Use Cases:** Team-based report development, feedback loops, shared workspaces.<br/>
- **Related Tools:** Power BI Workspaces, Microsoft Teams, SharePoint.<br/>

</details>

<details>
<summary><b>AI/ML</b> – Click to expand</summary>

> Domo offers Domo AI and Appstore ML tools. Fabric includes Copilot, AI Insights, and integration with Azure ML.

- **Benefits:** Fabric enables natural language querying, automated insights, and integration with enterprise ML models.<br/>
- **Differentiators:** Copilot in Power BI allows users to generate visuals and insights using natural language.<br/>
- **Use Cases:** Predictive analytics, anomaly detection, AI-assisted reporting.<br/>
- **Related Tools:** Power BI Copilot, Azure Machine Learning, AI Insights, Python/R Notebooks.<br/>

</details>

| Feature                     | Domo | Microsoft Fabric |
|-----------------------------|------|-----------------|
| **Dataflows**               | Yes  | Yes             |
| **Custom Connectors**       | Yes  | Yes             |
| **ETL/ELT**                 | Magic ETL, SQL | Data Factory, Power Query |
| **Scripting**               | Python/R, Beast Modes | Python/R, DAX, M        |
| **Row-Level Security**      | PDP Policies | Row-Level Security (RLS)  |
| **Collaboration**           | Buzz, Groups | Workspaces, Teams         |
| **AI/ML**                   | Domo AI, Appstore | Copilot, AI Insights     |

### Data Connection Types

| Feature         | Domo Import | Domo Federated | Fabric Import | Fabric Direct Lake/Query |
|-----------------|-------------|---------------|---------------|-------------------------|
| **Definition**  | Data imported into Domo | Live query to source | Data imported into Fabric/Power BI | Live query to source or Direct Lake |
| **Performance** | Fast, cached | Depends on source | Fast, cached | Depends on source       |
| **Security**    | PDP (Personalized Data Permissions), Domo security | Source security | RLS (Row-Level Security), Fabric security | Source security         |
| **Offline**     | Yes         | No            | Yes           | No                      |

## Data Transformation

| Feature                | Domo Magic ETL | Power Query Editor (Fabric) |
|------------------------|----------------|----------------------------|
| **Integration**        | Domo platform  | Fabric, Power BI, Excel    |
| **Custom Connectors**  | Yes            | Yes                        |
| **Row/Column Transforms** | Yes         | Yes                        |
| **Parameters**         | Limited        | Yes                        |
| **Scripting**          | Python/R, SQL  | Python/R, M                |
| **Output**             | Datasets, Views| Data model, Excel, Lake    |

## Data Modelling

| **Category**                         | **Comparison**                                                                                                                                      | **Learn More** |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| **Dataflows**                        | `Domo Dataflows are similar to Microsoft Fabric Dataflows, enabling reusable ETL logic.`                                                            | [Fabric Dataflows](https://learn.microsoft.com/en-us/power-bi/transform-model/dataflows/dataflows-introduction-self-service) |
| **Date Tables & Time Intelligence**  | `Domo supports date dimensions; Fabric/Power BI recommends dedicated date tables for time intelligence`                                             | [Time intelligence in DAX](https://learn.microsoft.com/en-us/dax/time-intelligence-functions-dax) |
| **Calculations**                     | `Domo Beast Modes ≈ Power BI Calculated Columns/Measures (DAX)`                                                                                     | [DAX basics in Power BI](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-calculated-columns) |
| **Measures**                         | `Domo Aggregations/Beast Modes ≈ Power BI Measures`                                                                                                 | [Create and use measures in Power BI](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-measures) |
| **Conditionals**                     | `Domo CASE WHEN ≈ DAX IF/SWITCH.`                                                                                                                   | [DAX IF and SWITCH](https://learn.microsoft.com/en-us/dax/if-function-dax) |
| **Star Schemas**                     | `Domo supports joins; Fabric/Power BI recommends star schema for performance.`                                                                      | [Star schema guidance](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema) |

## How to create visualizations

### Recreate Simple Visuals

| Functionality | Domo | Power BI (Fabric) |
|---------------|------|-------------------|
| Card Builder  | Drag-and-drop | Drag-and-drop, Visualizations pane |
| Appstore      | Custom visuals | Power BI Marketplace               |
| Drill Path    | Drill Path     | Drillthrough, Hierarchies          |
| Filters       | Page/Global    | Slicers, Filters                   |

### Custom Visuals

`Domo Appstore ≈ Power BI Visuals Marketplace`

> Click here to read more about [Custom visuals in Power BI](https://learn.microsoft.com/en-us/power-bi/developer/visuals/develop-power-bi-visuals)

### Bookmarks and Interactivity

`Domo Stories ≈ Power BI Bookmarks, Buttons, and Navigation`

> Click here to read more about [Bookmarks in Power BI](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-bookmarks)


## Optimization

- Domo: DataFusions, Magic ETL optimization, DataSet Views.
- Fabric: Query folding, aggregations, Performance Analyzer.

> Click here to read more about [Optimization guide for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/power-bi-optimization)

## Sharing Platform

- Domo: Groups, Buzz, Publication Groups.
- Fabric: Workspaces, Apps, Teams, SharePoint.

> Click here to read more about [Power BI sharing and collaboration](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-share-dashboards)

## Admin

- Domo: Admin Center, Data Governance Toolkit.
- Fabric: Admin Portal, Sensitivity Labels, Compliance.

> Click here to read more about [Power BI governance and administration](https://learn.microsoft.com/en-us/fabric/admin/)

## Governance

- Domo: PDP, Data Governance Toolkit, Certification.
- Fabric: Sensitivity labels, RLS, workspace management, ALM.

> Click here to read more about [Microsoft Fabric governance](https://learn.microsoft.com/en-us/power-bi/guidance/rls-guidance)


## Migration Approach

> There is no automated tool for migrating from Domo to Microsoft Fabric. Migration requires manual rebuilding of data connections, models, and reports.

### Steps

- **Plan migration**: Inventory Domo cards, dashboards, and dataflows. Prioritize by business value.
- **Proof of Concept**: Test key data sources and visuals in Fabric.
- **Phased migration**: Migrate in stages, starting with critical content.
- **Rebuild data connections**: Use Data Factory, Power Query, or direct connectors.
- **Recreate visuals**: Use Power BI Desktop to rebuild cards and dashboards.
- **Publish and share**: Use Fabric workspaces and apps for distribution.
- **Set up security**: Implement RLS and workspace permissions.
- **Train users**: Provide training and support for end users and developers.
- **Iterate and validate**: Test, gather feedback, and refine.

### How to migrate a report

- Reconnect to data sources in Fabric.
- Rebuild dataflows and transformations.
- Recreate cards and dashboards in Power BI.
- Publish to Fabric workspace.
- Set up RLS and permissions.
- Validate and iterate.

### Migrate End Users

- Communicate migration plan and benefits.
- Provide training and documentation.
- Use phased rollout and support channels.
- Leverage Microsoft Learn and community resources.


<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
