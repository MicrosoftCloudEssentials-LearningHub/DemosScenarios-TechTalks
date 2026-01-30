# MSFT Foundry IQ \& Control Plane - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

------------------------------------------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is the Microsoft Foundry Control Plane?](https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview?view=foundry)
- [MSFT Docs - What is the Microsoft Foundry Control Plane?](https://github.com/MicrosoftDocs/azure-ai-docs/blob/main/articles/ai-foundry/default/control-plane/overview.md) - GitHub repo
- [Foundry IQ for Multi-Source AI Knowledge Bases](https://techcommunity.microsoft.com/blog/microsoftmechanicsblog/foundry-iq-for-multi-source-ai-knowledge-bases/4474921)
- [Foundry Control Plane: Managing AI agents at scale | BRK202](https://www.youtube.com/watch?v=XjVj_qRwzVg) - YouTube video

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Control Plane](#control-plane)
- [Foundry IQ](#foundry-iq)

</details>

## Control Plane

> The Control Plane is the central management layer that governs how your AI agents operate across an enterprise. It does not execute model inference (that’s the data plane); instead, it provides visibility, governance, and orchestration for everything running in the data plane.
> `Think of it as mission control for your AI ecosystem, where you set policies, monitor performance, and enforce compliance across thousands of agents.` Click here to read more about [Azure control plane and data plane](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane), and [Microsoft Foundry architecture
](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/architecture?view=foundry-classic)

<img width="1007" height="381" alt="image" src="https://github.com/user-attachments/assets/bd7f3cc6-78c1-414c-8952-498c2e12c29e" />

Based on [What is the Microsoft Foundry Control Plane?](https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview?view=foundry)

| **Function**              | **Description**                                                                  | **Example Use Case**                                                                      |
| ------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Fleet-wide Operations** | Centralized management of all AI agents and services across environments.        | Update pricing logic for 500 retail agents in one click; scale agents during peak demand. |
| **Observability**         | Real-time monitoring of performance, cost, latency, and anomalies.               | Detect an agent making ungrounded recommendations and fix before customer impact.         |
| **Governance & Control**  | Apply policies, guardrails, and compliance rules across the fleet.               | Restrict finance agents to approved datasets; block marketing agents from accessing PII.  |
| **Security**              | Identity, access control, and threat protection integrated with Microsoft tools. | Revoke compromised agent credentials instantly using Entra Agent ID and Defender.         |

<img width="1904" height="830" alt="image" src="https://github.com/user-attachments/assets/29dcf372-c5ef-41d1-8d83-1ff44a4c723f" />

> [!NOTE]
> Control Plane ~ Management Layer: `E.g: Air Traffic Control, sets flight paths, monitors planes, enforces rules.`
> - Purpose: Governs, orchestrates, and monitors operations across your AI ecosystem.
> - Activities: Policy enforcement, lifecycle management, observability, security, compliance. <br/>
>   
> Data Plane ~ Execution Layer:  `E.g: The Airplanes, they fly and carry passengers (data/tasks).`
> - Purpose: Runs the actual workloads (model inference, data processing, agent actions).
> - Activities: Executes prompts, retrieves data, performs reasoning tasks.

## Foundry IQ

`Foundry IQ ~ embedded RAG (Retrieval-Augmented Generation) layer for enterprise AI agents.`

> **Foundry IQ** is Microsoft’s **enterprise knowledge layer** designed to power Retrieval-Augmented Generation (RAG) for AI agents. It connects agents to organizational data securely and efficiently, enabling them to retrieve, reason, and respond with grounded context. `Think of it as the “knowledge engine” for your AI ecosystem, where agents can access structured and unstructured data across multiple sources without manual integration.` Click here to read more about [Foundry IQ: Unlocking ubiquitous knowledge for agents](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-iq-unlocking-ubiquitous-knowledge-for-agents/4470812)

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/12d582fe-bd33-4444-8c99-f08194210424" />

> Core Capabilities of Foundry IQ:

| **Capability**                         | **Description**                                                        | **Example Use Case**                                                                            |
| -------------------------------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Unified Data Access**                | Connects to OneLake, SharePoint, Fabric IQ, Snowflake, S3, and more.   | An agent retrieves product specs from SharePoint and pricing from Snowflake in one query.       |
| **Automated Indexing & Vectorization** | Converts enterprise data into searchable embeddings automatically.     | HR documents and product catalogs indexed for semantic search without manual setup.             |
| **Advanced Query Planning**            | Breaks down complex queries into multi-step retrieval tasks.           | A compliance agent queries “latest GDPR policy impact on EU marketing” across multiple sources. |
| **Secure Retrieval**                   | Enforces Purview sensitivity labels and access policies at query time. | Finance agent blocked from accessing confidential HR data during retrieval.                     |
| **Multimodal RAG**                     | Supports text, tables, and structured data for richer grounding.       | AI assistant combines text from policy docs and tables from Excel for a complete answer.        |

<img width="1897" height="833" alt="image" src="https://github.com/user-attachments/assets/1f7b565a-1a28-42c9-b11c-6870fc194e1c" />

> [!NOTE]
> **Foundry IQ ~ Knowledge Layer**: `E.g: A smart library system, agents ask questions, IQ finds the right books and pages instantly.`
> - **Purpose**: Provides unified, secure access to enterprise data for AI agents.
> - **Activities**: Indexing, vectorization, query planning, synthesis, multimodal retrieval. <br/>
>
> **Data Plane Role**:
> - Foundry IQ operates in the **data plane**, serving as the retrieval and grounding engine for agents.
> - It works under governance from the **Control Plane**, which enforces compliance and security.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
