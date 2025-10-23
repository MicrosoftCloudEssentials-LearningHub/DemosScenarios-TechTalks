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





<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
