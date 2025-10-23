# Migrating from <br/> Multi-container Web Apps to AKS - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

</details>

> [!NOTE]
> If you have any questions or need further clarification, please reach out to your Microsoft account team or contact Microsoft directly: [Microsoft Sales and Support](https://support.microsoft.com/contactus?ContactUsExperienceEntryPointAssetId=S.HP.SMC-HOME) for additional support and guidance, or

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

## Best practices 

- Cluster Size & Node Pools
  - Use `Virtual Nodes or Burstable VMs (B-series) for cost efficiency.`
  - `Spot instances for non-critical workloads.`
- Autoscaling: Enable `Cluster Autoscaler to scale nodes dynamically.`
- Container Registry: Use Azure Container Registry `(ACR) with geo-replication only if needed.`
- Networking Costs: Minimize cross-region traffic;` keep AKS and app services in same region.`
- Reserved Instances: For predictable workloads, `reserve VMs for 1–3 years to save up to ~57%.`

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
