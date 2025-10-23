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

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
