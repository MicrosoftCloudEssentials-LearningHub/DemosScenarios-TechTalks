# Azure Red Hat OpenShift with Defender - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

> [!NOTE]
> If ARO, you can assume Linux by default, but asking is still fair in case they’ve configured Windows worker nodes via WMCO

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
- [Security for the Azure Red Hat OpenShift landing zone accelerator](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/scenarios/app-platform/azure-red-hat-openshift/security)
- [Containers support matrix in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-containers?tabs=azureva%2Cazurert%2Cazurespm%2Cazurecssc%2Cawsnet)
- [Container protection in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction) - overview
- [Defender for Containers architecture](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-architecture?tabs=defender-for-container-arch-aks) - how it works


</details>

> [!IMPORTANT]
> - AKS has tighter native integration with Defender.
> - ARO can feel like a `black box` since you don’t manage the control plane directly.
> - Once ARO is connected via Azure Arc, Defender treats it like any other Arc‑enabled Kubernetes cluster.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d1700211-8536-4b2d-a373-5c1ba953f882" />

From [What is Microsoft Defender for Cloud?](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)

> Cloud Native Application Protection Platform (CNAPP):

<img width="1124" height="741" alt="image" src="https://github.com/user-attachments/assets/40e54bde-d92d-43f0-9933-0fd07cc62f0e" />

From [What is Microsoft Defender for Cloud?](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)

## How it works

> Microsoft Defender for Containers covers Azure Red Hat OpenShift clusters at runtime when they are onboarded via Azure Arc.
> This enables Defender to monitor workloads, detect threats, and provide runtime protection across OpenShift-managed containers.

> [!NOTE]
> The Microsoft Learn page uses AKS (Azure Kubernetes Service) as the example, but the same Defender for Containers architecture applies to any Arc‑enabled Kubernetes cluster,
> including ARO. When ARO is connected through Azure Arc, Defender recognizes it as an Arc‑enabled Kubernetes cluster and manages it just like any other Kubernetes environment.
 
