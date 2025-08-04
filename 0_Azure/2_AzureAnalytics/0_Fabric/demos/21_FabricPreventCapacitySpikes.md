# Strategies to Prevent Capacity Spikes - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> When resource usage exceeds capacity limits, throttling and smoothing mechanisms are applied to manage the load. However, if demand is excessively high, performance issues may still occur. `If capacity is exceeded and an error message appears, it is recommended to pausa and start the fabric capacity in the Azure portal`.


> [!IMPORTANT]
> Ensure you have admin rights for the capacity you want to monitor.

> [!NOTE]
> In Microsoft Fabric, `smoothing is automatically applied to help manage and optimize capacity usage by spreading the compute demand over time`. This helps prevent sudden spikes and ensures more consistent performance.
> However, `there is no automatic autoscale feature available. Instead, you can configure the autoscale a P capacity or you can manually adjust your capacity based on your usage patterns and needs`. 

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Evaluate and optimize your Microsoft Fabric capacity](https://learn.microsoft.com/en-us/fabric/enterprise/optimize-capacity)
- [Smoothing and throttling in Fabric Data Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/compute-capacity-smoothing-throttling)
- [Burstable capacity in Fabric Data Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/burstable-capacity)
- [The Fabric throttling policy](https://learn.microsoft.com/en-us/fabric/enterprise/throttling)
- [Scale your capacity](https://learn.microsoft.com/en-us/fabric/enterprise/scale-capacity)
- [Actions you can take to recover from overload situations](https://learn.microsoft.com/en-us/fabric/enterprise/throttling#actions-you-can-take-to-recover-from-overload-situations)
- [Using Autoscale with Power BI Premium](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-auto-scale#enable-autoscale-in-the-power-bi-admin-portal)
- [Configure capacity notifications](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-capacity-notifications)
- [Notifications considerations and limitations](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-capacity-notifications#considerations-and-limitations)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>
    
- [Overview](#overview)
    - [Bursting and Smoothing](#bursting-and-smoothing)
    - [Throttling](#throttling)
- [Actions you can take to recover from overload situations](#actions-you-can-take-to-recover-from-overload-situations)
- [Monitor Usage](#monitor-usage)
- [Steps to Configure Capacity Alerts](#steps-to-configure-capacity-alerts)

</details>

## Overview 

Key mechanisms for resource optimization and system stability, this include Bursting, Smoothing, and Throttling:

- **Bursting and Smoothing**: These mechanisms ensure that CPU-intensive activities are completed quickly and efficiently by `temporarily using additional resources and balancing compute demand over time`.
- **Throttling**: This mechanism manages resource consumption by `controlling the rate of operations, preventing system overload, and maintaining stable performance`.

### Bursting and Smoothing

> Mechanisms designed to handle CPU-intensive activities efficiently without the need for a higher SKU.


| **Feature** | **Definition** | **Mechanism** | **Benefits** |
|-------------|----------------|---------------|--------------|
| **Bursting** | Bursting allows temporary use of additional compute resources beyond the provisioned capacity to handle short-term spikes in demand. | When a CPU-intensive task is initiated, the system temporarily allocates extra compute resources to ensure the task completes quickly. This is particularly useful for operations that require high CPU usage for a short duration. | This approach prevents the need to permanently upgrade to a higher SKU, which would incur additional costs. It ensures that tasks are completed efficiently without impacting the overall performance of the system. |
| **Smoothing** | Smoothing balances the compute demand over a specified period to prevent sudden spikes and ensure consistent performance. | For interactive operations, smoothing typically occurs over a minimum of 5 minutes, while for background operations, it spreads over 24 hours. This means that the compute usage is averaged over these periods, reducing the impact of short-term spikes. | Smoothing helps maintain a steady performance level by distributing the compute load evenly. It ensures that the system can handle varying workloads without experiencing significant performance degradation. |


### Throttling

> Mechanism used to manage resource consumption by delaying or rejecting operations when the capacity experiences sustained high demand. 


| **Aspect**             | **Details**                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| **Definition**         | Throttling controls the rate at which operations are processed to prevent overloading the system. It is automatically applied when the demand for CPU resources exceeds the capacity limits. |
| **Mechanism**          | When the system detects sustained high CPU usage above the SKU limit, it starts to throttle operations. This can involve delaying requests, reducing the rate of processing, or temporarily rejecting some operations to manage the load. |
| **Types of Throttling**| - **Interactive Operations**: User-initiated actions, such as running reports or dashboards, can be throttled if they exceed capacity limits. <br> - **Background Operations**: Automated processes like data refreshes can also be subject to throttling to manage resource usage. |
| **Benefits**           | Throttling helps maintain system stability and performance by ensuring that resources are not overused. It prevents the system from becoming overwhelmed and ensures that critical operations can still be performed. |
| **Technical Information** | - **Automatic Application**: Throttling is automatically applied by the system based on predefined thresholds and policies. <br> - **Thresholds**: Specific thresholds are set for CPU usage, and when these are exceeded, throttling mechanisms are triggered. <br> - **Impact on Operations**: Throttling can lead to delays in processing, reduced processing rates, or temporary rejection of operations. <br> - **Monitoring**: Administrators can monitor throttling events using tools like the Microsoft Fabric Capacity Metrics app to understand when and why throttling occurs. <br> - **Configuration**: While throttling is automatic, administrators can configure certain policies and thresholds to better manage how and when throttling is applied. |



## Actions you can take to recover from overload situations

> `When your capacity is throttled to the point it's frozen`, users receive an error if their action requires Fabric compute resources. For example, `the error can say Cannot load model due to reaching capacity limits`. In such cases, you can use these strategies to recover your capacity from its frozen state.

- Wait until the overload state is over before issuing new requests.
- Upgrade the SKU of an F capacity.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/1a8b4ade-5bd8-4a19-8c3a-7488bdab4512">

- Pause/resume an F capacity.

    | Pause | Resume |
    | --- | --- |
    | <img width="300" alt="image" src="https://github.com/user-attachments/assets/8085c163-b3bc-446d-a7ae-24a3e5d6ec77"> | <img width="300" alt="image" src="https://github.com/user-attachments/assets/215eb0d0-81a9-40af-96ad-90a1234352a0"> | 

- Move lower priority or overconsuming workspaces out of the capacity.

    > It can be done via `workspace settings`:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/004615e7-1f4c-4ac0-9d04-cda816508d3f">
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/d377dce7-6ecf-4173-8bfb-69663f06faee">
    
    > Or go to `settings`, click on `admin portal`, then under `workspaces`, pick the ones you want to reassign and click on `reassign workspace`:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/02a0f0d7-c86d-4c6e-a3f4-6caf2d3f3a4d">

- [Autoscale](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-auto-scale) a P capacity.

## Monitor Usage 

Below, you will find a quick overview of ways to monitor your usage with tools:

- [Microsoft Fabric Capacity Metrics App](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/20_FabricCapacityMetrics.md#microsoft-fabric-capacity-metrics-app): Powerful tool for administrators to `monitor and manage their capacity usage`. It provides detailed insights into `capacity utilization, throttling, and system events, helping to optimize performance and resource allocation`. By tracking these metrics, admins can make informed decisions to ensure efficient use of resources.
- [Admin Monitoring workspace](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/20_FabricCapacityMetrics.md#admin-monitoring): Centralized hub for `tracking and analyzing usage metrics across the organization`. It includes `pre-built reports and semantic models that provide insights into feature adoption, performance, and compliance`. This workspace helps administrators maintain the health and efficiency of their Fabric environment by offering a comprehensive `view of usage patterns and system events`.
- [Monitor Hub](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/20_FabricCapacityMetrics.md#monitor-hub): Allows users to `view and track the status of activities across all workspaces they have permissions for`. It provides a detailed overview of operations, `including dataset refreshes, Spark job runs, and other activities`. With features like historical views, customizable displays, and filtering options, the Monitor Hub helps ensure smooth operations and timely interventions when needed.

## Steps to Configure Capacity Alerts

> - **Monitoring**: Regularly monitor your capacity usage to ensure the alerts are functioning as expected. <br/>
> - **Adjustments**: You can adjust the threshold and recipients at any time based on your needs.

  | **Notification Setting** | **Value** |
  |--------------------------|-----------|
  | **Threshold**            | 80%       |
  | **Recipients**           | Capacity admins, Specific contacts |


1. Go to the [Microsoft Fabric service](https://app.fabric.microsoft.com/) and sign in with your admin credentials.
2. **Access the Admin Portal**:
   - Click on the `Settings` gear icon in the top right corner.
   - Select `Admin Portal` from the dropdown menu.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/65b61468-c046-469b-a98b-d8a93cd333b5">

3. **Navigate to Capacity Settings**:
   - In the Admin Portal, go to the `Capacity settings` section.
   - Select the capacity you want to configure notifications for.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/010dfd67-b88f-4c29-b8cd-f1dc6b7ebe75">

4. **Configure Notifications**:
   - Expand the `Notifications` section.
   - In the `Send notifications when` field, set the threshold to `80%`. This will trigger an alert when your capacity usage reaches 80% of the available CUs.
   - You can also configure additional notifications for other thresholds if needed.
5. **Specify Recipients**:
   - In the **Send notifications to** field, select who should receive the notifications:
     - **Capacity admins**: Email notifications will be sent to all admins of this capacity.
     - **These contacts**: Enter the email addresses of specific contacts who should receive the notifications.
6. **Apply Changes**: Click `Apply` to save the notification settings.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/962e9391-8510-4c15-acdb-5e53991c5a40">

Find below an example of the email format:

<img width="700" alt="image" src="https://github.com/user-attachments/assets/308e372d-48de-46f4-9138-984e15b5fd24">

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
