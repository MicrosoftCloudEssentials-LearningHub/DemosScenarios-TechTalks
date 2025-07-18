# Embedding Power BI Reports

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

> To allow users of a system to access Power BI reports without needing individual Power BI licenses, you can use **Power BI Embedded** or **Power BI Premium**. Find below a guide of the requirements, licensing options, and steps to achieve this integration.

## Wiki 

- [Power BI Embedded Documentation](https://docs.microsoft.com/en-us/power-bi/developer/embedded/embedding)
- [Power BI Premium Documentation](https://docs.microsoft.com/en-us/power-bi/admin/service-premium-what-is)

## Requirements
1. **Power BI Pro or Premium Per User (PPU) License**: Required for creating and publishing reports.
2. **Power BI Workspace**: The reports need to be published in a workspace.
3. **Microsoft Entra Tenant**: Necessary for managing authentication and permissions.
4. **Microsoft Entra App**: Used to generate tokens for embedding reports.
5. **Development Environment**: Tools like Visual Studio or Visual Studio Code for building your integration.

## Licensing Options
- Power BI Embedded
  - **Target Audience**: Independent Software Vendors (ISVs) and developers embedding reports into applications.
  - **Licensing**: Pay for capacity (compute and storage) rather than individual user licenses. This allows any user of your application to access the embedded reports without needing a Power BI license.
- Power BI Premium
  - **Target Audience**: Enterprises needing a comprehensive BI solution.
  - **Licensing**: Similar to Power BI Embedded, you pay for capacity. This can be more cost-effective for large organizations.

## Steps to Embed Reports
1. **Configure Microsoft Entra App and Service Principal**: Set up your app to authenticate and generate tokens.
2. **Generate Embed Tokens**: Use the Power BI REST API to generate tokens that allow access to the reports.
3. **Embed Reports in application**: Use the embed tokens and iframe or API calls to display the reports within your application system.

## Key Points
- **No Individual Licenses Needed**: With Power BI Embedded or Premium, users accessing the reports through application do not need individual Power BI licenses.
- **Secure Access**: Ensure that your application system handles authentication securely to prevent unauthorized access.

## Recommended Trainings 

- [Embed Power BI Analytics](https://learn.microsoft.com/en-us/training/paths/power-bi-embedded/): This learning path teaches you how to embed Power BI content in apps, develop programmatic solutions using the Power BI REST API and the Power BI Client APIs, enforce row-level security (RLS) for embedded content, automate common Power BI setup tasks, configure a development environment, and determine appropriate licensing.
- [Introduction to Power BI Embedded Analytics](https://learn.microsoft.com/en-us/training/modules/power-bi-embedded-intro/): This module covers planning for Power BI embedded analytics, determining the Power BI content types that you can embed, adopting a development methodology to embed Power BI content, preparing Power BI content for embedding, and using no-code embedding techniques.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->