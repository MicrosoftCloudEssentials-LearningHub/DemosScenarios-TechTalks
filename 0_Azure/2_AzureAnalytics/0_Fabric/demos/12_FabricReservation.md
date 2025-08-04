# Fabric Capacity Reservations - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

> Each license level provides different amounts of computational power and features, allowing organizations to choose the one that best fits their needs <br/> <br/>
> `Pay-as-you-go` capacities related with specific Azure `resource groups`. This allows you to manage and allocate resources within your organizational structure more effectively. <br/> 
> `Reservation` capacities are managed at the `subscription level`. This means you can’t directly associate them with individual resource groups. Instead, they apply to the entire subscription, providing a discount for committing to a certain amount of capacity over a period of time.
> Assign the capacity to your workspace

> [!NOTE]
> The total cost of the reservation is distributed over the reservation period. This means you don't have to pay the entire amount upfront; instead, the cost is spread out, making it easier to manage and predict your expenses.

> E.g: By choosing an `F128 reservation` in Microsoft Fabric, if the pay-as-you-go rate is `$23.04 per hour`, with the reservation, you might pay `$13.706 per hour`, saving ~41%.
> `F64 around 11.52/hour, $6.853/hour` ~41% savings. Click [here to see the pricing table](https://azure.microsoft.com/en-us/pricing/details/microsoft-fabric/?msockid=38ec3806873362243e122ce086486339)

<details>
<summary><b>Lis of References</b> (Click to expand)</summary>
  
- [Microsoft Fabric trial capacity](https://learn.microsoft.com/en-us/fabric/get-started/fabric-trial)
- [Buy a Microsoft Fabric subscription](https://learn.microsoft.com/en-us/fabric/enterprise/buy-subscription)
- [Microsoft Fabric pricing table: compute + storage](https://azure.microsoft.com/en-us/pricing/details/microsoft-fabric/)
- [Save costs with Microsoft Fabric Capacity reservations](https://learn.microsoft.com/en-us/azure/cost-management-billing/reservations/fabric-capacity)
- [General availability: Reservations for Microsoft Fabric](https://azure.microsoft.com/en-us/updates/general-availability-fabric-capacity-reservations/)
- [Fabric Capacity Size](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#capacity)
- [Workspace license mode and user capabilities](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#workspace)
- [User license and capabilities](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#per-user-licenses)
- [Microsoft Fabric features by SKU](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Overview](#overview)
- [Reservations & Capacity](#reservations--capacity)
    - [Scope Assignment in Reservations](#scope-assignment-in-reservations)
- [How to make a reservation](#how-to-make-a-reservation)
- [Creating/Linking Fabric Capacity to Your Reservation](#creatinglinking-fabric-capacity-to-your-reservation)
- [Assign Workspace Capacity](#assign-workspace-capacity)
- [How to Change Scope of a Reservation](#how-to-change-scope-of-a-reservation)

</details>

## Overview 

| **Benefit**               | **Description**                                                                                       |
|---------------------------|-------------------------------------------------------------------------------------------------------|
| **Cost Savings**          | - **Discounts**: By committing to a one-year reservation, you can save up to 41% compared to pay-as-you-go prices. <br> - **Predictable Costs**: Reservations provide predictable billing, which helps in budgeting and forecasting. |
| **Operational Efficiency**| - **Consistent Workloads**: Ideal for predictable and steady workloads, ensuring you get the most out of your reserved resources. <br> - **Flexibility**: You can exchange or refund reservations if your needs change, providing operational agility. |
| **Payment Flexibility**   | **Upfront or Monthly Payments**: You can choose to pay for reservations upfront or with monthly payments, without any additional fees. |
| **Enhanced Resource Management** | - **Scope Options**: Apply reservations to specific resource groups, subscriptions, or management groups to optimize resource allocation. <br> - **Automatic Application**: The reservation discount automatically applies to matching resources, simplifying management. |
| **Compliance and Governance** | **Policy Enforcement**: Use Azure Policy to ensure resources comply with organizational standards and regulatory requirements. |

Overall process:

> 1. Make a `reservation`, click to see [how to make a reservation](#how-to-make-a-reservation).
> 2. After making a reservation, you need to create the actual `Fabric capacity` where your workloads will run. Link the capacity to your reservation during this setup. Click to see [how to create and link fabric capacity with reservation](#creatinglinking-fabric-capacity-to-your-reservation).
> 3. Assign the workspace capacity, click [here](#assign-workspace-capacity) to see more.

## Reservations & Capacity

> Microsoft Fabric `Reservations are agreements` for a specific time period and compute capacity. Whether using the Pay-as-you-go model or reservations, you need to create the Microsoft Fabric Capacity within a resource group. <br/> <br/>
> Reservations in Azure, including Microsoft Fabric `reservations`, are `managed at the subscription level`. This means that the reserved capacity units (CUs) apply to the entire subscription, not to individual resource groups. <br/>
> - `Reservations`: Provide a `subscription-wide discount` for committing to a certain amount of capacity over a period of time. <br/>
> - `Capacity Creation`: You create and manage Fabric `capacities within specific resource groups`, but the `cost benefits from the reservation apply at the subscription level`. 

> While manage resources within resource groups, the reservation’s cost benefits are applied across the entire subscription.

| **Aspect** | **Details** |
|------------|-------------|
| **Reservation** | - `Subscription Level Management`: When you make a reservation, it applies to the entire subscription. This means any resource within that subscription can benefit from the reserved capacity.<br/>- `Discounts`: The primary benefit of reservations is the cost savings. By committing to a certain amount of capacity over a period of time, you receive a discount compared to pay-as-you-go pricing.<br/>- `Flexibility`: While the reservation itself is at the subscription level, you can still create and manage individual capacities within different resource groups. The reserved capacity units are utilized by any eligible resources within the subscription. |
| **Capacity** | - `Creating Capacity`: Even though the reservation is at the subscription level, you still need to create the actual Fabric capacity in the Azure portal. This capacity can be assigned to specific resource groups as needed.<br/>- `Utilizing Reservations`: When you create a Fabric capacity, it will automatically utilize the reserved capacity units from your subscription, ensuring you benefit from the cost savings. |

### Scope Assignment in Reservations

| **Level**                | **Scope**                                                                                                                                       | **Usage/Management**                                                                                                                                                                                                 |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Subscription Level**   | - Reservations are applied at the subscription level.<br/>- Reserved capacity units (CUs) provide a discount for any eligible resources within the entire subscription. | Any Fabric capacity created within this subscription can utilize the reserved CUs, benefiting from the cost savings. |
| **Resource Group Level** | - Reservations are managed at the subscription level.<br/>- The reserved capacity units are not directly assigned to individual resource groups but are available for any resource within the subscription.  | You can still organize and manage your resources within different resource groups. |

## How to make a reservation

1. Sign in to the Azure Portal: Go to the Azure portal and sign in with your Microsoft account credentials.
2. Navigate to Reservations: In the left-hand menu, select **All services** and then **Reservations** or use the search bar.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/cd710088-7b71-4323-873d-b849700063ff">

3. Click on `+ Add`, and select **Microsoft Fabric** from the list of available reservations.

   <img width="298" alt="image" src="https://github.com/user-attachments/assets/3455239f-e704-48ea-bc62-1a4a5a6553fb">

4. Choose a Subscription: Select the subscription you want to use for the reservation.
5. Select a Scope: Define the scope of the reservation
    
    | **Scope Option**         | **Description**                                                                                       |
    |--------------------------|-------------------------------------------------------------------------------------------------------|
    | **Single resource group**| Applies the reservation discount to the matching resources in the selected resource group only.       |
    | **Single subscription**  | Applies the reservation discount to the matching resources in the selected subscription.              |
    | **Shared**               | Applies the reservation discount to matching resources in eligible subscriptions within the billing context. |
    | **Management group**     | Applies the reservation discount to the matching resources in the list of subscriptions that are part of both the management group and billing scope. |

6. Choose a Region: Select the Azure region where the reservation will apply. This is important for ensuring that your resources are located in the desired geographical area.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/7f10db21-d922-4437-acbf-e0a6f383091f">

7. Add to Cart: Add the desired quantity of Capacity Units (CUs) to your cart. For example, if you need 64 CUs, add 64 CUs to your cart.
8. Review and Purchase: Review your selections and proceed to purchase. You can choose to pay upfront or with monthly payments.
9. Manage Your Reservation: After purchasing, you can manage your reservation settings, including enabling automatic renewal if desired.

> Additional Considerations
> - **Service Availability**: Ensure that the services you need are available in the selected region.
> - **Pricing**: Check the pricing for your desired region to ensure it fits within your budget.
> - **Latency**: Consider the proximity of the region to your users to reduce latency and improve performance.
> - **Data Residency and Compliance**: Ensure the region complies with any legal or regulatory requirements for your data.
> - **Availability Zones**: Some regions offer availability zones for enhanced resilience and availability.
> - **Paired Regions**: Consider using paired regions for geo-redundant storage and other services that depend on replication.

## Creating/Linking Fabric Capacity to Your Reservation

1. **Make a Reservation**: First, ensure you have made a reservation for the required capacity units (CUs) in the Azure portal. This involves selecting the region, size, and quantity of CUs you need. Click [here to see how](#how-to-make-a-reservation).
2. **Create Fabric Capacity**:
   - Go to the Azure portal and search for **Microsoft Fabric**.
   - Select **Create Fabric Capacity**.
3. **Fill in the Required Details**:
   - **Subscription**: Choose the subscription where you made the reservation.
   - **Resource Group**: Select the resource group for your capacity.
   - **Capacity Name**: Provide a unique name for your capacity.
   - **Region**: Ensure this matches the region of your reservation.
   - **Size**: Select the size based on the reserved CUs.
4. **Link to Reservation**:
   - During the setup, you will see an option to link your capacity to an existing reservation.
   - Select the reservation you made earlier from the list. This ensures that the capacity you are creating will utilize the reserved CUs.
5. **Review and Create**:
   - Click on **Review + create** to finalize the setup.
   - Review your configuration and then click **Create** to provision the capacity.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/9ac40a4f-a9cb-4f56-b591-8ef171d7f50b">

## Assign Workspace Capacity

- **Log In**: Open your web browser and go to the Power BI Admin portal. Log in using your administrator credentials.
- **Navigate to Admin Portal**: Once logged in, click on the gear icon (⚙️) in the top right corner and select `Admin Portal` from the dropdown menu.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/ec0c32dc-17aa-46c5-9912-1f5920d7e0d3">

- **Select Workspace**: Click on the workspace you want to migrate. This will open the workspace settings.
    - **Change Capacity**: In the workspace settings, look for the `Capacity` section. You will see an option to change the capacity assignment.
    - **Select Fabric SKU**: From the dropdown menu, select the new Fabric SKU that you have purchased.
    - **Save Changes**: Click "Save" to apply the changes. The workspace will now be reassigned to the new Fabric SKU.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/3587658e-50b8-484a-b048-07de018a15fe">

## How to Change Scope of a Reservation

> - **Permissions**: Ensure you have the necessary permissions to change the scope. Typically, you need to be an owner or have the reservation purchaser role on the subscription. <br/> 
> - **Impact**: Changing the scope can affect how the reservation discount is applied across your resources, so make sure to review the changes carefully.

1. **Sign in to the Azure Portal**: Go to the Azure portal and sign in with your credentials.
2. **Navigate to Reservations**: In the Azure portal, select `All services` and then `Reservations`.
3. **Select the Reservation**: Find and select the reservation you want to modify.
4. **Change the Scope**:
   - Go to `Settings` and then `Configuration`.
   - Here, you can change the scope of the reservation. You can switch between different scopes such as:
     - **Single Subscription Scope**: Applies the reservation discount to the matching resources in the selected subscription.
     - **Shared Scope**: Applies the reservation discount to matching resources in eligible subscriptions within the billing context.
     - **Management Group Scope**: Applies the reservation discount to the matching resources in the list of subscriptions that are part of the management group.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
