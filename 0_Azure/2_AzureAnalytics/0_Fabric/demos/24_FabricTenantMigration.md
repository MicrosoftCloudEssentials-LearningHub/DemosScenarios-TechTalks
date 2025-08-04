# Fabric Tenant Migration - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!NOTE]
> The examples below use regions `like Central US` \& `East US` and `West US` \& `West US 2`, and capacities like P1 and F64 as example. However, `the same logic can be applied to other region combinations`, essentially when dealing with `different regions`.

> [!IMPORTANT]
> Please read [Move between regions](https://learn.microsoft.com/en-us/power-bi/support/service-admin-region-move#can-i-migrate-or-merge-my-power-bi-tenant-into-a-different-tenant-for-example-because-of-a-company-merger) to understand the process. Also, click here to learn how to [Request a tenant region move](https://learn.microsoft.com/en-us/power-bi/support/service-admin-region-move#request-a-region-move). <br/>
> - Microsoft Support will coordinate the migration of tenant, but you are responsible for backing up and restoring your data. <br/>
> - They can assist with troubleshooting if issues arise during backup or restore.

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Microsoft Fabric deployment patterns](https://learn.microsoft.com/en-us/azure/architecture/analytics/architecture/fabric-deployment-patterns)
- [Evaluate and optimize your Microsoft Fabric capacity](https://learn.microsoft.com/en-us/fabric/enterprise/optimize-capacity)
- [Configure Multi-Geo support for Fabric](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)
- [Migrate workspaces to a different region with fabric items removed (MS community)](https://community.fabric.microsoft.com/t5/Service/Migrate-workspaces-to-a-different-region-with-fabric-items/m-p/3700743)
- [I'm looking to move my Premium capacity to another region, will my dataflows still work? (MS community)](https://community.fabric.microsoft.com/t5/Service/I-m-looking-to-move-my-Premium-capacity-to-another-region-will/m-p/991510)
- [Change Data Region (MS community)](https://community.fabric.microsoft.com/t5/Desktop/Change-Data-Region/td-p/2538791)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Why Migrate?](#why-migrate)
- [Overview](#overview)
- [Create F64 Capacity in Central US Same Region as Current P1 and Reassign Workspaces](#create-f64-capacity-in-central-us-same-region-as-current-p1-and-reassign-workspaces)
- [Create F64 Capacity in East US Same Region as Data Sources and Azure Tenant and Reassign Power BI Content Only Workspaces, Manually Migrate Fabric Items](#create-f64-capacity-in-east-us-same-region-as-data-sources-and-azure-tenant-and-reassign-power-bi-content-only-workspaces-manually-migrate-fabric-items)
- [Create New Capacity in East US Before Migrating Fabric Tenant](#create-new-capacity-in-east-us-before-migrating-fabric-tenant)
- [Hybrid Approach with Phased Migration](#hybrid-approach-with-phased-migration)
- [Use Azure ExpressRoute](#use-azure-expressroute)

</details>

## Why Migrate?

| **Potential Challenges of a Cross-Region Setup** | **Description** |
|----------------------------------|-----------------|
| **Increased Latency** | Since `West US` and `West US 2` are separate Azure regions, any interaction between the Fabric tenant and its capacity involves `cross-region data movement`. While latency is relatively low, typically `single-digit milliseconds`, there can still be an impact on `high-frequency queries, refreshes, and DirectQuery models`. For dashboards with multiple visuals, `slight delays in load times` may occur, especially under heavy usage scenarios. |
| **Data Residency & Compliance Risks** | Although both regions are within the `United States`, some `industry-specific compliance frameworks` such as `CJIS, HIPAA, FedRAMP` may require workloads to reside within a `single Azure region` for legal or security reasons. If strict `data residency` is necessary, operating a `tenant in West US` and `capacity in West US 2` may introduce `governance complexities` that require additional review. |
| **Complex Troubleshooting** | If a report running on a `West US 2 capacity` is slow or encounters issues, `Microsoft support teams` may need to `coordinate across regions` to diagnose the root cause. `Logs, telemetry, and diagnostics data` may be `split across both regions`, creating challenges in `incident resolution` and `extending troubleshooting timelines`. |
| **Cost Implications** | `Azure charges for data egress` when transferring data between different regions. Though costs are lower for `intra-US transfers` compared to international movement, frequent `query execution, dataset refreshes, and data ingestion` between `West US` and `West US 2` may `gradually increase cloud expenses` over time. Organizations with `high data volume workloads` should carefully `monitor egress costs` to avoid unexpected billing spikes. |
| **Service Availability & Redundancy** | Some `Fabric features`, such as `OneLake shortcuts, real-time event streaming, and failover configurations`, may require `additional setup complexity` in a `cross-region tenant-capacity configuration`. If a `disaster recovery` scenario occurs, failing over a `Fabric service` from `West US` to `West US 2` might require `extra configuration` to ensure that `all metadata, permissions, and workspace structures` remain intact. |
| **Managed Private Endpoints Efficiency** | While `Managed Private Endpoints` enhance security by allowing `private connectivity`, using them across `West US` and `West US 2` requires `explicit network configurations`, needs proper routing. A `single-region setup` eliminates these extra network requirements, making `private endpoints` more efficient. |

## Overview 

> Below is a table with several scenarios that provide further details on when it is recommended to migrate your Fabric/Power BI tenant to a different region:

| **Action** | **Scenario** | **Example** | **Technical Details** |
|------------|--------------|-------------|-----------------------|
| **Migrate Tenant** | Data Sources in Different Region | Your data sources are in East US, and your current Fabric/Power BI tenant is in Central US. To optimize performance and ensure compliance, you migrate your tenant to East US, aligning it with your data sources to reduce latency and improve data processing speeds. | - Reduces latency by aligning tenant with data sources.<br>- Ensures compliance with data residency requirements.<br>- Simplifies management of data connections and credentials.<br>- Requires updating all data source connections and credentials to reflect the new tenant region.<br>- Potential downtime during migration, so plan for a maintenance window. |
| **Migrate Tenant** | Long-Term Regional Alignment | You plan to consolidate all resources in East US for better management and performance. Currently, your tenant is in Central US. You migrate your tenant to East US and then provision a new F64 capacity, aligning all resources in the same region. | - Aligns all resources in the same region for long-term management.<br>- Reduces complexity of multi-region setups.<br>- Ensures consistent performance and compliance.<br>- Requires thorough planning to ensure all services and data are migrated smoothly.<br>- May involve reconfiguring network settings and security policies. |
| **Migrate Tenant** | Compliance and Governance | Regulatory requirements mandate that your tenant and data sources be in the same region. Your data sources are in East US, but your tenant is in Central US. You migrate your tenant to East US to meet compliance requirements. | - Necessary for meeting specific compliance or governance requirements.<br>- Ensures data residency and regulatory compliance.<br>- Simplifies audit and management processes.<br>- Involves validating compliance requirements and ensuring all data is correctly migrated.<br>- May require coordination with legal and compliance teams. |
| **Reassign Workspaces** | Immediate Capacity Needs | Your current Power BI Premium P1 capacity in Central US is nearing its limit. You provision a new F64 capacity in East US and reassign your workspaces to this new capacity, addressing capacity issues immediately without migrating the tenant. | - Quick solution to manage capacity without full migration.<br>- Minimal disruption to ongoing operations.<br>- Ensure dataflows and datasets are configured for new capacity.<br>- Requires updating workspace settings to point to the new capacity.<br>- Monitor performance to ensure the new capacity meets your needs. |
| **Reassign Workspaces** | Temporary Solution | You need an immediate solution for capacity management and plan a future tenant migration. You provision a new F64 capacity in East US and reassign workspaces as a temporary measure, addressing current needs while planning for the tenant migration. | - Provides a temporary fix while planning for future migration.<br>- Avoids immediate complexities of tenant migration.<br>- Monitor performance and plan for eventual migration.<br>- Allows for phased migration, reducing risk of disruption.<br>- Requires careful tracking of which workspaces have been reassigned. |
| **Reassign Workspaces** | Performance Optimization | Your data sources are in East US, and you want to improve performance by reducing latency. You reassign workspaces to a new F64 capacity in East US, improving performance without migrating the tenant. | - Improves performance by moving workspaces closer to data sources.<br>- No need for full tenant migration.<br>- Ensure all datasets and dataflows are compatible with new capacity.<br>- Requires testing to ensure performance improvements are realized.<br>- May involve reconfiguring data refresh schedules to optimize performance. |

> Below are some methods (approaches to achieve it) for tenant migration.

## Create F64 Capacity in Central US (Same Region as Current P1) and Reassign Workspaces

> Easier reassignment but incurs egress charges and networking inefficiencies. Useful when immediate reassignment is needed without changing the tenant region.

> [!IMPORTANT]
> - Establishing a new capacity in Central US before migrating the tenant may introduce complications. The migration process could require reassigning workspaces and content to the new capacity, depending on the existing objects can be complex and time-consuming. <br/>
> - After migrating the tenant, `multi-geo limitations` would still apply if you have content spread across different regions. However, if all content is consolidated in the new region, some limitations might be reduced.

| Pros | Considerations |
| --- | --- |  
|  **Easy Workspace Reassignment**: Reassigning workspaces within the same region simplifies the process | - **Egress Charges**: Since the capacity is in a different region from your data sources and Azure tenant (East US), you will incur egress charges. <br/> - **Networking Inefficiencies**: Networking can be less efficient and more complex due to cross-region data transfers. Strategies to mitigate this include optimizing data performance, reviewing network architecture, improving redundancy, and using data transfer methods like Traffic Manager or ExpressRoute. | 

## Create F64 Capacity in East US (Same Region as Data Sources and Azure Tenant) and Reassign Power BI Content Only Workspaces, Manually Migrate Fabric Items

> No egress charges and more efficient networking but requires manual migration of Fabric items and conversion of Gen1 Dataflows. Useful for long-term efficiency and cost-effectiveness when data sources are in East US. 
> With this option, the Fabric tenant will remain in Central US, which affects the efficiency and cost of data transfers for Fabric-specific workloads. Although this option provides better performance for Power BI content, it adds some complexity in recreating the Fabric workloads.

> [!IMPORTANT]
> - The current P1 capacity should behave the same in the migrated tenant until you create the new capacity and reassign or move content. However, there might be some performance impacts due to the migration. <br/> 
> - Existing content in the P1 capacity, such as dataflows, might be affected during the transition. Multi-geo limitations could still apply until the content is fully migrated and reassigned to the new capacity.

| **Pros** | **Considerations** |
| --- | --- |
| - **No Egress Charges**: The capacity is in the same region as your data sources and Azure tenant, eliminating egress charges.<br/>- **Efficient Networking**: Reduced cross-region data transfer leads to more efficient and simpler networking. | - **Multi-Geo Limitations**: No Power BI Metrics feature. This can be worked around by creating custom reports or DAX measures to generate KPIs and reports.<br/>- **Convert Gen1 Dataflows**: All Gen1 Dataflows need to be converted to Gen2. Assistance can be provided for this process. Click [here for more information about how to move queries from Dataflow Gen1 to Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/move-dataflow-gen1-to-dataflow-gen2) <br/>- **Manual Migration of Fabric Content**: Items like data pipelines, data warehouses, notebooks, lakehouses, ML models, dataflows, or any embedded content need to be manually moved. |

## Create New Capacity in East US Before Migrating Fabric Tenant

> No egress charges and efficient networking but introduces complications in tenant migration and potential multi-geo limitations. Useful when planning to consolidate all resources in East US but requires careful planning.

> [!IMPORTANT]
> - Creating a new capacity in East US before migrating the tenant can introduce complications. The migration process might involve reassigning workspaces and content to the new capacity, which can be complex and time-consuming. <br/>
> - After migrating the tenant, `multi-geo limitations` would still apply if you have content spread across different regions. However, if all content is consolidated in the new region, some limitations might be reduced. <br/>
> - Unfortunately, there isn't a straightforward way to migrate both the tenant and capacity to East US without creating a new capacity. However, this process is not as complicated as it might seem. It typically involves creating a new capacity in the desired region and then migrating content to it. With proper planning and support, the migration can be managed smoothly and efficiently.

| **Pros** | **Considerations** |
| --- | --- |
| - **No Egress Charges**: The capacity is in the same region as your data sources and Azure tenant, eliminating egress charges.<br/>- **Efficient Networking**: Reduced cross-region data transfer leads to more efficient and simpler networking. | - **Complications in Tenant Migration**: Creating a new capacity in East US before migrating the tenant can introduce complications. The migration process might involve reassigning workspaces and content to the new capacity, which can be complex and time-consuming.<br/>- **Multi-Geo Limitations**: After migrating the tenant, multi-geo limitations would still apply if you have content spread across different regions. However, if all content is consolidated in the new region, some limitations might be reduced. |

## Hybrid Approach with Phased Migration

> Combines elements of the previous options, offering flexibility and reduced risk but requiring careful planning. Useful for addressing immediate capacity needs while planning for a full migration.

> [!IMPORTANT]
> - This approach allows for a phased migration, reducing the risk of disruptions and providing flexibility to address immediate capacity needs while planning for a full migration. <br/>
> - May incur temporary egress charges during the transition.

The hybrid approach involves a phased migration plan that combines elements of creating new capacity and migrating the tenant. This method allows you to address immediate capacity needs while planning for a full migration, reducing the risk of disruptions and providing flexibility.

**Phases**:
1. **Phase 1**: Create a new F64 capacity in East US and reassign critical workspaces to address immediate capacity needs. This step ensures that you can manage current workloads effectively without waiting for the entire migration process to complete.
2. **Phase 2**: Gradually migrate the tenant and remaining workspaces to East US. This phase involves careful planning and coordination to ensure a smooth transition. By migrating in stages, you can monitor the impact and make adjustments as needed, minimizing disruptions.

| **Pros** | **Considerations** |
| --- | --- |
| - **Flexibility**: Allows you to address immediate capacity needs while planning for a full migration.<br/>- **Reduced Risk**: Phased approach can reduce the risk of disruptions.<br/>- **Scalability**: Adaptable to different sizes and complexities of migrations. | - **Complexity**: Requires careful planning and coordination.<br/>- **Potential Temporary Egress Charges**: May incur temporary egress charges during the transition.<br/>- **Resource Allocation**: Adequate resources must be allocated to manage the migration phases.<br/>- **Testing and Validation**: Each phase should include thorough testing and validation. |

## Use Azure ExpressRoute

> Improved performance and reduced egress charges, though it involves setup complexity and costs. Useful for reducing latency and egress charges without immediate tenant migration.

> [!IMPORTANT]
> - Use Azure ExpressRoute to create a private connection between your on-premises infrastructure and Azure, reducing latency and egress charges. <br/>
> - There are costs associated with setting up and maintaining ExpressRoute.

| **Pros** | **Considerations** |
| --- | --- |
| - **Improved Performance**: Reduces latency and improves data transfer speeds.<br/>- **Cost Savings**: Reduces egress charges by using a private connection. | - **Setup Complexity**: Requires setup and configuration of ExpressRoute.<br/>- **Cost**: There are costs associated with setting up and maintaining ExpressRoute. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
