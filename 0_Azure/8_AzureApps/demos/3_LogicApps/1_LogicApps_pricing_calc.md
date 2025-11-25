# Azure Logic Apps <br/> Consumption vs Standard plans - Pricing Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)
- [Logic Apps pricing table](https://azure.microsoft.com/en-us/pricing/details/logic-apps/?msockid=38ec3806873362243e122ce086486339)
- [Limits and configuration reference for Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-limits-and-config?tabs=consumption)
- [Usage metering, billing, and pricing for Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-pricing)
- [Run duration and history retention limits](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-limits-and-config?tabs=consumption#run-duration-and-history-retention-limits)
- [Estimate storage costs for Standard logic app workflows in single-tenant Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/estimate-storage-costs)
- [Storage operations](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-pricing#consumption-multitenant) - `Metering applies only to data retention-related storage consumption` such as saving inputs and outputs from your workflow's run history
</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Data Retention](#data-retention)
- [Consumption vs Standard](#consumption-vs-standard)
- [Prices Vary by Region](#prices-vary-by-region)
- [How to calculate it?](#how-to-calculate-it)

</details>

## Data Retention

> [!TIP]
> What is Data Retention in Logic Apps?
> - Logic Apps stores run history, inputs, and outputs for troubleshooting and auditing. By default:
>    - Consumption plan: 90-day retention for run history.
>    - Standard plan: Configurable retention (can be shorter or longer).
>    - Charges apply only when you store data beyond the default retention period or in additional storage.
> - In summary:
>   - Default retention (90 days) is included at no extra cost.
>   - If you:
>      - Extend retention (e.g., 180 days or 1 year).
>      - Export run history to Azure Storage or Log Analytics.
>      - Store diagnostic logs in Application Insights → Then storage charges apply.
> - Recommendations: 
>    - Enable log retention policies and purge old runs to minimize cost
>    - Use Azure Monitor and Application Insights for telemetry instead of storing full run history indefinitely.

| Consumption | Standard | 
| --- | --- |
| <img width="1438" height="898" alt="image" src="https://github.com/user-attachments/assets/b4e4a381-1e15-4322-83e9-6289b0937b74" /> | <img width="1415" height="860" alt="image" src="https://github.com/user-attachments/assets/8f495fed-966c-43f4-9748-d6bf8e95f43f" /> | 

## Consumption vs Standard

> [!TIP]
> - Consumption = `cheaper for small workloads, but cost grows with volume.`
> - Standard = `predictable pricing, ideal for large-scale integrations like yours.`

| Feature                 | **Consumption Plan**                                                                                                                                          | **Standard Plan**                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Billing Basis**       | Pay-as-you-go per **trigger**, **action**, and **connector call**                                                                                             | Fixed monthly cost based on **compute resources**                                                                                    |
| **Cost Predictability** | Variable, scales with usage                                                                                                                                  | Predictable, flat rate per App Service plan                                                                                         |
| **Integration Account** | Same pricing for Integration Account                                                                                                                    | Same pricing for Integration Account                                                                                                 |
| **Performance**         | Multi-tenant, scales automatically                                                                                                                            | Dedicated compute, better performance for heavy loads                                                                                |
| **Best For**            | Low/medium volume or sporadic workflows                                                                                                                       | High-volume, continuous integrations                                                                                                 |
| **Your Example Cost**   | \~$269/month for 4M actions<br>($1,200+ if 48M actions)                                                                                                       | $364/month fixed (WS2) regardless of executions                                                                                      |
| **Features**            | - No local dev<br>- Limited VNET integration                                                                                                                  | - Local dev support<br>- Containerized runtime<br>- VNET integration                                                                 |


https://github.com/user-attachments/assets/74d91084-d4ba-4de8-91a8-b168de4dec6a

## Prices Vary by Region

> Azure pricing is not globally uniform. It differs by region due to several factors:

1.  **Infrastructure Costs**
    *   Data centers in different regions have varying operational costs (power, cooling, real estate).
    *   Regions with higher energy or facility costs tend to have slightly higher service prices.
2.  **Local Taxes & Compliance**
    *   Some regions include additional taxes, VAT, or compliance-related surcharges.
    *   Regulatory requirements (e.g. GDPR in EU) can increase operational overhead.
3.  **Currency Exchange Rates**
    *   Prices are adjusted based on local currency fluctuations against USD.
    *   Azure updates regional pricing periodically to reflect exchange rate changes.
4.  **Demand & Capacity**
    *   Regions with high demand or limited capacity may have premium pricing.
    *   Conversely, newer regions or those with excess capacity may offer lower rates.

E.g Consumption: `Per-action and connector call rates can differ slightly by region.`

| North Central US | Australia Southeast | 
| --- | --- | 
| <img width="790" height="913" alt="image" src="https://github.com/user-attachments/assets/c31c1c5d-9187-44c3-b0c2-f26c972929a8" /> | <img width="787" height="921" alt="image" src="https://github.com/user-attachments/assets/659bf154-d581-4923-8ee3-61863e5939f1" /> | 

E.g Standard: `App Service Premium or Workflow Service Plan pricing varies by region.`

| North Central US | Australia Southeast | 
| --- | --- | 
| <img width="817" height="899" alt="image" src="https://github.com/user-attachments/assets/8c2550af-844a-4fbd-a9e4-981faa593c99" /> | <img width="793" height="882" alt="image" src="https://github.com/user-attachments/assets/6cebebab-e128-4bbd-b478-f06e517f0e0c" /> | 

## How to calculate it?

> If Consumption

1. Identify Key Inputs

*   **Avg Messages per Month** 
*   **Estimated actions per message** (e.g. 50)
*   **Estimated standard connector calls per message** (e.g. 30)
*   Pricing:
    *   Actions: $0.000025 per execution
    *   Standard connector: $0.000125 per call

2. Calculate Actions per Month

~~~
    Actions per Month = Avg Messages per Month × Estimated actions per message
~~~

3. Calculate Connector Calls per Month

~~~
    Connector Calls per Month = Avg Messages per Month × Estimated standard calls per message
~~~

4. Calculate Cost of Actions

~~~
    Cost of actions = Actions per Month × $0.000025
~~~

5. Calculate Cost of Connector

~~~
    Cost of connector = Connector Calls per Month × $0.000125
~~~

6. Calculate Total Cost

~~~
    Total cost = Cost of actions + Cost of connector
~~~

> If Standard Plan:

*   No per-action cost.
*   Use fixed monthly instance cost (e.g. WS2 = $364/month).
*   Either:
    *   Put plan price in **Total cost** for all integrations combined.
    *   Or distribute proportionally by message volume.


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
