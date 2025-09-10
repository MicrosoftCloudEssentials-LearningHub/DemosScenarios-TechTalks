# Azure DevOps Services vs Azure DevOps Server – Technical Recap

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<img width="1867" height="548" alt="image" src="https://github.com/user-attachments/assets/d7920c93-9c86-4107-89d6-6019fbbd0287" />

From [Pricing for Azure DevOps](https://azure.microsoft.com/en-us/pricing/details/devops/azure-devops-services/)

| Feature                | Azure DevOps Services (Cloud) | Azure DevOps Server (On-Premises) |
|------------------------|-------------------------------|------------------------------------|
| Hosting               | Microsoft-managed cloud       | Self-hosted infrastructure        |
| Cost Model            | Pay-as-you-go                | Licensing + infrastructure        |
| Maintenance           | Automatic updates            | Manual updates and patching       |
| Scalability           | Elastic, global              | Limited by hardware               |
| Security              | Microsoft Entra ID, RBAC     | Full control, custom policies     |
| Integration           | Azure, GitHub, cloud-native  | Legacy systems, custom tools      |
| Offline Use           | Not supported                | Fully supported                   |
| Compliance            | Meets most standards         | Best for strict regulatory needs  |


<details>
<summary><strong>Hosting </strong></summary>

Definition:
- Cloud: Microsoft hosts the entire service stack (web UI, APIs, storage, backups, HA).
- On-Premises: You host the application tier, SQL Server, storage and networking in your environment.

Operational impact:
- Cloud: minimal ops, fast onboarding, dependency on internet and Microsoft availability.
- On-Premises: full control over network, physical access and data locality; requires staff to operate.

Pros / Cons:
- Cloud pros: low operational burden, automatic HA, global endpoints. Cons: less control over maintenance windows, compliance exceptions may apply.
- On-Prem pros: absolute control over network and storage location. Cons: CAPEX and dedicated admin teams.

Checklist if you choose On‑Prem:
- Size SQL Server (IOPS, memory), design backups and DR.
- Plan maintenance windows and staging upgrades.
- Define network segmentation and firewall rules.
</details>

<details>
<summary><strong>Cost Model </strong></summary>

What it means:
- Pay-as-you-go: Ongoing OPEX for users, parallel jobs, hosted minutes and artifact storage.
- Licensing + infrastructure: Upfront server and CAL licenses plus hardware/network costs.

Financial implications:
- Cloud: predictable monthly billing, easier to scale up/down; watch usage spikes like pipeline minutes and artifact storage.
- On‑Prem: higher upfront cost, possible lower long-term marginal cost, but staff & power are recurring.

Optimization tips:
- Use self-hosted agents to reduce hosted pipeline minute costs.
- Audit and reclaim licenses and inactive accounts monthly.
</details>

<details>
<summary><strong>Maintenance </strong></summary>

- Cloud behavior: Microsoft pushes feature updates, security patches and platform improvements continuously. No server maintenance required.
- On‑Prem responsibilities: You must plan upgrades, test migrations, apply security patches to OS/SQL, and maintain backups.

Best practices:
- Cloud: follow Microsoft release notes; test critical pipelines in isolated projects after major changes.
- On‑Prem: maintain a test/staging environment for upgrades and automate backups with restore drills.
  
</details>

<details>
<summary><strong>Scalability </strong></summary>

- Cloud advantages: Elastic compute for hosted agents, storage scaled by the provider, and global endpoints for distributed teams.
- On‑Prem constraints: Scale requires provisioning additional VMs/servers, storage and possibly database sharding/replication.

Capacity planning:
- Cloud: rely on autoscaling and pay-as-you-grow.
- On‑Prem: implement monitoring, capacity reserves and purchase cycles.

</details>

<details>
<summary><strong>Security </strong></summary>

- Cloud controls: Integrates with Microsoft Entra ID: SSO, MFA, Conditional Access and RBAC at organization/project level.
- On‑Prem controls: Use AD, ADFS or custom auth; implement internal SIEM, bespoke firewall rules, HSMs and advanced network segmentation.

Trade-offs:
- Cloud reduces operational security burden but implies a shared responsibility model.
- On‑Prem grants total control but requires mature security ops.

Operational checklist:
- Enforce least privilege, enable MFA, centralize audit logs, and periodically review access.
</details>

<details>
<summary><strong>Integration </strong></summary>

- Cloud strengths: Native connectors to Azure services, GitHub, marketplace extensions, webhooks and SaaS tooling.
- On‑Prem strengths: Direct network access to internal systems (databases, legacy build systems, SCADA), enabling simpler internal integrations.
- Bridging strategies: Use self-hosted agents or secure gateway/proxy patterns to enable hybrid connectivity.

</details>

<details>
<summary><strong>Offline Use </strong></summary>

Explanation:
- Cloud requires internet access to reach Microsoft-managed endpoints; not suitable for strictly air‑gapped environments.
- On‑Prem can be fully offline, supporting builds, releases and artifact storage without external connectivity.

- When to choose On‑Prem: Classified projects, OT/manufacturing environments, or government systems mandating network isolation.
- Operational tips: For air‑gapped On‑Prem, plan internal distribution of updates and secure artifact promotion procedures.

</details>

<details>
<summary><strong>Compliance </strong></summary>

- Cloud compliance:Microsoft maintains many certifications (ISO, SOC, GDPR, HIPAA etc.) and provides attestation packages.
- On‑Prem compliance: Enables physical control, in-country data residency and customized retention/audit policies required by some regulations.
- Decision guidance: Map specific regulatory controls to cloud provider attestations; choose On‑Prem if any required control cannot be satisfied by cloud attestations.

</details>


## Billing Explained

> Even if you're using Microsoft 365 (Office 365), billing for Azure DevOps is handled through an **Azure subscription**. `Why billing goes through Azure`: Azure DevOps Services consumes Azure billing constructs: the organization must be linked to an Azure subscription (owner/billing admin) to pay for paid features, parallel jobs and other billable resources.

Billing Options:

| Billing Type               | Credit Card Required? | Notes                          |
|----------------------------|-----------------------|--------------------------------|
| Pay-As-You-Go             | Yes (by default)      | Can request invoice billing   |
| Enterprise Agreement (EA) | No                    | Invoiced billing              |
| Cloud Solution Provider (CSP) | No                | Partner-managed billing       |
| Invoice Billing (Pay-As-You-Go) | No (after approval) | Requires credit check        |

<details>
<summary><strong>Pay‑As‑You‑Go</strong></summary>

- Description: Standard Azure subscription billing with monthly charges tied to consumption and purchased licenses.
- When to choose: Small organizations, pilots, or projects with variable usage.
- Pros: Quick setup, flexible, integrates with Azure Cost Management.
- Cons: Default requires a credit card; invoice billing requires approval.

Operational tips:
- Use budgets + alerts to prevent surprises.
- Move heavy CI workloads to self‑hosted agents where cost-effective.
- Enable caching and incremental builds to reduce minutes.
</details>

<details>
<summary><strong>Enterprise Agreement (EA)</strong></summary>

- Description: Volume licensing and consolidated invoicing for large organizations.
- When to choose: Large enterprises with predictable spend and procurement processes.
- Benefits: Consolidated invoices, procurement alignment, potential negotiated terms.

</details>

<details>
<summary><strong>Cloud Solution Provider (CSP)</strong></summary>

- Description: Partner-managed billing (billing handled by a CSP).
- When to choose: Organizations that want partner-managed billing, consolidated vendor support or managed services.
- Notes: Simplifies procurement but ties invoicing/support to the partner.
  
</details>

<details>
<summary><strong>Invoice Billing (Pay-As-You-Go → Invoice)</strong></summary>

- Description: Convert Pay‑As‑You‑Go to invoice billing for PO-driven organizations.
- Requirements: Credit checks and Azure support engagement; expect lead time.
- Operational note: Prepare procurement contacts and documentation before requesting conversion.

</details>

Primary cost drivers:
- Paid user licenses beyond free tiers
- Microsoft-hosted pipeline minutes and parallel jobs
- Azure Artifacts storage and retention
- Marketplace paid extensions and premium Test Plans

Billing roles (examples):
- Billing owner: Azure subscription Owner, responsible for payment methods and invoices.  
- Organization billing admin: Azure DevOps organization owner, links org to subscription and purchases organization licenses.

Cost controls & best practices:
- Use self-hosted agents: offload heavy builds to reduce hosted-minute cost.  
- Apply artifact retention policies: delete stale artifacts automatically.
- Assign Stakeholder access for non-devs: reduce paid Basic seats.

</details>


## Free Licenses in Azure DevOps


| Plan               | Users         | Cost              |
|--------------------|---------------|-------------------|
| Basic              | First 5 users | Free              |
| Basic (6+ users)   | Each additional | $6/user/month   |
| Basic + Test Plans | Per user      | $52/user/month    |

- Applies **per organization**, regardless of billing method.
- Includes:
  - Azure Boards
  - Azure Repos
  - Azure Pipelines (1 free Microsoft-hosted job)
  - Azure Artifacts (2 GiB free)


<details>
<summary><strong>Basic (first 5 users free)</strong></summary>

- What it covers: Up to five Basic users are free per organization, full access to core DevOps features.
- When to use: Small teams or initial pilot orgs; use Stakeholder role for non-developer contributors.
- Management tip: Periodically audit active users and reclaim unused Basic seats.

</details>

<details>
<summary><strong>Basic (paid) & Basic + Test Plans </strong></summary>

- Cost control: Assign Stakeholder access where appropriate; use Azure AD groups to manage license assignment.
- Test Plans: Use Basic + Test Plans only for roles that require manual/exploratory testing features; automate tests in pipelines as a lower-cost alternative.

</details>

<img width="1036" height="765" alt="image" src="https://github.com/user-attachments/assets/ae605a5d-1c96-4bd5-9597-d0b05212c61c" />

> Click here to understand more about [Pricing for Azure DevOps](https://azure.microsoft.com/en-us/pricing/details/devops/azure-devops-services/)

## How to Configure Billing

> [!NOTE]
> Azure DevOps and Microsoft 365 can share the same **Microsoft Entra ID tenant**, but billing is **not unified**.

Setup:

1. **Create or use an Azure subscription** (EA, CSP, or Pay-As-You-Go).
2. Go to `https://dev.azure.com/{your-org}`.
3. Navigate to **Organization Settings > Billing**.
4. Click **Set up billing** and select your Azure subscription.
5. Save and confirm.

## Recommended Architecture: GitHub + Azure DevOps

| Component          | Recommended Tool       | Reason                                   |
|--------------------|------------------------|-----------------------------------------|
| Source Code        | GitHub                | Developer familiarity, GitHub Advanced Security |
| CI/CD Pipelines    | Azure Pipelines       | Enterprise-grade workflows, hybrid agents |
| Project Tracking   | Azure Boards          | Agile tools, sprint planning            |
| Dashboards & Reporting | Azure DevOps      | Custom dashboards, work item analytics  |
| Security           | GitHub + Azure DevOps | Secret scanning, RBAC, audit logs       |

> Why GitHub for Repos:
- Rich collaboration features (PRs, reviews)
- GitHub Advanced Security
- Open-source friendliness
- IDE integration (VS Code, Copilot)

<details>
<summary><strong>Why GitHub for Repos</strong></summary>

- Overview: GitHub is built for collaborative Git workflows (PRs, reviews, issues) and excels at developer ergonomics and open-source integration.
- Key benefits:
  - Rich collaboration: PRs, draft PRs, required reviews, inline suggestions and code owners.
  - Security: GitHub Advanced Security (SAST, secret scanning, dependency alerts).
  - Ecosystem: Actions, Marketplace apps, Codespaces and large community libraries.
  - Developer experience: Tight IDE/CLI integration (VS Code, Copilot, GH CLI) and instant dev environments (Codespaces).
- Practical examples:
  - Protect branches with required checks and CODEOWNERS for automatic reviewers.
  - Run code scanning + dependency checks in PR pipelines to block risky merges.
  - Use Actions or external CI to publish artifacts to registries (use LFS for large files).
- Implementation checklist:
  - Define branch protection rules and PR templates.
  - Configure CODEOWNERS and required status checks.
  - Enable GitHub Advanced Security features where available.
  - Decide storage strategy for large binaries (Git LFS or external artifact store).
- Common pitfalls:
  - Storing large binaries directly in Git (use LFS).
  - Missing pre-merge security checks (adds risk).
  - Over-permissive merge policies or no CODEOWNERS (reduces review quality).
</details>


> Why Azure DevOps for Pipelines & Boards:
- Multi-stage CI/CD
- Kanban boards and work item tracking
- Test plans and artifacts
- Enterprise integration with Azure

<details>
<summary><strong>Why Azure DevOps for Pipelines & Boards</strong></summary>

- Overview: Azure DevOps Pipelines + Boards provide enterprise-grade CI/CD orchestration and end-to-end traceability from backlog to release.
- Key benefits:
  - Multi-stage CI/CD: YAML pipelines, artifact promotion, approvals and release gates.
  - Hybrid agent model: Microsoft-hosted agents for low ops and self-hosted agents inside your network for sensitive workloads.
  - Traceability: Link work items → commits → builds → releases for audit and reporting.
  - Test & artifacts: Integrated Test Plans and Azure Artifacts with retention controls.
- Practical examples:
  - Implement a multi-stage YAML pipeline that promotes an artifact dev → staging → prod with approval gates.
  - Deploy self-hosted agent pools inside a VNet to access internal DBs or private registries.
  - Use Azure Boards to link backlog items to PRs and pipeline runs for release notes and compliance evidence.
- Implementation checklist:
  - Store pipeline YAML in repo and enable pipeline protections.
  - Design environments and approval gates for production rollouts.
  - Choose agent strategy (hosted vs self-hosted) and size pools to match concurrency needs.
  - Integrate secrets with Azure Key Vault and grant pipelines least privilege.
- Common pitfalls:
  - Not monitoring hosted-agent minutes (unexpected costs).
  - Weak environment gating causing unsafe promotions.
  - Failing to link work items to commits/PRs (loses traceability).

## Use Case Matrix

| Use Case            | Azure DevOps Services | Azure DevOps Server |
|---------------------|-----------------------|---------------------|
| Small Agile Teams   |  Supported          |  Overkill         |
| Global Collaboration|  Supported          |  Requires VPN     |
| CI/CD Pipelines     |  Microsoft-hosted agents |  Self-hosted agents |
| Azure Integration   |  Seamless           |  Manual setup     |
| GitHub Integration  |  Native             |  Manual           |
| Compliance Needs    |  Most standards     |  Full control      |
| Offline Development |  Not supported      |  Ideal             |
| Legacy Systems      |  Limited           |  Easier integration |
| Custom Security     |  Entra ID only      |  Full control      |
| Cost Management     |  Elastic           |  Upfront investment |

<details>
<summary><strong>What "Full control" means (expand)</strong></summary>

- Definition: Full control covers complete ownership of infrastructure, identity providers, physical access, logging, retention and custom security appliances (HSMs, firewalls). It includes the ability to:
  - Enforce network isolation and bespoke firewall rules.
  - Use custom or legacy identity systems (AD/ADFS) and on-prem HSMs.
  - Retain raw logs, run in-house SIEMs, and store data entirely within a specific geographic location.

- Implications:
  - Higher operational cost and staffing needs.
  - Greater ability to meet strict regulatory or contractual requirements.
  - Requires formal processes for backups, DR, patching and audit evidence.

</details>

<details>
<summary><strong>What "Entra ID only" means</strong></summary>

- Definition: The cloud Service relies on Microsoft Entra ID for authentication/authorization, conditional access and MFA. Custom identity models are limited and must be federated through Entra ID.
- Implication: Simpler central management but less flexibility for legacy auth requirements; use federation if on-prem identity must be preserved.

</details>

<details>
<summary><strong>Offline / Air‑gapped workflows</strong></summary>

- When to choose On‑Prem: Classified projects, OT/manufacturing, or government systems that cannot accept external connectivity.
- Operational checklist for air‑gapped deployments:
  - Plan internal distribution of updates and signed packages.
  - Implement strict artifact promotion and verification processes.
  - Run internal build agents and maintain private artifact registries.
</details>

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1403-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
