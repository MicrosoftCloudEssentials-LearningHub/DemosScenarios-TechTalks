# Multi-Geo support for Fabric - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> The `multi-geography setup` in Microsoft Fabric allows you to deploy content to data centers in regions other than the home region of your Fabric tenant. This feature is particularly useful for multinational customers who need to address regional, industry-specific, or organizational data residency requirements.` In your example, if you have the US as the geography with Central US and West US 2 as regions, you can set up a Fabric capacity reservation in one of these regions. Once a capacity is created, it remains in that region, and any workspaces created under it will have their content stored in that region`. This approach ensures that `you don't need to move the home region`, which can simplify management and compliance. Click [here for more information about it](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium)

<details>
<summary><b>List of References </b> (Click to expand)</summary>
  
- [How to request a tenant remap to another region](https://learn.microsoft.com/en-us/power-bi/support/service-admin-region-move#can-i-migrate-or-merge-my-power-bi-tenant-into-a-different-tenant-for-example-because-of-a-company-merger)
- [Overview of managed private endpoints for Fabric](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview)
- [Managed private endpoints](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview#limitations-and-considerations) - limitations and considerations
- [Multi-Geo](https://learn.microsoft.com/en-us/fabric/admin/service-admin-premium-multi-geo?tabs=power-bi-premium#considerations-and-limitations) - limitations and considerations
- [Private endpoints in Fabric](https://learn.microsoft.com/en-us/fabric/security/security-private-links-overview#what-is-a-private-endpoint)
- [Private links for secure access to Fabric](https://learn.microsoft.com/en-us/fabric/security/security-private-links-overview)
- [Microsoft Fabric concepts and licenses](https://learn.microsoft.com/en-us/fabric/enterprise/licenses#microsoft-fabric-concepts) - tenant, capacity, etc

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Fabric Object Residency](#fabric-object-residency)
- [Private Connectivity Residency](#private-connectivity-residency)
    - [Private Endpoints PE](#private-endpoints-pe)
    - [Private Link PL](#private-link-pl)
    - [Managed Private Endpoints MPE](#managed-private-endpoints-mpe)

</details>

https://github.com/user-attachments/assets/16fd8e90-22cc-48d3-8dce-e79e4ee9789b

> [!NOTE]
> When you deploy a workspace in a region different from your tenant’s home region, the `workspace’s data resides` in the region of the `capacity`. But, some `metadata and control-plane operations still interact with the tenant’s home region`. This setup supports data residency compliance while maintaining centralized governance. `Egress charges between regions like West US and West US 2 are minimal, especially since they are part of the same Azure geography (United States).`

## Fabric Object Residency

> - Fabric Tenant (Home Region): These components are global or control-plane level. <br/>
> - Fabric Capacity (Regional): These components are data-plane level and reside in the region where the capacity is deployed.

| **Fabric Tenant Location** | **Fabric Capacity Location** |
|----------------------------------|----------------------------------|
| - User identities and licenses (via Microsoft Entra ID)<br/>- Tenant-wide settings (e.g., Private Link enablement, governance policies)<br/>- Audit logs and telemetry<br/>- Global service configurations<br/>- Cross-region metadata coordination <br/>- Admin portal configurations<br/>- Capacity provisioning metadata | - Workspaces<br/>- Lakehouses and OneLake data<br/>- Data Warehouses<br/>- Notebooks and Pipelines<br/>- KQL Databases<br/>- Semantic Models and Datasets<br/>- Reports and Dashboards<br/>- Managed Private Endpoints<br/>- Data refresh and compute operations |

## Private Connectivity Residency

| **Connectivity Type**            | **Configuration Scope** | **Residency Behavior**| **Use Cases**| **Limitations**|
|----------------------------------|--------------------------|----------------------------------|----------------------------------------------|----------------|
| **Private Endpoints (PE)**       | Capacity                 | Bound to the **region of the Fabric capacity**. All traffic and data remain in that region. | Secure access to Fabric services within a specific region. | Must be in a supported region. Up to 450 capacities per tenant can support Private Link.              |
| **Private Link (PL)**            | Tenant                   | Applies **globally across the tenant**. Controls access to all capacities regardless of region. | Enforce secure-by-default access across all Fabric services. | Not all services support Private Link. Requires tenant-level configuration and DNS setup.             |
| **Managed Private Endpoints (MPE)** | Workspace (Capacity)               | Region is determined by the **capacity backing the workspace**. Data access is region-bound. | Secure access to external data sources (e.g., Azure SQL, Storage) from within a workspace.       | Workspace migration across regions is not supported. Must be recreated in the target region.          |

### Private Endpoints (PE)

> **Private Endpoints** are configured at the **capacity level**. They provide a secure, private IP-based connection to Fabric services, ensuring that traffic between your network and Fabric remains isolated from the public internet. Each private endpoint is tied to a specific Fabric capacity and is region-specific.

> [!IMPORTANT]  
> The private endpoint is bound to the **region where the capacity is provisioned**. All data and traffic routed through the endpoint remain within that region, supporting strict data residency and compliance requirements.

<details>
<summary><b>Use Cases</b> (Click to expand)</summary>

- **Isolating sensitive workloads from the public internet**: Private Endpoints ensure that communication between your network and Microsoft Fabric services occurs entirely over a private IP address within your Azure Virtual Network (VNet). This eliminates exposure to the public internet, significantly reducing the attack surface and enhancing security posture.
- **Ensuring compliance with regional data handling laws (e.g., GDPR, HIPAA)**:  By keeping data and traffic confined to a specific Azure region, Private Endpoints help organizations meet strict regulatory requirements for data residency and sovereignty. This is especially important for industries like healthcare, finance, and government.
- **Supporting secure, low-latency access to Fabric services within a specific Azure region**: Since traffic does not traverse the public internet, latency is minimized and performance is optimized for users and services operating within the same region. This is ideal for high-throughput analytics, real-time data processing, and latency-sensitive applications.
- **Enabling hybrid network architectures**: Organizations with on-premises infrastructure connected via VPN or ExpressRoute can use Private Endpoints to securely access Fabric services without routing traffic through the internet, maintaining a consistent and secure hybrid environment.
- **Segmenting access by region or business unit**: Enterprises operating in multiple regions or with distinct business units can assign separate capacities with their own Private Endpoints, allowing for granular control over network access and data boundaries.

</details>

<details>
<summary><b>Limitations</b> (Click to expand)</summary>

- **Region-specific**: Private Endpoints are strictly tied to the region of the Fabric capacity. They cannot be used to access services in other regions. This means that if your users or services are distributed globally, you must provision separate capacities and endpoints in each required region.
- **Capacity-bound**: Each Private Endpoint is associated with a specific capacity. If you scale out or migrate workloads to a different capacity (even within the same region), you must reconfigure the Private Endpoint for the new capacity. This adds operational overhead during scaling or rebalancing.
- **Provisioning delay**: After enabling Private Link and configuring a Private Endpoint, it can take up to **24 hours** for the endpoint to be fully registered and functional within the private DNS zone. This delay can impact deployment timelines and requires planning.
- **Quota limits**: Microsoft imposes a limit of **450 capacities per tenant** that can be configured with Private Link. Large enterprises with many regional workloads may approach this limit, requiring careful planning and capacity management.
- **DNS complexity**: Private Endpoints require integration with **Azure Private DNS Zones**. In complex environments, this may involve custom DNS forwarding rules, split-horizon DNS, or coordination with on-premises DNS infrastructure. Misconfiguration can lead to failed name resolution and service outages.
- **No cross-region failover**: Because endpoints are region-bound, they do not support automatic failover to another region. High availability across regions must be architected manually using multiple capacities and endpoints.

</details>

### Private Link (PL)

> **Private Link** is a **tenant-wide setting** that enforces secure, private access to Microsoft Fabric services across all capacities and regions. Once enabled, it ensures that all traffic to Fabric endpoints is routed through Azure’s private backbone network, bypassing the public internet.

> [!IMPORTANT]  
> Private Link applies **globally across the tenant**. It does not move or store data but governs how services are accessed, enforcing private connectivity across all regions and capacities.

<details>
<summary><b>Use Cases</b> (Click to expand)</summary>

- **Enforcing a zero-trust network model across the organization**: Private Link ensures that all access to Microsoft Fabric services is routed through Azure’s private backbone, eliminating exposure to the public internet. This aligns with zero-trust principles by minimizing the attack surface and enforcing strict access boundaries.
- **Blocking public internet access to Fabric services for all users and workloads**: Once Private Link is enabled at the tenant level, it overrides public endpoint access across all capacities and workspaces. This is ideal for organizations that require strict network isolation for compliance or security reasons.
- **Simplifying compliance audits by demonstrating that all traffic is private and encrypted**: With Private Link, organizations can show auditors that all data-in-transit is routed through private, encrypted channels. This supports compliance with standards like ISO 27001, SOC 2, and industry-specific regulations.
- **Centralized network governance**: Because Private Link is tenant-wide, it allows IT and security teams to enforce consistent network access policies across all regions and business units, reducing the risk of misconfiguration or policy drift.
- **Supporting secure hybrid connectivity**: Organizations with on-premises environments connected via ExpressRoute or VPN can use Private Link to securely access Fabric services without traversing the public internet, maintaining a consistent hybrid architecture.

</details>

<details>
<summary><b>Limitations</b> (Click to expand)</summary>

- **Global enforcement**: Private Link is a tenant-wide setting. Once enabled, it applies to all capacities and workspaces, regardless of region. This lack of granularity can be limiting for organizations that want to apply private access selectively.
- **Service support**: Not all Microsoft Fabric services may support Private Link at launch or in all regions. This can lead to inconsistent behavior or require fallback to public endpoints for unsupported services, which may conflict with security policies.
- **DNS and routing complexity**: Enabling Private Link requires careful DNS configuration, including integration with Azure Private DNS Zones. Misconfigured DNS can result in failed service resolution, broken connections, or routing loops, especially in hybrid or multi-region environments.
- **Cross-region latency**: Although traffic is routed privately, it may still traverse longer physical paths if users are accessing services in distant regions. This can introduce latency and impact performance for globally distributed teams.
- **Operational overhead**: Setting up and maintaining Private Link requires coordination between Azure administrators, network engineers, and security teams. It may also require updates to infrastructure-as-code templates, DNS forwarding rules, and monitoring configurations.
- **Limited rollback flexibility**: Once Private Link is enabled, reverting to public access requires deliberate reconfiguration and may disrupt services if not carefully planned. This makes testing and phased rollouts more complex.

</details>

### Managed Private Endpoints (MPE)

> **Managed Private Endpoints** are configured at the **workspace level**. They allow Fabric workspaces to securely connect to **external Azure resources** (e.g., Azure SQL, Azure Data Lake Storage) over a private network. These endpoints are created and managed within Fabric and are **not visible in the Azure portal**.

> [!IMPORTANT]  
> The region of a managed private endpoint is determined by the **region of the capacity** backing the workspace. This ensures that **data access remains within the same regional boundary**, which is essential for maintaining compliance and minimizing latency.

<details>
<summary><b>Use Cases</b> (Click to expand)</summary>

- Securely ingesting data from external sources into Fabric without exposing endpoints to the public internet.  
- Enabling fine-grained, workspace-specific access to Azure services.  
- Supporting hybrid data integration scenarios where Fabric connects to existing Azure-based data estates.  

</details>

<details>
<summary><b>Limitations</b> (Click to expand)</summary>

- **Region-locked**: Managed private endpoints are tied to the region of the workspace’s capacity. If you need to move the workspace to another region, you must **recreate the workspace and reconfigure all endpoints**.  
- **No workspace migration**: Fabric does not support native workspace migration across regions. Customers must use deployment pipelines, backups, or manual recreation.  
- **Manual approval required**: The owner of the target Azure resource must manually approve the connection request, which can delay setup.  
- **Limited visibility and tooling**: Managed private endpoints are not exposed in Azure Resource Manager or the Azure portal, making them harder to monitor and audit.  
- **Service compatibility**: Only certain Azure services are supported as targets for managed private endpoints. Unsupported services require alternative integration methods.  

</details>



<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
