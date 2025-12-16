# Azure Red Hat OpenShift - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

`Red Hat OpenShift is built on open source technologies, but the commercial Red Hat OpenShift product itself is not fully open source. Instead, its upstream community project called OKD (Origin Kubernetes Distribution) is the open source version that powers Red Hat OpenShift`

> Red Hat OpenShift is a Kubernetes-based container platform, and Azure Red Hat OpenShift (ARO) is the same OpenShift technology but offered as a fully managed service running on Azure infrastructure, jointly operated and supported by Microsoft and Red Hat.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Azure Red Hat OpenShift](https://learn.microsoft.com/en-us/azure/openshift/intro-openshift)
- [What is Azure Kubernetes Service (AKS)?](https://learn.microsoft.com/en-us/azure/aks/what-is-aks)
- [Microsoft Azure Red Hat OpenShift explained](https://cloud.redhat.com/learn/microsoft-azure-red-hat-openshift-explained)
- [Azure Red Hat OpenShift documentation](https://learn.microsoft.com/en-us/azure/openshift/)
- [Core concepts for Azure Kubernetes Service (AKS)](https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts)
- [Red Hat OpenShift vs. Kubernetes](https://www.redhat.com/en/technologies/cloud-computing/openshift/red-hat-openshift-kubernetes)
- [Azure Red Hat OpenShift pricing](https://azure.microsoft.com/en-us/pricing/details/openshift/)
- [Azure Kubernetes Service (AKS) pricing](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/)
- [Four benefits from Red Hat and Microsoft for Azure Red Hat OpenShift customers](https://www.redhat.com/en/blog/four-benefits-red-hat-and-microsoft-azure-red-hat-openshift-customers)
- [OpenShift](https://github.com/openshift) - GH org
- [Red Hat OpenShift Ecosystem](https://github.com/redhat-openshift-ecosystem)  - GH org

</details>


<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [What is Red Hat OpenShift?](#what-is-red-hat-openshift)
- [Core Advantages of ARO](#core-advantages-of-aro)
- [Key Differences Between ARO and AKS](#key-differences-between-aro-and-aks)

</details>

## What is Red Hat OpenShift?

`Running Kubernetes in production requires many tools (registries, networking, logging, monitoring). Azure Red Hat OpenShift bundles these into one platform, reducing operational overhead`

> - Container platform: OpenShift is a family of containerization products built by Red Hat. Its core product, `OpenShift Container Platform, is based on Kubernetes and Red Hat Enterprise Linux, providing orchestration, scaling, and management of containerized applications.`
> - Developer-friendly: It `simplifies building, deploying, and scaling applications in containers, with integrated CI/CD pipelines, developer tools, and security features.`
> - Hybrid cloud:` OpenShift can run on-premises, in private clouds, or on public clouds, giving flexibility to enterprises.`

## Core Advantages of ARO

`Azure Red Hat OpenShift`

- Fully managed clusters: Microsoft and Red Hat jointly operate ARO, `handling upgrades, patching, and infrastructure so customers focus on apps.`
- Enterprise security and compliance: Built-in `Entra ID (Azure Active Directory) integration, role-based access control, and compliance with standards like ISO, SOC, HIPAA, and GDPR.`
- Hybrid cloud flexibility: Seamless `extension to on-premises or edge environments using Azure Arc, enabling consistent management across environments.`
- Integrated monitoring and logging: Azure Monitor and Log Analytics `provide observability into workloads, clusters, and applications.`
- Global availability: Azure’s worldwide `datacenter footprint ensures low latency, disaster recovery, and compliance with local regulations.`

> Integration Benefits with Azure: 
> - Identity and access management: ARO integrates with Azure  Entra ID (Azure Active Directory) for `single sign-on and secure role-based access.`
> - DevOps and CI/CD pipelines: `Native integration with GitHub Actions, Azure DevOps, and Jenkins accelerates application delivery.`
> - Networking and storage: `Azure Virtual Network, Load Balancer, and Blob Storage integrate directly with OpenShift workloads.`
> - Security services: Azure Security Center and Defender for Cloud extend `protection to containerized workloads.`
> - Data and AI services: Applications running on `ARO can easily consume Azure services like Cosmos DB, Azure AI, and Synapse Analytics.`

## Key Differences Between ARO and AKS

> - **AKS** is cheaper and simpler if you want raw Kubernetes with Azure integrations. 

  <img width="750" alt="image" src="https://github.com/user-attachments/assets/3da60e89-3ce3-4752-9b29-ac5802d8461c" />
  
  > Cluster:
  
  <img width="1947" height="662" alt="image" src="https://github.com/user-attachments/assets/6fd33c2b-47d1-4bb3-b021-2fa86e868383" />

  > Nodes: 
  <img width="1561" height="578" alt="image" src="https://github.com/user-attachments/assets/d9c22fb5-d8e7-4270-8bce-f7ef3b4b23b0" />

  > Namespaces:
  <img width="500" height="380" alt="image" src="https://github.com/user-attachments/assets/5e22e14e-3af3-475b-8f0d-abecee0d50b7" />
  
>- **ARO** is more expensive but delivers **enterprise‑grade features, compliance, and reduced operational overhead**, ideal for regulated industries and large enterprises.  

| **Aspect** | **Azure Red Hat OpenShift (ARO)** | **Azure Kubernetes Service (AKS)** |
|------------|-----------------------------------|------------------------------------|
| **Platform** | Kubernetes + OpenShift enterprise features | Vanilla Kubernetes |
| **Management** | Fully managed by Microsoft + Red Hat (patching, upgrades, infra) | Control plane managed by Microsoft; worker nodes managed by you |
| **Operating System** | Red Hat Enterprise Linux CoreOS (hardened, auto‑updated) | Azure Linux or Windows Server nodes |
| **Developer Tools** | Built‑in CI/CD (Tekton), GitOps (ArgoCD), Source‑to‑Image (S2I), integrated registry | Requires separate setup (Azure DevOps, GitHub Actions, Jenkins, ACR) |
| **Security & Compliance** | Hardened defaults, enterprise certifications (ISO, SOC, HIPAA, GDPR) | Secure but requires manual configuration for compliance |
| **Identity Integration** | Native Azure AD + OpenShift RBAC | Native Azure AD RBAC |
| **Monitoring & Logging** | Prometheus, Grafana, EFK stack + Azure Monitor | Azure Monitor, Log Analytics (add‑ons for Prometheus/Grafana) |
| **Networking** | Azure VNet + OpenShift Service Mesh (Istio‑based) | Azure VNet + Kubernetes ingress controllers |
| **Hybrid Cloud** | Seamless with Azure Arc + Red Hat ACM | Works with Azure Arc, but less opinionated |
| **Support Model** | Joint Microsoft + Red Hat enterprise support | Microsoft support only |
| **Pricing** | Higher (VMs + OpenShift license fee per node) | Lower (VMs only, control plane free) |
| **Best Fit** | Enterprises needing turnkey, compliant, production‑ready Kubernetes | Teams comfortable managing Kubernetes themselves, cost‑sensitive workloads |


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
