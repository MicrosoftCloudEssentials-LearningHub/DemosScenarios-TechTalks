# Azure Red Hat OpenShift with Defender - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-22

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

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
