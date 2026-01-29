# Multi-Region Load Balancing Architecture for MSFT Foundry - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-22

----------

> [!TIP]
> Leverages Azure API Management (APIM) as a unified gateway to orchestrate requests across multiple US regions where MSFT Foundry workloads are deployed.
> By distributing traffic through APIM, customers can mitigate TPM (tokens per minute) limitations and protect against isolated regional outages,
> while maintaining a consistent API surface for developers.

<details>
<summary><b>List of References</b> (Click to expand)</summary>
  
- [What is Azure API Management?](https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts)
- [What is Azure Front Door?](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)
- [Comparison between Azure Front Door and Azure CDN services](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-cdn-comparison)
- [GPT-RAG Solution Accelerator](https://github.com/Azure/GPT-RAG) - AI Factory
- [Hub-spoke network topology in Azure](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke)
- [Circuit Breaker pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker?utm_source=copilot.com)

    <img width="651" height="539" alt="image" src="https://github.com/user-attachments/assets/121c47f8-4297-454a-bcb2-62fddd58cdee" />

    <img width="1196" height="632" alt="image" src="https://github.com/user-attachments/assets/0a8a73f0-18bf-424d-8add-6eea9b04e004" />

- [Azure Load Balancer Best Practices](https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-best-practices?utm_source=copilot.com)
- [Baseline architecture for an Azure Kubernetes Service (AKS) cluster](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks)

    <img width="1063" height="833" alt="image" src="https://github.com/user-attachments/assets/cde38e46-9f20-450d-a022-40eff4cd4c07" />

</details>
  
> To enhance resiliency and scalability, the solution can be split into frontend and backend layers: `This design ensures high availability, performance optimization, and simplified management, while preparing teams for new model rollouts that may initially be limited to specific regions.`

1. Frontend Layer:
   - `Azure Front Door` provides global entry points, latency-based routing, and DDoS protection.
   - `Microsoft Entra ID` secures authentication and authorization for user access.
2. Backend Layer:
   - `Regional APIM instances and load balancers` distribute workloads across MSFT Foundry deployments.
   - Architectures can follow either a `hub-and-spoke model` (centralized control with spokes in each region) or a `hub-to-hub model` (interconnected hubs for regional autonomy).

        | Approach | Structure | Strengths | Trade-offs |
        |----------|-----------|-----------|------------|
        | **Hub-to-Hub** | Multiple hubs interconnected | High resiliency, regional autonomy | More complex networking, higher cost |
        | **Hub-and-Spoke** | One central hub, multiple spokes | Easier to manage, centralized policies | Hub becomes a critical dependency |

> [!NOTE]
> For **MSFT Foundry APIs**, you can use **Application Gateway** because it’s HTTP/S‑aware, integrates with APIM, and provides advanced routing + [WAF](https://docs.azure.cn/en-us/web-application-firewall/overview) security. Azure Load Balancer is useful for **internal, low‑level traffic distribution**, but not sufficient on its own for developer‑facing Foundry workloads.
> - If your Foundry `deployments are directly consumed as APIs (which they usually are), Application Gateway is the right fit` because it understands `HTTP/S and integrates naturally with APIM.`
> - If your `Foundry workloads are wrapped inside VM/container clusters and you just need raw traffic distribution, Load Balancer` is simpler and faster. But you’d still `need APIM or Gateway in front for API‑level features.`

<img width="567" height="383" alt="image" src="https://github.com/user-attachments/assets/bb67fc6c-5407-49b2-8a1f-52963689d37d" />

From [What is Azure Web Application Firewall?](https://docs.azure.cn/en-us/web-application-firewall/overview)

> [!TIP]
> If you have a solid foundation by using APIM as the orchestrator across multiple MSFT Foundry deployments. The design is purpose‑built, resilient, and developer‑friendly. The next evolution would be layering in Front Door for external traffic, refining routing models, and strengthening observability and failover automation.
> - Frontend Layer: If external users or customers will consume AI services, consider adding Azure Front Door for global entry, latency‑based routing, and DDoS protection.
> - Routing Models:
>   - Hub‑and‑Spoke: Central APIM hub routes to regional spokes. Easier to manage.
>   - Hub‑to‑Hub: Each hub can route to others, improving resiliency but adding complexity.
> - Observability: Centralize logs and metrics in Azure Monitor + Application Insights for full visibility.
> - Failover Automation: Implement health probes and rerouting logic to handle outages seamlessly.
> - Future‑Proofing: Pre‑provision capacity in regions where new models are released first.

## Unified Gateway with APIM

`Applications only call APIM endpoints, not individual Foundry instances. This simplifies SDKs and client logic.`

- Role of APIM: APIM sits at the edge of each region, exposing a consistent API surface to developers. It abstracts away the complexity of multiple Foundry deployments.
- Policies: Developers can configure APIM policies for:
    - Rate limiting: Prevent exceeding TPM quotas per region.
    - Conditional routing: Direct traffic based on headers, tokens, or quota status.
    - Transformation: Normalize requests/responses across regions.

<img width="1620" height="1098" alt="image" src="https://github.com/user-attachments/assets/58f8f967-0334-4174-8ea4-1b6e6b5b6cf8" />

From [What is Azure API Management?](https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts)

> API Management components:

<img width="783" height="400" alt="image" src="https://github.com/user-attachments/assets/e11b03c9-e36c-4502-bc34-272b2b549026" />

From [What is Azure API Management?](https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts)

> E.g 

<img width="1407" height="860" alt="image" src="https://github.com/user-attachments/assets/0ba7a045-b7e1-4297-b690-d3e87d74532d" />

From [GPT-RAG Solution Accelerator](https://github.com/Azure/GPT-RAG)

## Frontend Layer

`Frontend ensures that user traffic is secure and optimized before hitting backend workloads. You don’t need to hardcode region logic in the client, Front Door handles it`

- Azure Front Door:
    - Provides global entry points with latency‑based routing.
    - Uses health probes to detect regional failures and reroute traffic.
    - Supports caching for static responses, reducing load on Foundry.
- Microsoft Entra ID:
    - Handles OAuth2/OpenID Connect flows for secure access.
    - Issues tokens that APIM validates before forwarding requests.
    - Developers integrate Entra ID into client apps (web/mobile) for seamless authentication.

<img width="500" height="530" alt="image" src="https://github.com/user-attachments/assets/33e45a0e-ea29-4f16-b53e-d93586c61007" />

From [What is Azure Front Door?](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)

<img width="1200" height="581" alt="image" src="https://github.com/user-attachments/assets/bcf03970-950f-4a6a-b945-f7c6d99d3820" />

From [Comparison between Azure Front Door and Azure CDN services](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-cdn-comparison)

> E.g Front Door + PE:

<img width="1518" height="698" alt="image" src="https://github.com/user-attachments/assets/a4c822b1-8bc1-4346-beb8-613141fb8f84" />

## Backend Layer

> [!TIP]
> `Azure Monitor + Application Insights provide real‑time metrics on TPM consumption, latency, and error rates.`
> - APIM policies track TPM usage.
> - When nearing limits, traffic is rerouted to another region.
> - Developers implement retry logic with exponential backoff to handle throttling gracefully.

- Regional APIM Instances: Each region has its own APIM connected to local Foundry deployments. Developers can configure per‑region policies (e.g., TPM quotas, logging).
- Load Balancers:
    - Azure Load Balancer or Application Gateway distribute traffic across multiple Foundry instances in a region.
    - Health probes detect unhealthy instances and remove them from rotation.
        
        | Dimension | **Azure Load Balancer** | **Azure Application Gateway** |
        |-----------|--------------------------|-------------------------------|
        | **Core Functionality** | Operates at **Layer 4 (TCP/UDP)**. Distributes raw network traffic across backend pools (VMs, containers, or services). No awareness of HTTP/S protocols. Best for simple, high‑throughput scenarios. | Operates at **Layer 7 (HTTP/S)**. Fully protocol‑aware, designed for web/API workloads. Supports SSL termination, URL/path‑based routing, and advanced traffic rules. |
        | **Health & Routing** | Uses **TCP/UDP probes** to check if instances are reachable. Routing is basic (round‑robin, hash‑based). No ability to inspect API responses. | Uses **HTTP/S probes** that can validate Foundry endpoints directly. Supports routing by path, hostname, headers, and cookies. Enables intelligent failover and sticky sessions. |
        | **Security & Features** | Provides basic distribution only. Security handled externally (NSGs, firewalls). No SSL offload, no [WAF](https://docs.azure.cn/en-us/web-application-firewall/overview). | Includes **Web Application Firewall ([WAF](https://docs.azure.cn/en-us/web-application-firewall/overview))**, SSL/TLS termination, request inspection, and session affinity. Directly protects Foundry APIs from malicious traffic. |
        | **Developer Impact** | Lightweight, fast, but requires APIM or another Layer 7 service for API‑aware routing, logging, and quota enforcement. Developers see it as “plumbing.” | Rich features directly usable by developers: routing rules, SSL offload, [WAF](https://docs.azure.cn/en-us/web-application-firewall/overview), cookie affinity. Integrates naturally with APIM for policy enforcement and observability. |
        | **Best Fit for Foundry** | Internal traffic distribution where simplicity and raw throughput matter (e.g., VM/container clusters hosting Foundry). | External/API traffic distribution where **security, routing intelligence, and observability** are critical — the recommended choice for MSFT Foundry workloads. |
- Routing Models:
    - Hub‑and‑Spoke: Central hub routes traffic to spokes (regional APIM + Foundry). Easier to manage, but hub is a dependency.
    - Hub‑to‑Hub: Each hub can route to others, providing regional autonomy. More resilient but complex networking.
        
        | Dimension | **Hub‑and‑Spoke** | **Hub‑to‑Hub** |
        |-----------|-------------------|----------------|
        | **Topology** | One **central hub VNet** peered with multiple **spoke VNets**. All traffic flows through the hub before reaching regional APIM + Foundry. | Multiple **regional hubs**, each with its own APIM + Foundry. Hubs are interconnected via VNet peering or Azure Virtual WAN, allowing direct routing between hubs. |
        | **Traffic Flow** | User → Front Door → Hub APIM → Spoke APIM/Foundry → Response. Centralized routing logic. | User → Front Door → Nearest Hub APIM → Local Foundry OR rerouted to another hub if local capacity is exceeded/outage. |
        | **Control Plane** | Centralized: policies, quotas, and routing rules defined at the hub APIM. Developers manage one control point. | Distributed: each hub maintains its own APIM policies, quotas, and routing rules. Developers must coordinate across hubs. |
        | **Resiliency** | Hub is a **single point of dependency**. If hub fails, spokes are unreachable unless fallback is designed. | No single dependency. Each hub can operate independently. Outages in one hub don’t affect others. |
        | **Complexity** | Easier to design and manage. Clear separation of responsibilities. | Higher complexity: requires consistent policy replication, routing synchronization, and monitoring across hubs. |
        | **Latency** | Potentially higher latency: traffic always traverses hub before reaching spoke. | Lower latency: traffic can terminate at nearest hub without detouring through a central hub. |
        | **Networking Requirements** | Hub VNet must be sized for aggregate traffic. Requires hub‑spoke peering and routing tables. | Requires **full mesh peering** or Virtual WAN. More complex routing tables and potential overlapping IP address challenges. |
        | **Security** | Centralized firewall and NSGs at hub enforce security. Easier to audit and control. | Security distributed across hubs. Each hub must replicate firewall rules and NSGs consistently. |
        | **Quota Management (TPM)** | Hub monitors TPM usage across spokes. Easier to implement quota‑aware routing logic. | Each hub monitors its own TPM usage. Requires cross‑hub coordination to balance workloads. |
        | **Failover Strategy** | Failover logic must be implemented at hub level. If hub is down, fallback requires secondary hub or alternate entry point. | Failover is local to each hub. Front Door can reroute traffic to another hub automatically. |
        | **Observability** | Centralized logging and monitoring at hub. Easier to correlate traffic flows. | Distributed logging. Requires aggregation across hubs for full visibility. |
        | **DevOps Impact** | Single CI/CD pipeline for hub APIM policies. Spokes are simpler (mostly Foundry + load balancers). | Multiple CI/CD pipelines for each hub APIM. Requires automation to ensure consistency. |
        | **Cost Considerations** | Lower operational cost: fewer APIM instances, centralized infrastructure. | Higher cost: multiple hubs with APIM, monitoring, and networking overhead. |
        | **Best Use Case** | Organizations prioritizing **simplicity and centralized control**. Suitable for small/medium deployments. | Organizations prioritizing **resiliency, autonomy, and low latency**. Suitable for large, distributed deployments. |

        > Hub-spoke network topology in Azure:
        
        <img width="1083" height="681" alt="image" src="https://github.com/user-attachments/assets/6833341f-2ae0-4aa9-9159-193e3e35f713" />
        
        From [Hub-spoke network topology in Azure](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
