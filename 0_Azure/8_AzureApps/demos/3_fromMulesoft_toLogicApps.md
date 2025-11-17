# From Mulesoft to Azure Logic Apps - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

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

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
