# Migrating from <br/> Multi-container Web Apps to AKS - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is Azure Kubernetes Service (AKS)?](https://learn.microsoft.com/en-us/azure/aks/what-is-aks)
- [Choose an Azure compute service (Decision Tree)](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)
- [Free, Standard, and Premium pricing tiers for Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/free-standard-pricing-tiers)
- [AKS long-term support](https://learn.microsoft.com/en-us/azure/aks/long-term-support)
- [AKS pricing details](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- [Azure managed disk types](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types)
- [Disk type comparison](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types#disk-type-comparison)
- [Microsoft Sales and Support](https://support.microsoft.com/contactus?ContactUsExperienceEntryPointAssetId=S.HP.SMC-HOME)
- [Microsoft Copilot in Azure (VM sizing demo video)](https://www.youtube.com/watch?v=HGdhUFHnij4&t=819s)
- [Cluster components](https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts#cluster-components)

    <img width="1947" height="662" alt="image" src="https://github.com/user-attachments/assets/7398b98f-499b-4707-9c69-163cf520c88d" />

- [Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale)
- [Best practices for performance and scaling for large workloads in Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale-large)
- [Best practices for network policies in Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/network-policy-best-practices)
- [We can use Cilium instead of `kube-proxy`](https://learn.microsoft.com/en-us/azure/aks/network-policy-best-practices#azure-powered-by-cilium)

  <img width="1693" height="738" alt="image" src="https://github.com/user-attachments/assets/22185e92-58ac-4119-9c56-c1c87345c242" />

- [Using Azure API Management Circuit Breaker and Load balancing with Azure OpenAI Service](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/using-azure-api-management-circuit-breaker-and-load-balancing-with-azure-openai-/4041003)
- [Expose an agent as an MCP tool](https://learn.microsoft.com/en-us/agent-framework/tutorials/agents/agent-as-mcp-tool?pivots=programming-language-python)
- [How to configure a private link for Microsoft Foundry (Foundry projects)](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/configure-private-link?view=foundry-classic&utm_source=copilot.com)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Overview](#overview)
- [Container related services](#container-related-services)
- [How to choose?](#how-to-choose)
- [Pricing example](#pricing-example)
- [Migration process](#migration-process)
- [Best practices](#best-practices)

</details>

> [!NOTE]
> If you have any questions or need further clarification, please reach out to your Microsoft account team or contact Microsoft directly: [Microsoft Sales and Support](https://support.microsoft.com/contactus?ContactUsExperienceEntryPointAssetId=S.HP.SMC-HOME) for additional support and guidance, or  more detailed information.

| Component | Role | 
| --- | --- | 
| Containers | Lightweight, `portable units that package code, dependencies, and runtime together`. | 
| Docker | Tool that `builds and runs these containers locally`. It lets you define`multi-container setups using docker-compose.` |
| Docker Compose | Manages multiple containers on one host |
| Kubernetes (K8s) | Orchestrates containers across many hosts (nodes) | 
| AKS | Azure’s managed Kubernetes `handles infrastructure, scaling, and updates for you` | 

## Overview 

`Monolithic → Microservices → Containerization → Orchestration` This progression improves scalability, resilience, and agility for modern cloud-native applications.

<div align="center">
  <img width="778" height="369" alt="image" src="https://github.com/user-attachments/assets/23f6e6e9-1c37-47f5-afae-e5fcdf847d93" />
</div>

> - `Monolithic Application`: A single, large application that contains all components (Recruitment Website, Job Application, Job Vacancies, Recruiters, etc) bundled together.
>   - The modules really rely on each other quite a bit.
>   - It's tricky to scale features on their own.
>   - Any updates mean we have to redeploy the whole app.
> - `Transition to Microservices`: The monolithic app is split into smaller, independent services (Recruiters, Job Application, Job Vacancies).
>   - Each service can be developed, deployed, and scaled independently.
>   - Easier to maintain and adopt new technologies per service.
> - `Docker`: Each microservice is packaged into application containers using Docker.
>   - Provides portability across environments.
>   - Ensures consistency between development and production.
> - `Kubernetes`: Containers are deployed and managed in a Kubernetes cluster (K8s).
>   - Handles orchestration: scaling, load balancing, self-healing.
>   - Enables automated deployments and rolling updates.

## Container related services

> Typical Flow:

1.  **Build image → Push to ACR**
2.  **Choose deployment service:**
    *   AKS (more flexible orchestration)
    *   Container Apps (simpler, serverless)
    *   ACI (quick jobs)
3.  **Add storage if needed**
4.  **Configure networking, scaling, monitoring**

<div align="center">
  <img width="750" height="677" alt="image" src="https://github.com/user-attachments/assets/400f5be2-45c2-4486-9c53-adf739aff4d0" />
</div>

<details>
<summary><b> 1. Azure Container Registry (ACR)</b> (Click to expand)</summary>
  
> This is where you store your container images (like Docker images). Think of it as your private container image repository.
> - **When to use:** Almost always if you’re deploying containers in Azure. You build your app locally or in CI/CD, push the image to ACR, and then other services (AKS, Container Apps, etc.) pull from it.
> - **Setup order:** Usually first, because your deployment services need access to the images.
  
</details>

<details>
<summary><b>2. Azure Kubernetes Service (AKS)</b> (Click to expand)</summary>

> A managed Kubernetes cluster for running containerized workloads at scale.
> - **When to use:** If you need orchestration, scaling, and advanced networking for multiple containers or microservices.
> - **Relation to ACR:** AKS pulls images from ACR to run your pods.
> - **Setup order:** After ACR is ready and your images are pushed.

</details>

<details>
<summary><b>3. Azure Container Apps</b> (Click to expand)</summary>

> A serverless container platform for microservices and apps without managing Kubernetes directly.
> - **When to use:** If you want simplicity from management perspective and autoscaling.
> - **Relation to ACR:** Same as AKS, pulls images from ACR.
> - **Setup order:** After ACR.

</details>

<details>
<summary><b>4. Azure Container Instances (ACI)</b> (Click to expand)</summary>

> Run containers quickly without orchestration, good for short-lived tasks or simple apps.
> - **When to use:** For lightweight workloads or batch jobs.
> - **Relation to ACR:** Can also pull images from ACR.

</details>

<details>
<summary><b>5. Azure Container Storage</b> (Click to expand)</summary>

> Persistent storage for stateful containers.
> - **When to use:** If your containers need to keep data beyond their lifecycle (e.g., databases).
> - **Setup order:** Alongside AKS or Container Apps if needed.

</details>

<details>
<summary><b>6. Azure Kubernetes Service Edge Essentials</b> (Click to expand)</summary>

> On-premises Kubernetes for edge scenarios.
> - **When to use:** If you need hybrid or edge deployments.

</details>

## How to choose?

<img width="900" height="916" alt="image" src="https://github.com/user-attachments/assets/259cba67-0742-4ff8-b9b5-4481772c04f9" />

From [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)

## Pricing example

> AKS `itself is free`; you pay for:
> - VMs in Node Pools (Standard vs Premium SSD, VM size)
> - Networking (Azure CNI vs Kubenet)
> - Storage
> - Optional features (e.g., Azure Monitor, Virtual Nodes)
> Your `node VM size and features define cost and performance.`

How determine which **AKS tier** (or node size/configuration) you need, you can follow these steps:

> [!NOTE]
> Quick Way to Decide:
- If you want **low cost** → B-series or Spot VMs.
- If you want **balanced performance** → D-series.
- If you need **high compute** → F-series or GPU nodes.

1. Estimate Resource Requirements:
  - **CPU & Memory per container**: Check your app’s baseline usage.
  - **Number of containers per pod**: Multi-container apps share pod resources.
  - **Expected traffic**: Peak vs average load.
2. Use AKS Recommendations: 
  - Enable **Cluster Autoscaler** and **Horizontal Pod Autoscaler**.
  - Use **Azure Advisor** → It gives cost and performance recommendations based on telemetry.

> [!TIP]
> Use [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339) and **AKS Sizing Guide**:

From AKS perspective we can choose between tier for the cluster management, click here for more details about [Free, Standard, and Premium pricing tiers for Azure Kubernetes Service (AKS) cluster management](https://learn.microsoft.com/en-us/azure/aks/free-standard-pricing-tiers)

| **Feature**                 | **Free Tier** | **Standard Tier** | **Premium Tier** |
| --------------------- | -------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **When to Use**             | - Experiment with AKS at no cost<br>- New to AKS/Kubernetes                                 | - Production or mission-critical workloads needing high availability<br>- Financially backed SLA    | - Mission-critical workloads requiring **two years** of Kubernetes version support<br>- Highest reliability |
| **Supported Cluster Types** | - Dev/test clusters<br>- Clusters < 10 nodes                                                | - Enterprise-grade or production workloads<br>- Up to 5,000 nodes                                   | - Enterprise-grade or production workloads<br>- Up to 5,000 nodes                                           |
| **Pricing**                 | - Free cluster management<br>- Pay-as-you-go for resources                                  | - Pay-as-you-go for resources<br>- [Standard tier cluster management pricing](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/)                         | - Pay-as-you-go for resources<br>- [Premium tier cluster management pricing](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/)|
| **Feature Comparison**      | - Recommended for clusters < 10 nodes<br>- Supports up to 1,000 nodes<br>- All AKS features | - Uptime SLA enabled<br>- Greater reliability<br>- Supports up to 5,000 nodes<br>- All AKS features | - Includes all Standard tier features<br>- [Microsoft maintenance past community support](https://learn.microsoft.com/en-us/azure/aks/long-term-support)                     |

> [!TIP]
> Which Tier Should You Choose?
> - **Free Tier** → Best for **testing or learning**, small clusters (<10 nodes).
> - **Standard Tier** → Best for **production workloads**, SLA-backed, up to 5,000 nodes.
> - **Premium Tier** → Best for **mission-critical workloads**, extended Kubernetes version support (2 years), and advanced reliability.

<img width="1198" height="392" alt="image" src="https://github.com/user-attachments/assets/97244861-fd9c-476a-9a40-d90d49c18e0c" />

> [!NOTE]
> Cost Impact as today (check last updated date):
> - **Free Tier**: $0 for cluster management, pay for nodes only.
> - **Standard Tier**: Adds cluster management cost (usually $0.10/hour per cluster).
> - **Premium Tier**: Higher cluster management cost + advanced support.

E.g as today (check last updated date):

<img width="1410" height="977" alt="image" src="https://github.com/user-attachments/assets/6992a004-c148-44f2-9235-4f00b988f255" />

For VMs in Node Pools (Standard vs Premium SSD, VM size): 

<img width="1217" height="972" alt="image" src="https://github.com/user-attachments/assets/accbab1c-4818-46db-ba5e-22dbc4a7b5ae" />

- You can use `Microsoft Copilot in Azure` to find the `best VM size for you`. Click here to see the [demo on how to use it](https://www.youtube.com/watch?v=HGdhUFHnij4&t=819s).
  - Copilot uses your `subscription details and resource availability to recommend the most suitable VM size.`
  - It can also `assist with quota checks and guide you to request more capacity if needed.`

    <img width="1910" height="1003" alt="image" src="https://github.com/user-attachments/assets/6deae8de-410f-478f-9327-a5af8b296fa3" />
    
- And, Managed OS Disks in Azure are block-level storage volumes that are automatically managed by Azure for virtual machines. Click here to read more about [Azure managed disk types](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types)

    <img width="1200" height="662" alt="image" src="https://github.com/user-attachments/assets/2d6773ce-45eb-4053-a1d1-791ab106d023" />

From [Disk type comparison](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-types#disk-type-comparison)

## Migration process

> Difference Between Stateless and Stateful Applications:

| **Aspect**           | **Stateless Application**                                    | **Stateful Application**                                      |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------- |
| **Definition**       | `Does not retain data or session state` between requests.      | `Maintains data or session state across` requests or restarts.  |
| **Examples**         | Web front-end, REST APIs, microservices without persistence. | Databases, message queues, AI model serving with local cache. |
| **Scaling**          | Easy to scale horizontally; `no dependency on storage.`        | Requires persistent storage and careful scaling strategies.   |
| **Storage Needs**    | None or external (e.g., cloud DB).                           | Needs Persistent Volumes (PV/PVC) and StatefulSets in AKS.    |
| **Migration Effort** | Mostly lift-and-shift (Deployment + Service).                | Requires PV/PVC, StatefulSets, backup/restore planning.       |

> ACA (Azure Container Application) → AKS Migration:
- **Stateless apps** → Mostly lift-and-shift (Deployment + Service + Ingress).
- **Stateful apps** → Additional work for storage, StatefulSets, and backup strategies.
- **Infrastructure changes** → Networking, ingress, scaling, monitoring, and governance must be explicitly configured in AKS.

| **Category**                  | **Details** |
| ----------------------------- | -------------- |
| **Infrastructure Components** | - **Container Image**: Reuse from Azure Container Registry (ACR); configure image pull secrets.<br>- **Networking**: Plan VNet, node pool subnet, Service CIDR, Pod CIDR.<br>- **Ingress / Routing**: Deploy Ingress Controller (NGINX or Azure Application Gateway), configure DNS and TLS.<br>- **Scaling**: Set up Horizontal Pod Autoscaler (HPA) or install KEDA manually.<br>- **Monitoring**: Enable Azure Monitor for Containers and Log Analytics.<br>- **Secrets Management**: Create Kubernetes Secrets for sensitive data.<br>- **Persistent Storage**: Define Persistent Volumes (PV), Persistent Volume Claims (PVC), and StatefulSets for stateful workloads.<br>- **Governance**: Apply Azure Policy and RBAC for cluster compliance. |
| **Application Components**    | - **App Code**: No major changes if already containerized; validate readiness for Kubernetes (health probes, resource limits).<br>- **Environment Variables**: Move to ConfigMaps (non-sensitive) and Secrets (sensitive).<br>- **Ingress Rules**: Create Kubernetes Ingress YAML for routing.<br>- **Autoscaling Policies**: Configure resource requests/limits and HPA/KEDA triggers.<br>- **Advanced Features**: Install Dapr for service invocation or event-driven patterns; configure GPU node pools for AI workloads.<br>- **Stateful Logic**: Update app to use persistent storage paths if needed.<br>- **Observability Hooks**: Ensure app exposes metrics for Prometheus/Azure Monitor integration.                                        |

## Modern Traffic Patterns for AKS

> Strengthening API, Routing, and Global Traffic Strategy: `AKS introduces more moving parts, more flexibility, and more responsibility for traffic management, resiliency, and observability.`
> - You now own the orchestration layer.
> - You need stronger traffic management.
> - You need more robust observability.
> - You need better failover automation.
> - You need global routing if you’re serving AI workloads.


Your architecture evolves like this:

```
┌──────────────────────┐   ┌──────────────────────────┐   ┌────────────────────────────┐   ┌──────────────────────────┐   ┌────────────────────────────────┐
│   Azure Front Door    │ → │ Azure API Management      │ → │   AKS Ingress Controller    │ → │   Kubernetes Services     │ → │ Pods / Microservices / AI Models │
│ - Global routing       │   │ - Auth & rate limits      │   │ - NGINX / AGIC / Traefik    │   │ - Stable virtual IPs      │   │ - Application containers         │
│ - WAF / DDoS           │   │ - API abstraction layer   │   │ - Path/host routing         │   │ - Internal load balancing  │   │ - AI model runtimes              │
└──────────────────────┘   └──────────────────────────┘   └────────────────────────────┘   └──────────────────────────┘   └────────────────────────────────┘
```

<details>
<summary><b>Click here to read more about it</b></summary>

1. **Azure Front Door (the global entry point):**  
   - Everything starts at Azure Front Door. This is our global edge layer.  
   - It gives us global routing, latency‑based load balancing, WAF, and DDoS protection.  
   - Before traffic even reaches our APIs or our cluster, it’s already secured and optimized.
2. **Azure API Management (the API control plane):**  
   - After Front Door, traffic flows into APIM.
   - This is where we enforce authentication, rate limits, transformations, and API governance.
   - APIM abstracts the backend, so clients never know whether the workload runs on App Service, AKS, or something else.
3. **AKS Ingress Controller (the cluster’s entry point):**
   - APIM forwards the request to the AKS Ingress Controller.
   - This component handles routing rules such as hostnames, paths, and TLS.
   - It decides which Kubernetes Service inside the cluster should receive the request.
5. **Kubernetes Services (stable internal endpoints):**
     - Behind the Ingress, Kubernetes Services provide stable virtual IPs.
     - Even if pods scale up, down, or move between nodes, the Service endpoint stays the same.
     - This decouples traffic routing from the actual container instances.
6. **Pods / Microservices / AI Models (the workloads):**
   - Finally, the request reaches the actual workloads running inside AKS.
   - These can be microservices, APIs, background workers, or AI model runtimes.
   - This is where the business logic executes and the response is generated.

</details>

<img width="600" alt="image" src="https://github.com/user-attachments/assets/d8d24dd6-e744-436d-9bae-1c51d9597d55" />

From [Defender for Containers architecture](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-architecture?tabs=defender-for-container-arch-aks)

<img width="1063" height="833" alt="image" src="https://github.com/user-attachments/assets/6a944706-ec3f-4a14-ba56-20ca5baf7c6e" />

From [Baseline architecture for an Azure Kubernetes Service (AKS) cluster](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks)

| Architecture Area | Detailed Explanation | Why It Still Applies with AKS | How It Integrates with AKS | Key Benefits | Risks If Ignored |
|-------------------|----------------------|-------------------------------|-----------------------------|--------------|------------------|
| **APIM as the Orchestrator** | - Acts as unified API gateway<br/>- Centralizes auth, rate limiting, transformations, versioning<br/>- Abstracts backend infrastructure from clients<br/>- Provides consistent API governance | - APIM hides backend changes (App Service → AKS)<br/>- Prevents exposing AKS directly<br/>- Maintains stable API contracts<br/>- Ensures consistent policies across services | - APIM forwards traffic to AKS via Ingress Controller<br/>- Backend URLs simply point to AKS Ingress endpoints<br/>- No client‑side changes required | - Stable API surface<br/>- Centralized governance<br/>- Security boundary<br/>- Backend abstraction<br/>- Developer‑friendly onboarding | - Clients tightly coupled to backend<br/>- AKS exposed directly<br/>- No centralized throttling or auth<br/>- Harder API lifecycle management |
| **Azure Front Door** | - Global entry point for all external traffic<br/>- Provides WAF, DDoS protection, TLS termination<br/>- Offers global load balancing and latency‑based routing | - AKS is regional; Front Door provides global reach<br/>- Adds edge security before traffic hits APIM or AKS<br/>- Improves performance and resiliency | - Typical flow: Users → Front Door → APIM → AKS<br/>- Can also route directly to AKS Ingress if needed | - Global routing<br/>- Edge security<br/>- Faster TLS termination<br/>- Multi‑region failover<br/>- Performance acceleration | - No global resiliency<br/>- Higher latency for global users<br/>- No edge protection<br/>- Regional outages impact customers |
| **Routing Model: <br/> Hub‑and‑Spoke** | - Central APIM hub<br/>- Regional AKS clusters as spokes<br/>- Front Door routes to APIM hub, APIM routes to regions | - Simplifies governance<br/>- Aligns with enterprise landing zones<br/>- Reduces operational overhead | - APIM hub forwards requests to regional AKS Ingress endpoints<br/>- Centralized policy enforcement | - Easy management<br/>- Centralized governance<br/>- Predictable routing<br/>- Lower operational complexity | - APIM hub becomes a bottleneck<br/>- Slightly higher latency for distant regions |
| **Routing Model: <br/> Hub‑to‑Hub** | - Multiple APIM instances globally<br/>- Each APIM can route to others or local AKS clusters<br/>- Supports active‑active deployments | - AKS supports multi‑region active‑active patterns<br/>- Improves resiliency and performance for global users | - Each APIM instance routes to its nearest AKS cluster<br/>- Cross‑region APIM routing for failover | - High resiliency<br/>- Low latency for global users<br/>- True active‑active architecture | - Higher complexity<br/>- More governance overhead<br/>- Requires strong observability |
| **Observability** | - Centralized logs and metrics<br/>- Tracks cluster health, pods, deployments<br/>- Monitors ingress traffic and service mesh telemetry<br/>- Captures application and container logs | - AKS adds more moving parts than App Service<br/>- Requires deeper visibility into cluster internals<br/>- Ensures reliability and performance | - Azure Monitor for Containers<br/>- Application Insights for app telemetry<br/>- Optional: Prometheus, Grafana, OpenTelemetry | - Full visibility<br/>- Faster troubleshooting<br/>- Better performance tuning<br/>- Stronger SRE practices | - Blind spots in cluster health<br/>- Harder debugging<br/>- Increased downtime risk<br/>- No insight into traffic patterns |
| **Failover Automation** | - Automated detection and rerouting during outages<br/>- Uses health probes and multi‑region logic<br/>- Works across Front Door, APIM, and Kubernetes | - AKS gives more control over failover<br/>- Multi‑region clusters need automated routing<br/>- Ensures high availability | - Front Door handles global failover<br/>- APIM can route to alternate backends<br/>- Kubernetes uses readiness/liveness probes + HPA/KEDA | - High availability<br/>- Seamless failover<br/>- Reduced downtime<br/>- Better user experience | - Outages impact customers<br/>- Manual failover required<br/>- No resilience to regional failures |
| **Future‑Proofing (AI & GPU Workloads)** | - Pre‑provision capacity in regions where new models appear first<br/>- GPU node pools take time to scale<br/>- AI workloads require specific SKUs (A100, H100, MI300X) | - AKS scaling is slower for GPU nodes<br/>- AI workloads need predictable capacity<br/>- Multi‑region deployments reduce risk | - Pre‑warm GPU node pools<br/>- Deploy clusters in multiple regions<br/>- Use Front Door to route to nearest available model | - Predictable performance<br/>- Faster model adoption<br/>- Reduced capacity shortages<br/>- Better global coverage | - GPU shortages<br/>- Slow scaling<br/>- Regional capacity constraints<br/>- Inability to deploy new AI models quickly |

## Best practices 

- Cluster Size & Node Pools
  - Use `Virtual Nodes or Burstable VMs (B-series) for cost efficiency.`
  - `Spot instances for non-critical workloads.`
- Autoscaling: Enable `Cluster Autoscaler to scale nodes dynamically.`
- Container Registry: Use Azure Container Registry `(ACR) with geo-replication only if needed.`
- Networking Costs: Minimize cross-region traffic;` keep AKS and app services in same region.`
- Reserved Instances: For predictable workloads, `reserve VMs for 1–3 years to save up to ~57%.`

| Area | Technical Best Practice (Azure‑focused) | Question to Ask | Example Response Back |
|------|------------------------------------------|-----------------|-----------------------|
| **Deployment Strategy** | Use Kubernetes `Deployment` with `RollingUpdate` strategy. Configure `maxSurge` and `maxUnavailable`. Integrate with **Azure DevOps Pipelines** or **GitHub Actions** for controlled rollout. | How are your rolling update parameters set, and which CI/CD tool applies them? | “We use Azure DevOps Pipelines with `maxSurge=1` and `maxUnavailable=0` so new pods come online before old ones terminate.” |
| **CI/CD Integration** | Use **Azure DevOps Release Pipelines** or **GitHub Actions** with AKS deployment tasks. Leverage staged rollouts and approvals. | How do you prevent breaking changes from being applied instantly? | “Our pipeline uses staged environments with approvals; manifests are applied progressively to AKS.” |
| **Ingress / Gateway API** | Use **Azure Application Gateway Ingress Controller (AGIC)** or Gateway API. Ensures traffic only routes to pods marked `Ready`. Supports path/host routing and TLS termination. | How do you guarantee traffic is only routed to healthy pods? | “AGIC integrates with Kubernetes Services; pods must pass readiness probes before being added to traffic.” |
| **Readiness Probes** | Implement readiness probes that check actual dependencies (DB, cache, external APIs). Example: HTTP GET `/health/ready`. | What does your readiness probe validate? | “Our probe checks DB connectivity and cache warm‑up, not just process start.” |
| **Liveness Probes** | Lightweight probes to restart stuck pods. Example: HTTP GET `/health/live`. | How do you detect pods that are alive but stuck? | “We use a liveness probe hitting `/health/live`; if it fails, Kubernetes restarts the pod.” |
| **Replica Counts** | Maintain ≥3 replicas for production workloads. Use **Azure Kubernetes Autoscaler (Cluster Autoscaler)** and **Horizontal Pod Autoscaler (HPA)** for scaling. | How many replicas do you run during rollouts? | “We run 3–5 replicas per service and use HPA to scale based on CPU/memory.” |
| **Graceful Shutdown** | Implement SIGTERM handlers in apps. Configure `terminationGracePeriodSeconds` (20–60s typical). Use **Azure Load Balancer connection draining** to avoid dropped requests. | How do you drain in‑flight requests when pods terminate? | “We use graceful shutdown hooks and set `terminationGracePeriodSeconds=30`; Azure LB drains connections.” |
| **Automatic Rollback** | Kubernetes halts rollout if new pods fail readiness. Use `progressDeadlineSeconds`. Monitor with **Azure Monitor for Containers** and **Application Insights**. | What happens if new pods fail readiness checks during rollout? | “The rollout halts automatically; existing replicas keep serving traffic until we fix the issue.” |
| **Observability** | Use **Azure Monitor**, **Log Analytics**, and **Application Insights** for rollout health, probe failures, and traffic routing. | How do you track rollout health across APIM, Ingress, and pods? | “We use Azure Monitor for cluster metrics and App Insights for app telemetry, tied together with dashboards.” |
| **Resiliency** | Ensure multi‑region failover with **Azure Front Door** + APIM health probes. | How do you handle failover if one AKS cluster goes down mid‑deployment? | “Front Door detects unhealthy regions and reroutes traffic; APIM policies ensure fallback routing.” |

> [!TIP]
> - **Azure DevOps Pipelines or GitHub Actions** for declarative, progressive deployments, combined with AGIC for ingress and Azure Monitor for observability.
> - **AGIC (Application Gateway Ingress Controller)** or Gateway API ensures traffic routing is Azure‑native.
> - **Azure Monitor + App Insights** provide observability across rollout stages.
> - **Front Door + APIM** give global resiliency and health‑based routing.  

## FAQ 

1. Do I need to rewrite my application? `R/ Usually **no**. If your app already runs in containers, the main changes are:`
    - Converting **docker-compose.yml** into **Kubernetes manifests** or **Helm charts**.
    - Externalizing configuration into ConfigMaps/Secrets.
    - Ensuring containers are stateless.

> The application code rarely needs modification unless it relies on App Service‑specific features.

2. How do I migrate my docker-compose setup to Kubernetes? `R/ Typical mapping:`
    - `services:` → Kubernetes Deployments + Services  
    - `volumes:` → PersistentVolumeClaims  
    - `environment:` → ConfigMaps + Secrets  
    - `ports:` → Container ports + Ingress  
> Tools that help:
    - **kompose** (automatic conversion)
    - **Helm** (recommended for production)
    - **Draft** or **Bridge to Kubernetes** for dev workflows

3. What about environment variables and secrets? `R/ In App Service, env vars are injected automatically. In AKS:`
    - Use **ConfigMaps** for non‑sensitive settings.
    - Use **Secrets** for sensitive values.
    - Use **Azure Key Vault** + CSI driver for secure secret injection.
      
4. How do I expose my application publicly? `R/ In App Service, exposure is automatic. In AKS, you choose:`
    - **Ingress Controller** (NGINX, AGIC, Traefik) — most common  
    - **LoadBalancer Service** — simple but less flexible  
    - **Service Mesh** (Istio, Linkerd) — advanced traffic control  
    
5. How do I handle logging and monitoring? 
`R/`
> - App Service → Application Insights
> - AKS → You can still use App Insights, but most teams add:
    - **Prometheus** for metrics  
    - **Grafana** for dashboards  
    - **Azure Monitor for Containers** for cluster health  
    - **OpenTelemetry** for tracing  
    
6. What about scaling? `R/ AKS gives you more options:`
    - **Horizontal Pod Autoscaler (HPA)**  
    - **KEDA** for event‑driven autoscaling  
    - **Cluster Autoscaler** for node scaling  
    - **Virtual Nodes** for burst workloads  

> This is a major upgrade from App Service’s simpler autoscaling rules.

7. How do I deploy to AKS? `R/ Common approaches:`
    - **Azure DevOps Pipelines** or **GitHub Actions**

> AKS supports more sophisticated deployment strategies than App Service.

8. What are the cost considerations? `R/ AKS can be cheaper or more expensive depending on:`
    - Node size and count  
    - Whether you use spot nodes  
    - Whether you use managed add‑ons  
    - How well you autoscale  

> - App Service is predictable but less flexible.
> - AKS rewards optimization.

9. What are the common migration pitfalls? `R/ Teams often run into:`
    - Missing health probes → pods restart endlessly  
    - Incorrect Ingress configuration → app unreachable  
    - Not externalizing config → containers fail on startup  
    - Over‑provisioning nodes → unnecessary cost  
    - Forgetting persistent storage → data loss  
    - Not setting resource limits → noisy neighbor issues  
    
10. How long does a typical migration take? `R/ Depends on complexity:`
    - **Simple 2–3 container app** → 1–2 weeks  
    - **Medium microservice app** → 4–8 weeks  
    - **Large distributed system** → 3–6 months  

> Most of the time is spent on:
> - Infrastructure setup
> - CI/CD redesign
> - Observability
> - Security and networking  
    
11. Can I run both environments during migration? `R/ Yes, and you should. Common patterns:`
    - **Side‑by‑side testing**  
    - **Blue/green cutover**  
    - **Gradual traffic shifting** via Ingress or Front Door  

> This reduces risk dramatically.

12. What’s the recommended folder structure for AKS deployments? `R/ A clean structure might look like:`

```
/deploy
  /helm
    /app
      values.yaml
      templates/
  /manifests
    deployment.yaml
    service.yaml
    ingress.yaml
/src
  (your application code)
```

13. What Azure services pair well with AKS?
    - **Azure Container Registry (ACR)**  
    - **Azure Key Vault**  
    - **Azure Monitor**  
    - **Azure Front Door**  
    - **Azure Load Testing**  
    - **Azure Files / Azure Disks**  
    - **Azure Service Bus / Event Grid / Event Hubs**  

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
