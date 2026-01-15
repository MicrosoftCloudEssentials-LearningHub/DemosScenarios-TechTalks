# MSFT Foundry - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-05

------------------------------------------

> Microsoft Foundry is not just a rebrand, it’s a major evolution. `It shifts from model-centric experimentation to agent-centric enterprise AI,
> with unified governance, observability, and developer tooling.` If you used Classic Foundry, expect a more streamlined portal,
> stronger compliance features, and a deeper focus on agents.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is Microsoft Foundry?](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-foundry?view=foundry-classic&utm_source=copilot.com)
- [Microsoft Foundry architecture](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/architecture?view=foundry-classic&utm_source=copilot.com)
- [What is the Microsoft Foundry Control Plane?](https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview?view=foundry&utm_source=copilot.com)
- [Comparing Content Understanding in Microsoft Foundry vs Content Understanding Studio](https://learn.microsoft.com/en-us/azure/ai-services/content-understanding/foundry-vs-content-understanding-studio?utm_source=copilot.com)
- [Foundry Agent Service at Ignite 2025: Simple to Build. Powerful to Deploy. Trusted to Operate.](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-agent-service-at-ignite-2025-simple-to-build-powerful-to-deploy-trusted-/4469788)

</details>

| MSFT Foundry (New) | AI Foundry (Classic) |
| --- | --- | 
| <img width="1901" height="982" alt="image" src="https://github.com/user-attachments/assets/d7195178-8d6d-4681-90f2-8fd273ed95f7" /> | <img width="1893" height="980" alt="image" src="https://github.com/user-attachments/assets/89769a23-376b-4f7e-81aa-e9ea73b0258d" /> | 

## Classic vs. New Foundry

> - Unified AI Platform: Combines `infrastructure, models, agents, and tools under one management layer`
> - Enterprise Ready: `Built-in monitoring, tracing, evaluations, and compliance features`
> - Agent Centric: Designed around `AI agents and workflows rather than just models`
> - Developer-Friendly: Simplifies `project setup, resource management, and SDK/API usage`

`Classic = LLM sandbox` <br/>
`New = Agent platform with enterprise governance`

| Aspect | Foundry (Classic) | Foundry (New) |
|--------|------------------|---------------|
| **Focus** | `LLM deployment & experimentation` → Classic Foundry was designed around large language models. Developers could explore different LLMs, fine‑tune them with custom data, and embed them into applications. It was essentially a sandbox for working with generative AI models, not a full enterprise agent platform. | `Agent-first workflows, governance, observability` → The new Foundry shifts from just hosting LLMs to managing **AI agents** that use LLMs as components. It emphasizes workflows, compliance, monitoring, and enterprise‑scale deployment. Models are still there, but they’re part of a larger agent ecosystem. |
| **Portal Experience** | `Fragmented resource creation` → Users had to separately configure model endpoints, storage, and monitoring. | `Streamlined project creation & unified portal` → One project setup provisions everything needed for agents, models, and observability. |
| **Governance** | `Limited enterprise controls` → Basic access and monitoring, but not deep compliance. | `Full enterprise setup: tracing, monitoring, evaluations` → Governance is built in, with dashboards for performance, compliance, and policy enforcement. |
| **Integration** | `Separate tools for models, apps, infra` → Developers had to stitch together SDKs and services. | `Unified under one platform (agents + models + tools)` → A cohesive environment where agents, models, and data connectors work seamlessly. |
| **Evolution** | `Azure AI Foundry branding` → Focused on LLM experimentation within Azure. | `Microsoft Foundry rebrand (Ignite 2025)` → Signals the strategic pivot to enterprise AI agents and unified workflows. |

## Key New Features (2025–2026)

> `Microsoft Foundry is no longer just a model playground, it’s a unified agent platform that lets developers and enterprises`:

- Build multi-agent systems
- Orchestrate models across providers
- Govern and monitor AI behavior
- Deploy agents into real-world environments like Teams, web apps, and internal tools

| Feature | Description | Key Benefits |
|---------|-------------|--------------|
| [Hosted Agents](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/hosted-agents?view=foundry&tabs=cli) | Build, test, and deploy agents without managing infrastructure. No need for Kubernetes or containers. Supports multi-agent orchestration with shared memory and tools. | Simplifies deployment, reduces infra overhead, enables complex agent ecosystems for enterprise workflows and internal copilots. |
| [Model Router](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/model-router?view=foundry-classic#supported-underlying-models) | Routes requests across multiple models (OpenAI, Claude, Gemini, etc.). Automatically selects the best model for the task. Supports fallback and load balancing. | Optimizes performance and cost, ensures reliability, allows seamless switching between models without code changes. |
| [BYO Model Gateway](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/ai-gateway?view=foundry) | Bring your own model (BYOM) from Hugging Face, Azure ML, or custom endpoints. Integrates with Foundry’s governance and observability stack. | Flexibility to use custom or proprietary models, hybrid cloud/on-prem strategies, unified monitoring and compliance. |
| [One-Click Deployment to Microsoft 365](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/publish-copilot?view=foundry) | Deploy agents directly into Teams, Outlook, SharePoint, and other M365 apps. Includes low-code/no-code templates for internal copilots. Supports user identity, permissions, and organizational data access. | Rapid enterprise adoption, seamless integration with daily productivity tools, secure identity-aware deployments. |
| [Built-in Observability](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/observability-in-foundry-control-plane-empowering-developers-to-evaluate-and-opt/4471107) | Native tracing, telemetry, and evaluation dashboards. Human-in-the-loop feedback tools. Agent memory inspection and optimization tracking. | Improves reliability, enables debugging and optimization, ensures agents meet performance and compliance standards. Useful refs: [Exercise 04: Observe model utilization in Microsoft Foundry](https://microsoft.github.io/TechWorkshop-L300-AI-Apps-and-agents/docs/04_observability_ai_foundry/04_observability_ai_foundry.html), [Agent tracing overview (preview)](https://learn.microsoft.com/en-us/azure/ai-foundry/observability/concepts/trace-agent-concept?view=foundry), [Observability in generative AI](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/observability?view=foundry-classic), [Continuously evaluate your AI agents (preview)](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/continuous-evaluation-agents?view=foundry-classic) |
| [Enterprise Governance](https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview?view=foundry) | Identity management via Microsoft Entra ID. Policy enforcement, audit logging, and compliance controls. Role-based access and agent sandboxing. | Enterprise-grade security, compliance readiness, controlled access, and safe scaling across organizations. |

> BYO Model Gateway:

<img width="850" alt="image" src="https://github.com/user-attachments/assets/24ad6a0b-5de9-4cbf-a5ff-3c480aff6d8a" />

From [Bring your own AI gateway to Azure AI Agent Service (preview)](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/ai-gateway?view=foundry)

> **Core Idea**: In all three cases, your **Agent service** (inside AI Foundry) sends API calls to an **AI Gateway**, which then forwards those calls to the actual AI model resource. The difference is **where the gateway lives** and **which models it connects to**.

**Common Pattern**: 
- **Agent service → Gateway → AI Resource**
- Gateway abstracts the complexity of multiple AI backends.
- Endpoints are consistent (`GET /models`, `POST /chat/completions`), so your agent doesn’t change when you switch backends.
  
  <details>
  <summary> Scenario 1: APIM → Azure OpenAI </summary>
  
  **Flow:**
  
  1.  **Agent service** calls:
      *   `GET /models` → to list available models.
      *   `POST /chat/completions` → to send prompts.
  2.  These requests go through **Azure API Management (APIM)**, which acts as the gateway.
  3.  APIM routes the requests to **Azure OpenAI Resource**.
  4.  Azure OpenAI responds with:
      *   Available models: `gpt-4o`, `gpt-4.1-mini`.
      *   Chat completion results.
  
  **How it works:**
  
  *   APIM is configured with an API that proxies to Azure OpenAI endpoints.
  *   You set up policies for authentication and rate limiting.
  *   Your Agent service only talks to APIM, not directly to OpenAI.
  
  </details>
  
  <details>
  <summary> Scenario 2: APIM → AI Foundry </summary>
  
  **Flow:**
  
  1.  **Agent service** sends the same API calls (`GET /models`, `POST /chat/completions`) to APIM.
  2.  APIM routes these requests to **AI Foundry Resource** (instead of Azure OpenAI).
  3.  AI Foundry responds with:
      *   Models like `gpt-4o`, `mistral-small-2503`.
  
  **How it works:**
  
  *   Same APIM setup, but backend points to AI Foundry’s API.
  *   Useful if you want a single gateway for multiple AI sources.
  
  </details>
  
  <details>
  <summary> Scenario 3: Self-hosted Gateway → AI Foundry</summary>
  
  **Flow:**
  
  1.  **Agent service** sends requests to your **self-hosted gateway**.
  2.  Gateway routes to AI Foundry Resource.
  3.  AI Foundry responds with:
      *   Models like `Deepseek`, `grok-3`, `gpt-5`.
  
  > **How it works:**
  
  - You build and host your own gateway (e.g., using NGINX, FastAPI, or Kong).
  - You control routing, security, and scaling.
  - Ideal if you need full customization or want to avoid APIM costs.
  
  </details>


> Foundry Control Plane Core Functionalities:

<img width="600" alt="image" src="https://github.com/user-attachments/assets/31dcc997-0eb0-424c-b843-dc58e3b89f7d" />

From [What is the Microsoft Foundry Control Plane?](https://learn.microsoft.com/en-us/azure/ai-foundry/control-plane/overview?view=foundry)

> Agent-Centric Architecture: 

| Component | Role |
|-----------|------|
| **Agent Framework** | Defines agent behavior, tools, memory, and orchestration |
| **Hosted Agents** | Runs agents in managed environments |
| **Model Router** | Chooses optimal model per task |
| **Observability Stack** | Tracks agent decisions, performance, and feedback |
| **Governance Layer** | Enforces policies, identity, and compliance |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
