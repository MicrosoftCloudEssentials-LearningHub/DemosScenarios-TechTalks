# From Mulesoft to Azure Logic Apps - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

> - **Cost Flexibility & Cloud-Native Model**: Logic Apps offers `pay-per-use (Consumption) or predictable pricing (Standard).` No heavy upfront licensing, ideal for scaling Manhattan Active integrations and EDI flows.
> - **Enterprise-Grade EDI/B2B Support**: Built-in `AS2, X12, EDIFACT actions with Integration Account Premium (unlimited artifacts, VNET support).` Plus `lossless B2B tracking via Azure Data Explorer for compliance.`
> - **Hybrid & Multicloud Ready**: APIM self-hosted gateway can run near `Manhattan on GCP while keeping governance centralized in Azure`, reducing `latency and egress costs.`
> - **Developer Productivity & Automation**: Visual workflow designer, 400+ connectors, `CI/CD with Azure DevOps/GitHub Actions`, and `Infrastructure-as-Code support.`

https://github.com/user-attachments/assets/14f21262-a153-4a8b-880e-5a53ced605f6

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is Azure Service Bus?](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)
- [Storage queues and Service Bus queues - compared and contrasted](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)

</details>

## What is Manhattan Active platform?

> [Manhattan Active](https://www.manh.com/en-in/our-solutions/manhattan-active-platform) is a cloud native `SaaS platform`, and it is always hosted by Manhattan Associates, `you do not self-host it on your own infrastructure.` Here’s the key detail:

<details>
<summary><b> To read more about it  </b> (Click to expand)</summary>

Deployment model:
> - Manhattan Active runs on Google Cloud Platform (GCP) in a multi-tenant architecture.
> - It’s delivered as a `managed service by Manhattan Associates, customers do not install or manage servers.`


What you control:
> - You `configure integrations, APIs, and extensions through Manhattan’s provided tools.`
> - You `cannot move Manhattan Active to Azure or on-prem; instead, you integrate with it via REST APIs and event streams.`

Implication for your project:
> - Your `integration layer (Azure Logic Apps, APIM, etc.) will connect to Manhattan Active over secure HTTPS endpoints.`
> - If you need low latency or private networking, you can use `APIM self-hosted gateway near Manhattan’s GCP region or set up private connectivity options Manhattan offers (usually via VPN or private link equivalents).`

</details>

<img width="910" height="537" alt="image" src="https://github.com/user-attachments/assets/88056868-4236-491c-bba0-27883b5c4809" />

From [ MANHATTAN ACTIVE® PLATFORM TECHNOLOGY](https://assets-global.website-files.com/609ce44d3dfdab98b5019cf9/61435ff88db5d62c6fd81e6b_MANHATTANACTIVEPLATFORMTECHNOLOGY.pdf)

## Integration with Manhattan Active platform 

> Azure Logic Apps doesn’t have a native connector for Manhattan Active, but they `integrate very well because Manhattan Active is API first and exposes thousands of RESTful endpoints`
>  for WMS, TMS, and Supply Chain Planning:
> - Manhattan Active platform provides `REST APIs (JSON over HTTPS) for all its microservices.`
> - Logic Apps can call these APIs using:
>   - HTTP `action (built-in) for GET/POST/PUT calls.`
>   - Custom `connector if you want reusable Manhattan-specific actions.`
> - For authentication, `Manhattan typically uses OAuth 2.0 or API keys, which Logic Apps supports out of the box.`

> [!TIP]
> - Manhattan Active’s `API-first architecture means any system that can make secure HTTP calls can integrate.`
> - Logic Apps `adds workflow orchestration, error handling, retry policies, and built-in connectors for other systems (ERP, CRM, EDI).`

Event-Driven Patterns:
> - Manhattan Active supports `asynchronous messaging via Google Pub/Sub.`
> - Logic Apps `can subscribe to events by:`
>   - Using [Azure Event Grid](https://learn.microsoft.com/en-us/azure/event-grid/overview) or [Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) as intermediaries.
>   - Building a webhook endpoint in Logic Apps to receive Manhattan notifications.

| Event Grid | Services Bus |
| ---- | ----- | 
| <img width="1002" height="186" alt="image" src="https://github.com/user-attachments/assets/6782e350-3d31-4d09-9011-5fdcebcbebe9" /> | <img width="780" height="137" alt="image" src="https://github.com/user-attachments/assets/18e7dd1e-d9e6-4d15-80c8-2465c128a7b5" /> |


Common Use Cases:

<details>
<summary><b> To read more about it  </b> (Click to expand)</summary>

> - Order orchestration: Logic Apps `can call Manhattan APIs to create or update orders.`
> - Shipment updates: Trigger Logic Apps `when Manhattan sends status changes.`
> - Inventory sync: Periodically `poll Manhattan APIs or react to events for stock updates.`
> - EDI ( Electronic Data Interchange) flows: Logic Apps can transform data from Manhattan into X12/EDIFACT for trading partners using Integration Account. `Refer to the automated exchange of business documents between
> organizations using Electronic Data Interchange (EDI) standards. Instead of sending PDFs or emails, companies use structured formats like X12 or EDIFACT to communicate orders, invoices, shipment notices, etc.`

</details>

What is EDI: 

`EDI flows are the backbone for B2B communication in supply chain, ensuring standardized, automated document exchange between systems and trading partners.`

<details>
<summary><b> What EDI Flows Are?  </b> (Click to expand)</summary>

An **EDI flow** is the end-to-end process of:
1.  **Receiving or sending an EDI message** (e.g., a purchase order in X12 850 format).
2.  **Validating and transforming** the message into your internal system format (JSON, XML, etc.).
3.  **Acknowledging** receipt (e.g., sending a 997 Functional Acknowledgment).
4.  **Routing** the message to the right system (ERP, WMS, TMS).
5.  **Tracking and logging** for compliance.

> Common EDI Document Types:

-  **850** – Purchase Order
-  **855** – Purchase Order Acknowledgment
-  **856** – Advance Ship Notice
-  **810** – Invoice

> Why It Matters for Manhattan Active

- Your carriers, suppliers, and customers often require EDI for **orders, shipments, invoices**.
- Manhattan Active handles internal processes via APIs, but external partners may still expect EDI.
- Logic Apps (with **Integration Account**) can:
  - Convert JSON from Manhattan APIs → X12/EDIFACT for partners.
  - Handle **AS2/SFTP** transport for secure exchange.
  - Manage acknowledgments and batching.

</details>

## Migration from MuleSoft to Azure Logic Apps

> There’s `no “one-click” migration from MuleSoft to Azure Logic Apps because they are fundamentally different platforms,` but you can make the process easier with a structured approach and some automation. Here’s how:

### Inventory & Assessment

~~~mermaid
flowchart LR
    A[Export MuleSoft assets] --> B[Identify]
    B --> C[Classify flows]
~~~~

- Export MuleSoft assets (flows, APIs, DataWeave scripts).
- Identify:
  - **API endpoints** (Manhattan Active, ERP, portals).
  - **Transformations** (JSON ↔ XML ↔ EDI).
  - **Protocols** (HTTP, AS2, SFTP).
- Classify flows into **orchestration**, **API gateway**, and **B2B/EDI**.

### Mapping MuleSoft Components to Azure

| MuleSoft Component        | Azure Equivalent                                     |
| ------------------------- | ---------------------------------------------------- |
| Flows (orchestration)     | **Logic Apps workflows**                             |
| API Gateway               | **Azure API Management (APIM)**                      |
| DataWeave transformations | **Logic Apps inline actions** or **Azure Functions** |
| EDI connectors            | **Logic Apps + Integration Account**                 |

<details>
<summary><b>Flows (orchestration) → Azure Logic Apps workflows</b> (Click to expand)</summary>

- When you migrate a Mule **flow** to Azure, the natural destination is a **Logic Apps (Standard)** workflow because `it gives you stateful or stateless execution,` robust scopes with retries/compensation, parallel branches, and debatching, `so you preserve the control‑flow semantics you rely on while gaining cloud‑native scale.`
- We recommend **Logic Apps Standard (single‑tenant)** rather than Consumption for Manhattan‑grade integrations **because** Standard runs on dedicated compute, supports **VNET integration and Private Endpoints** for fully private inbound/outbound traffic, and hosts **built‑in connectors in‑process** for lower latency—critical when you’re orchestrating many REST calls to Manhattan Active and back‑office systems.
  - [Differences between Standard single-tenant logic apps versus Consumption multitenant logic apps](https://learn.microsoft.com/en-us/azure/logic-apps/single-tenant-overview-compare)
  - [Secure traffic between Standard logic apps and Azure virtual networks using private endpoints](https://learn.microsoft.com/en-us/azure/logic-apps/secure-single-tenant-workflow-virtual-network-private-endpoint)
- This choice also sets you up for sustained throughput: `you can scale vertically (WS1–WS3 SKUs) and horizontally (instances/burst),` tune trigger batch sizes, and exploit high‑throughput patterns when ingesting from **Service Bus** or **Event Hubs**. Some guidance about Logic Apps Standard handling sustained high‑rate event and message processing when sized and tuned correctly—exactly the profile you’ll see during cutover waves or seasonal peaks.
  - [Scaling Logic App Standard for High Throughput Scenarios](https://techcommunity.microsoft.com/blog/integrationsonazureblog/scaling-logic-app-standard-for-high-throughput-scenarios/3866731)
  - [Scaling Logic Apps Standard – Sustained Message Processing System](https://techcommunity.microsoft.com/blog/integrationsonazureblog/scaling-logic-apps-standard-%E2%80%93-sustained-message-processing-system/4339043)
- Manhattan Active is **API‑first (REST/JSON)** and also supports asynchronous delivery via queues; your orchestration will frequently mix HTTP calls with message/event triggers. Logic Apps fits that pattern natively, `and you can pick the right Azure backbone` (**Service Bus** for durable commands/workflows, **Event Grid** for light event fan‑out, **Event Hubs** for streaming—without bending the workflow model). `We prefer this decoupling` **because** it `keeps business logic readable in the workflow while letting the right messaging service do the heavy lifting.`
  - [Developer Manhattan Active Documentation - Enterprise Integration: Async vs Sync](https://developer.manh.com/docs/concept-guides/enterprise-integration/)
  - [Choose between Azure messaging services - Event Grid, Event Hubs, and Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/compare-messaging-services)

</details>

<details>
<summary><b>API Gateway → Azure API Management (APIM)</b> (Click to expand)</summary>

- When you migrate Mule’s **API Manager/Flex Gateway**, the natural Azure equivalent is **API Management (APIM)** because `it provides full API lifecycle management, policy enforcement, and a developer portal`, so you maintain governance while modernizing for cloud-native scale.
- We recommend **APIM with self-hosted gateway** for Manhattan integrations **because** Manhattan Active runs on GCP, and placing the gateway close to Manhattan reduces latency and egress costs while keeping a single control plane in Azure. [Self-hosted gateway overview](https://learn.microsoft.com/en-us/azure/api-management/self-hosted-gateway-overview)
- APIM gives you strong **security and policy control**: `validate OAuth2/OIDC/JWT tokens, enforce mTLS, apply rate limits and quotas, and transform requests/responses` at the edge, so all Manhattan-facing calls and partner-facing APIs follow consistent governance.
- For cost and scale, APIM **v2 tiers** (Basic, Standard, Premium) include predictable request quotas and SLAs; Premium adds VNET and multi-region HA. `We recommend sizing with the Azure calculator` to avoid surprises as traffic grows. [API Management pricing tiers](https://learn.microsoft.com/en-us/azure/api-management/api-management-features)
- Why this matters for Manhattan: `Manhattan Active exposes thousands of REST APIs` for WMS, TMS, and Planning. APIM acts as a secure façade, centralizing auth and throttling, while Logic Apps handle orchestration behind it. [Manhattan Active Developer Docs](https://developer.manh.com/docs/concept-guides/enterprise-integration/)

</details>

<details>
<summary><b>DataWeave transformations → Logic Apps inline actions or Azure Functions</b> (Click to expand)</summary>

- Mule’s **DataWeave** maps become **Logic Apps inline actions** (Compose, Liquid templates, XML/JSON transforms) or **Azure Functions** for heavy transformations. `We split this way so orchestration stays clean and complex logic runs in scalable code`.
- We recommend **Liquid templates for JSON/XML** and **Functions for CPU-heavy or reusable mappings** **because** Functions can scale elastically and be tested independently, reducing workflow complexity and improving maintainability.
  - [Limits and configuration reference for Azure Logic Apps](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-limits-and-config)
  - [What is Azure Functions?](https://learn.microsoft.com/en-us/azure/azure-functions/functions-overview)
- For validation, enforce **JSON Schema/XSD** inside Logic Apps and contracts at APIM. `Failing early at the gateway saves runtime cost and improves security posture`.
- Why this matters for Manhattan: `Most flows are JSON-to-JSON between Manhattan and your ERP`, and when crossing to EDI, you’ll hand off to the Integration Account layer, keeping boundaries clean and performance predictable. [Manhattan Active Integration Concepts](https://developer.manh.com/docs/concept-guides/enterprise-integration/)

</details>

<details>
<summary><b>EDI connectors → Logic Apps + Integration Account (Premium)</b> (Click to expand)</summary>

- Mule’s **EDI/Partner Manager** maps to **Logic Apps Standard + Integration Account (Premium)** because `it supports AS2, X12, EDIFACT natively, handles batching and acknowledgments, and scales without artifact limits`.
-  We recommend **Integration Account Premium** **because** it is GA with **unlimited partners, agreements, schemas**, supports **VNET isolation**, and offers **Availability Zones** for enterprise resilience. [B2B enterprise integration workflows with Azure Logic Apps and Enterprise Integration Pack](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-overview)
- For compliance, enable **B2B tracking to Azure Data Explorer (ADX)**. `This gives lossless, queryable telemetry for MDNs, 997s, and failures`, far better than raw logs, and supports Power BI dashboards for SLA reporting.
- Why this matters for Manhattan: `Manhattan Active is API-first, but carriers and suppliers still require EDI`. Logic Apps bridges JSON from Manhattan APIs to X12/EDIFACT for partners, handles AS2/SFTP transport, and manages acknowledgments, all without a separate B2B platform. [Manhattan Active Integration Guide](https://developer.manh.com/docs/concept-guides/enterprise-integration/)

</details>


### Migration Accelerators

> **Export specs**: MuleSoft APIs are often documented in **RAML/OpenAPI** → import into **APIM**.

<details>
<summary>(Click to expand)</summary>

- **Why:** Migrating APIs from MuleSoft to Azure requires preserving contracts, documentation, and governance. MuleSoft APIs are often defined in **RAML** or **OpenAPI**, which APIM natively supports for import.
- **How:**
    - Export your MuleSoft API definition (RAML or OAS).
    - Convert **RAML → OpenAPI** using tools like MuleSoft CLI.
    - Import the OpenAPI spec into **Azure API Management**:
        - In APIM, go to **APIs → Add API → OpenAPI**.
        - Upload the spec or provide a URL.
    - Apply **policies** (rate limiting, JWT validation, mTLS) and configure **products** for subscription management.
- **Best Practices:**
    - Validate the spec for completeness (operations, response codes, examples).
    - Use **versioning** in APIM to manage future changes.
    - Automate import via **ARM/Bicep templates** or **APIM DevOps toolkit** for consistency across environments. [Tutorial: Import and publish your first API](https://learn.microsoft.com/en-us/azure/api-management/import-and-publish)

</details>

> **Reusable schemas**: X12/EDIFACT schemas can be reused in **Integration Account**.

<details>
<summary>(Click to expand)</summary>

- **Why:** EDI flows rely on **X12/EDIFACT schemas** for validation and transformation. Reusing these schemas avoids rework and ensures compliance with trading partner requirements.
- **How:**
    - Export schemas from MuleSoft (usually stored in DataWeave or connector configs).
    - Upload schemas into **Integration Account** in Azure:
        - Navigate to **Integration Account → Schemas → Add**.
        - Provide schema name, type (X12/EDIFACT), and upload the .xsd or .edi file.
    - Associate schemas with **maps** and **agreements** for partners.
- **Best Practices:**
    - Store schemas in **source control** (GitHub/Azure DevOps) for versioning.
    - Use **naming conventions** for transaction sets (e.g., X12\_850\_v4010).
    - Validate schema compatibility with Logic Apps built-in EDI actions.
    
</details>

>  **Automation**: Use **Azure DevOps/GitHub Actions** for CI/CD pipelines to deploy Logic Apps/APIM.

<details>
<summary>(Click to expand)</summary>


- **Why:** Manual deployments are error-prone. CI/CD ensures consistency, traceability, and faster releases across Dev, Test, and Prod.
- **How:**
    - Use **Azure DevOps** or **GitHub Actions** pipelines:
        - Define Logic Apps, APIM, Integration Account in **ARM/Bicep/Terraform** templates.
        - Create pipeline stages: Build → Validate → Deploy → Smoke Test.
        - Secure secrets via **Azure Key Vault** integration.
    - For Logic Apps:
        - Export workflows as JSON templates.
        - Parameterize environment-specific values (connections, endpoints).
    - For APIM:
        - Use **APIM DevOps toolkit** to extract and deploy APIs, policies, and products.
- **Best Practices:**
    - Implement **blue-green or canary deployments** for critical APIs.
    - Add **automated tests** for workflows and API endpoints.
    - Monitor deployments with **Azure Monitor** and set alerts for failures.
    - [Overview: Automate deployment for Azure Logic Apps by using Azure Resource Manager templates](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-azure-resource-manager-templates-overview)

</details>

### Phased Migration

- Start with **new integrations** (Manhattan Active APIs, EDI flows).
- Gradually **retire MuleSoft flows** as you replicate them in Logic Apps.
- Use **APIM self-hosted gateway** near Manhattan Active for hybrid coexistence during transition.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