To enable it: `This way, you get both runtime threat detection and image vulnerability scanning for your OpenShift workloads.`
> - Connect your OpenShift cluster to Azure using Azure Arc. Click here to read more about [Use cluster connect to securely connect to Azure Arc-enabled Kubernetes clusters](https://learn.microsoft.com/en-gb/azure/azure-arc/kubernetes/cluster-connect?tabs=azure-cli#service-account-token-authentication-option)
> - Enable Defender for Containers in the Azure portal under Microsoft Defender for Cloud. Click here to read more about [Container protection in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction), and  [Defender for Containers architecture](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-architecture?tabs=defender-for-container-arch-aks)

  <img width="1152" height="1009" alt="image" src="https://github.com/user-attachments/assets/d8d24dd6-e744-436d-9bae-1c51d9597d55" />
  
  
  From [Defender for Containers architecture](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-architecture?tabs=defender-for-container-arch-aks)

> - Deploy the Defender agent (via the Azure Arc extension) to your OpenShift nodes.

  <img width="1872" height="382" alt="image" src="https://github.com/user-attachments/assets/9d50114f-48bc-432f-acff-60702527db9a" />

> - Configure image vulnerability scanning for your container registries (e.g., Azure Container Registry or integrated third-party registries).

## Automating recommendations

> Microsoft Defender for Cloud (and Defender for Containers) is primarily a monitoring, detection, and recommendation engine. `It does not directly “reach into” your ARO (Azure Red Hat OpenShift) or AKS/containers and change configurations by itself. Instead, it surfaces recommendations and alerts, and you can automate actions around them.`

> [!TIP]
> - **Defender does not directly “do actions” inside ARO/containers.**  
> - It provides **recommendations and alerts**, and you can **wire automation** (Azure Policy, Logic Apps, Kubernetes admission controllers) to enforce or remediate those recommendations.  
> - In practice, Defender acts as the **brains** (detect + recommend), while **Policy/Logic Apps/Function Apps/Kubernetes controllers** act as the **hands** (enforce + remediate).  

> [!NOTE]
> The pattern is the same across all Azure resources: Defender monitors + recommends, while Azure Policy and automation tools enforce/remediate.
> The specific enforcement mechanisms differ depending on the resource type (VMs, databases, containers, etc.).

> What You *Can* Do in ARO or Containers: 

1. **Monitoring & Recommendations** Defender for Containers integrates with **ARO** (since ARO is built on OpenShift/Kubernetes). It provides:
    - Vulnerability scanning of container images.
    - Runtime threat detection.
    - Compliance checks (e.g., privileged containers, read-only root filesystem).
    - Recommendations for hardening workloads.
2. **Automated Actions**: Defender itself doesn’t directly enforce changes inside ARO pods or containers. But you can **automate remediation** using:
    - **Azure Policy** → enforce container security settings (e.g., read-only root filesystem, disallow privileged escalation).
    - **Workflow automation (Logic Apps/Function Apps)** → trigger scripts or actions when Defender raises an alert.
    - **Kubernetes admission controllers / Gatekeeper** → enforce policies at deployment time, often aligned with Defender’s recommendations.
3. **Examples of Automation**: 
   - **ARO / AKS cluster hardening:** Automatically block deployments that violate Defender recommendations (via Azure Policy + Gatekeeper).
   - **Container image scanning:** If Defender finds a vulnerable image in ACR, trigger a Logic App/Function App to block its deployment or notify DevOps.
   - **Runtime alerts:** If Defender detects suspicious activity in a container, trigger automation to isolate the pod, scale down the deployment, or alert security teams.

> Defender acts as the “brains”, while Policy/Logic Apps/FA act as the “hands” to enforce or remediate.

| **Resource Type** | **Defender Role** | **Typical Recommendations** | **Automation / Enforcement Options** |
|-------------------|-------------------|-----------------------------|--------------------------------------|
| **Virtual Machines (VMs)** | Monitors OS vulnerabilities, malware, insecure configurations | Apply missing patches, enable endpoint protection, restrict open ports | Azure Policy for secure baseline; Logic Apps/FA to trigger patching scripts; Azure Update Management |
| **Databases (SQL, Cosmos DB, etc.)** | Detects weak authentication, insecure connections, excessive permissions | Enforce TLS, enable auditing, restrict firewall rules | Azure Policy to enforce TLS; Logic Apps/FA to rotate keys or alert DB admins |
| **Storage Accounts** | Identifies public access, missing encryption, insecure shared keys | Require private endpoints, enable encryption, disable anonymous access | Azure Policy to block public access; Logic Apps/FA to disable insecure settings |
| **AKS / ARO / Containers** | Scans images, detects runtime threats, checks pod security | Disallow privileged containers, enforce read-only root filesystem, scan images for CVEs | Azure Policy + Gatekeeper for enforcement; Logic Apps/FA to block deployments or notify DevOps |
| **App Services (Web Apps, Functions)** | Monitors SSL/TLS, outdated frameworks, insecure configurations | Require HTTPS-only, update runtime versions, restrict CORS | Azure Policy to enforce HTTPS; Logic Apps/FA to notify developers |
| **Key Vault** | Detects excessive access permissions, missing logging | Enforce RBAC, enable logging, rotate secrets | Azure Policy to enforce RBAC; Logic Apps/FA to trigger secret rotation |
| **Networking (NSGs, Firewalls)** | Detects overly permissive rules, insecure endpoints | Restrict inbound rules, enforce segmentation, enable DDoS protection | Azure Policy to block insecure NSG rules; Logic Apps/FA to auto-close risky ports |
| **Azure Container Registry (ACR)** | Scans images for vulnerabilities | Block vulnerable images, enforce signed images | Policy to enforce image scanning; Logic Apps/FA to prevent deployment of non-compliant images |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
