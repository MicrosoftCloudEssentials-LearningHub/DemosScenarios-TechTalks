# Azure Open AI: Model Availability - Quick Overview 

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Azure OpenAI deployment types](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/deployment-types)
- [What is provisioned throughput?](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/provisioned-throughput?tabs=global-ptum)
- [Azure OpenAI provisioned Managed offering updates](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/provisioned-migration)
- [Provisioned throughput units onboarding](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/provisioned-throughput-onboarding)
- [Azure OpenAI Service pricing](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/)

</details>

## Content

- [Deployment Options](#deployment-options)
- [Pricing models](#pricing-models)
- [When Azure OpenAI Model Availability PTU is Not Available](#when-azure-openai-model-availability-ptu-is-not-available)
    - [Complete a Capacity Request](#complete-a-capacity-request)
    - [Use a Different Model](#use-a-different-model)
    - [Use a Different Region/Zones or Global](#use-a-different-regionzones-or-global)
    - [Attempt Deployment at a Different Time](#attempt-deployment-at-a-different-time)
    - [Azure Reserved Instances](#azure-reserved-instances)

## Deployment Options

| **Deployment Option** | **Description** | **Pros** | **Cons** | **Technical Notes** |
|-----------------------|-----------------|----------|----------|---------------------|
| **Data Zones**        | Data Zones allow customers to process and store their data within specific geographic boundaries, ensuring compliance with regional data residency requirements while maintaining optimal performance. | Ensures data residency compliance, optimized for regional performance. | Limited availability compared to global options. | Suitable for applications with strict data residency requirements. May require configuration of virtual networks and subnets. |
| **Global Standard**   | Global Standard deployments leverage Azure's global infrastructure to dynamically route customer traffic to the data center with the best availability for the customer’s inference requests. | Highest initial throughput limits, best model availability, low latency. | Potential latency variation for high volume workloads. | Ideal for applications needing high availability and low latency. Uses Azure's global load balancing and routing capabilities. |
| **Provisioned Throughput Units (PTUs)** | PTUs provide guaranteed throughput by allocating specific processing capacity for your deployment. This ensures stable performance and predictable latency. | Predictable performance, allocated processing capacity, potential cost savings for high throughput workloads. | Requires accurate forecasting of capacity needs, may involve higher upfront costs. | Best for applications with consistent and high throughput requirements. Requires careful planning and capacity management. |

## Pricing models

> [!NOTE]
> How Provisioned Throughput Units (PTUs) are charged in Azure OpenAI Service:
1. **Hourly Rate**: PTUs are charged based on the number of PTUs deployed and the duration of the deployment. For example, if you deploy 100 PTUs, you will be charged the hourly rate for 100 PTUs.
2. **Partial Hour Deployment**: If a deployment exists for only part of an hour, the charge is prorated based on the number of minutes the deployment was active. For instance, if a 100 PTU deployment exists for 15 minutes, it will be charged as a 25 PTU deployment for that hour.
3. **Predictable Costs**: PTUs provide predictable costs for applications with consistent usage patterns. This is beneficial for budgeting and cost management, especially for production environments with stable traffic.

> This prorated charging ensures you only pay for the actual usage, making it cost-effective for varying workloads. For example:
- **Full Hour Deployment**: Deploying 50 PTUs for a full hour will incur a charge for 50 PTUs for that hour.
- **Mid-Hour Deployment**: Deploying 50 PTUs for 30 minutes will incur a charge for 25 PTUs for that hour.

| **Pricing Model**                | **Description**                                                                 | **Ideal For**                          | **Billing**|
|----------------------------------|---------------------------------------------------------------------------------|----------------------------------------|-----------------------------------------------------------------------------|
| **Standard (On-Demand)**         | Charges based on the number of input and output tokens used.                     | Applications with variable or unpredictable usage. | Pay-as-you-go.|
| **Provisioned Throughput Units (PTUs)** | Allocates specific throughput capacity for predictable costs.                   | Applications with predictable and consistent usage. | Monthly or annual basis, often at a discounted rate compared to on-demand. |

## When Azure OpenAI Model Availability PTU is Not Available

<img width="550" alt="image" src="https://github.com/user-attachments/assets/f1da9940-a809-4902-95ba-f524e490edbe" />

### Complete a Capacity Request
> Submit a request to Azure for additional capacity.
- **Pros**: Tailored to your specific needs.
- **Cons**: May take time to process and approve.
> Steps:
  1. **Sign in to Azure Portal**: Use your Azure subscription credentials.
  2. **Navigate to `Quotas`**: Enter `quotas` in the search box and select `Quotas`
  3. **Request Increase**: Click `Request Quota`.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/b6cc365a-6a54-407e-850b-79b932d09e5d" />

  4. **Submit Details**: Fill the [Azure OpenAI Service: Request for Quota Increase](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR4xPXO648sJKt4GoXAed-0pUMFE1Rk9CU084RjA0TUlVSUlMWEQzVkJDNCQlQCN0PWcu)

### Use a Different Model
> Switch to an alternative model that is available in the desired region. Use the [Azure AI Foundry Model Catalog](https://ai.azure.com/explore/models) to discover and evaluate a wide range of models from various providers.

- **Pros**: Immediate availability, potentially lower costs.
- **Cons**: May require adjustments to your application to accommodate the new model.
> Steps:
  1. **Identify Alternative Models**: Check the Azure OpenAI Service models available in your region.
  2. **Evaluate Compatibility**: Assess the performance and compatibility of the alternative model with your application.
  3. **Update Application**: Make necessary adjustments to your application to integrate the new model.

https://github.com/user-attachments/assets/5b10270d-b5fe-40f7-9af2-df2cdc77658b

### Use a Different Region/Zones or Global

> Deploy the model in a different region or use Azure's global infrastructure to dynamically route traffic to the best available data center.
- **Pros**: Increased availability, potential cost savings.
- **Cons**: Possible latency issues, data residency concerns.

> Steps:
  1. **Select Region**: Choose a different region or data zone for deployment.
  2. **Configure Deployment**: Set up the deployment in the new region using Azure's global load balancing features.
  3. **Monitor Performance**: Track latency and performance to ensure it meets your application's requirements.

https://github.com/user-attachments/assets/341dfc6a-a996-40a5-9f73-96adafe2f92b

### Attempt Deployment at a Different Time
> Capacity availability can change dynamically, so trying at a different time might help.
- **Pros**: Simple to try.
- **Cons**: No guarantee of success.
> Steps:
  1. **Monitor Capacity Status**: Keep an eye on Azure's capacity status and availability.
  2. **Plan Off-Peak Deployments**: Schedule deployments during off-peak hours when capacity is more likely to be available.
  3. **Retry Deployment**: Attempt the deployment again at a different time if initial attempts fail.

### Azure Reserved Instances

> Reserved Instances allow you to reserve capacity in advance, ensuring availability and potentially reducing costs. This is essentially a commitment to use a certain amount of PTUs over a specified period.

> [!NOTE]
> Azure OpenAI `Reservations are agreements` for a specific time period and compute capacity. Whether using the Pay-as-you-go model or reservations, you need to create the Azure OpenAI Capacity within a resource group. <br/><br/>
> Reservations in Azure, including Azure OpenAI `reservations`, are `managed at the subscription level`. This means that the reserved capacity units (PTUs) apply to the entire subscription, not to individual resource groups. <br/>
> - `Reservations`: Provide a `subscription-wide discount` for committing to a certain amount of capacity over a period of time. <br/>
> - `Capacity Creation`: You create and manage Azure OpenAI `capacities within specific resource groups`, but the `cost benefits from the reservation apply at the subscription level`.

- **Pros**: Guaranteed capacity, potential cost savings, predictable performance.
- **Cons**: Requires upfront commitment, less flexibility.

> Steps:
  1. **Evaluate Needs**: Assess your long-term capacity requirements.
  2. **Purchase Reserved Instances**:
     - Sign in to the Azure portal.
     - Navigate to `Cost Management + Billing` and select `Reservations + Hybrid Benefit`.
     - Click on `Add` and choose `Azure OpenAI Service`.
     - Select the region, quantity, and deployment type (Global, Data Zone, or Regional).
     - Add the Azure OpenAI Service SKU to your cart.
     - Verify the quantity of PTUs you want to purchase and complete your order.
  3. **Configure Deployment**: Set up your deployment using the reserved instances.
  4. **Monitor Usage**: Track usage to ensure it aligns with your reserved capacity.

> [!NOTE]
> While managing resources within resource groups, the reservation’s cost benefits are applied across the entire subscription.

| **Aspect** | **Details** |
|------------|-------------|
| **Reservation** | - `Subscription Level Management`: When you make a reservation, it applies to the entire subscription. This means any resource within that subscription can benefit from the reserved capacity.<br/>- `Discounts`: The primary benefit of reservations is the cost savings. By committing to a certain amount of capacity over a period of time, you receive a discount compared to pay-as-you-go pricing.<br/>- `Flexibility`: While the reservation itself is at the subscription level, you can still create and manage individual capacities within different resource groups. The reserved capacity units are utilized by any eligible resources within the subscription. |
| **Capacity** | - `Creating Capacity`: Even though the reservation is at the subscription level, you still need to create the actual Azure OpenAI capacity in the Azure portal. This capacity can be assigned to specific resource groups as needed.<br/>- `Utilizing Reservations`: When you create an Azure OpenAI capacity, it will automatically utilize the reserved capacity units from your subscription, ensuring you benefit from the cost savings. |

> [!NOTE]
> Scope Assignment in Reservations

| **Level**                | **Scope**                                                                                                                                       | **Usage/Management**                                                                                                                                                                                                 |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Subscription Level**   | - Reservations are applied at the subscription level.<br/>- Reserved capacity units (PTUs) provide a discount for any eligible resources within the entire subscription. | Any Azure OpenAI capacity created within this subscription can utilize the reserved PTUs, benefiting from the cost savings. |
| **Resource Group Level** | - Reservations are managed at the subscription level.<br/>- The reserved capacity units are not directly assigned to individual resource groups but are available for any resource within the subscription.  | You can still organize and manage your resources within different resource groups. |

> [!TIP]
> Define the scope of the reservation

| **Scope Option**         | **Description**                                                                                       |
|--------------------------|-------------------------------------------------------------------------------------------------------|
| **Single resource group**| Applies the reservation discount to the matching resources in the selected resource group only.       |
| **Single subscription**  | Applies the reservation discount to the matching resources in the selected subscription.              |
| **Shared**               | Applies the reservation discount to matching resources in eligible subscriptions within the billing context. |
| **Management group**     | Applies the reservation discount to the matching resources in the list of subscriptions that are part of both the management group and billing scope. |

https://github.com/user-attachments/assets/b42e4446-73ef-46fe-b84c-246b2636b391


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
