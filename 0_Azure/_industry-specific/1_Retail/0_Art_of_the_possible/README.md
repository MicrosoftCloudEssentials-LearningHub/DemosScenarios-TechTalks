# AI Use cases: Art of the possible - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------


<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What is Real-Time Intelligence?](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/overview#how-do-i-use-real-time-intelligence)
- [Overview of Microsoft Fabric eventstreams](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-streams/overview?tabs=enhancedcapabilities)
- [Overview of Microsoft Fabric eventstreams](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-streams/overview?tabs=enhancedcapabilities)

</details>


## AI Shopping assistant

> `my own copilot`, `want to chat with my data` [GPT-RAG Solution Accelerator](https://github.com/Azure/GPT-RAG). RAG-based chatbot to interact with manuals, guides, and product data for better search and personalization.

| [Public Architecture](#basic-architecture)  | [Private Architecture](./1_PrivateArchitecture.md) |  [Standard Zero-Trust Architecture](https://github.com/Azure/GPT-RAG) |
| --- | --- | --- | 
|  <img width="800" alt="image" src="https://github.com/user-attachments/assets/5444e87c-32af-44e8-aa86-22fe4082c4f4" />    |   <img width="800" alt="image" src="https://github.com/user-attachments/assets/af835493-2d76-4216-8df6-3e258c9db949"> | <img width="800" alt="image" src="https://github.com/user-attachments/assets/67e7d9eb-f757-4fe9-85f4-d5bb08b9e55f" /> |

## Analyze customer behavior and feedback for trend discovery

[Demo: How to configure the Microsoft Fabric (Power BI) MCP connector in Copilot Studio](https://github.com/MicrosoftCloudEssentials-LearningHub/Fabric-MCP-Agent2Agent)

> Low code approach (Copilot Studio Agents):

<img width="1141" height="669" alt="MCP-Fabric-Agent2Agent-CopilotStudio-databricks+data-agents+copilot-Studio drawio" src="https://github.com/user-attachments/assets/76be59e3-f48e-4c01-aa58-464463658d92" />

> Full code approach (AI Foundry Agents):

<img width="1141" height="668" alt="MCP-Fabric-Agent2Agent-CopilotStudio-data agent Fabric + AI Foundry drawio" src="https://github.com/user-attachments/assets/5742dc3a-427d-4ab5-862d-ba291a31fc35" />

## Customer360 AI Experience

- Enable AI-driven suggestions for complementary products
- Real-time sentiment analysis and campaign triggers based on trends.
- Improve data taxonomy and metadata
- Enhance user experience with personalized content blocks.

<img width="1656" height="921" alt="retail-ai-samples drawio" src="https://github.com/user-attachments/assets/c7b41c55-fd5e-4e6f-af1c-d206e32e0d51" />

> [!TIP]
> 1.  **Complementary Product Suggestions**: Gold layer → AI Foundry/OpenAI → Recommendation API → Web App.
> 2.  **Real-Time Sentiment & Campaign Triggers**: Eventstream → KQL → Data Activator → Marketing automation.
> 3.  **Improve Taxonomy & Metadata**: Purview ensures consistent metadata and compliance across layers.
> 4.  **Personalized Content Blocks**: Azure ML models → App Service → Front Door → End-user experience.

| **Layer / Component** | **Details** |
|------------------------|-------------|
| **1. Data Sources** | • **E-commerce Platform**: Provides product catalog, pricing, inventory, and order history.<br>• **Customer Interaction Data**: Includes clickstream, browsing patterns, and purchase behavior.<br>• **Social Media APIs (X, YouTube, Instagram, TikTok)**: Streams hashtags, influencer posts, and comments for trend and sentiment analysis.<br>• **API Connections**: Enable secure data pulls from external sources into the platform. |
| **2. Ingestion Layer** | • **Fabric Data Factory**:<br> – Handles **batch ingestion** of structured data from e-commerce and customer systems.<br> – Moves raw data into the **Bronze layer** in OneLake.<br>• **Eventstream (Fabric)**:<br> – Captures **real-time social media feeds** and customer interaction events.<br> – Streams data directly into OneLake and **Real-Time Analytics (KQL)** for immediate processing. |
| **3. Medallion Architecture in Fabric** | • **Bronze (Raw)**: Stores unprocessed data from APIs and batch pipelines.<br>• **Silver (Cleaned/Transformed)**:<br> – PySpark notebooks clean, standardize, and enrich data.<br> – Apply taxonomy rules and metadata alignment.<br>• **Gold (Curated)**:<br> – Business-ready tables for analytics and AI models.<br> – Includes aggregated sentiment scores, product attributes, and customer segments. |
| **4. Governance & Metadata (Microsoft Purview)** | • Scans Silver and Gold layers for lineage and compliance.<br>• Maintains taxonomy dictionaries and metadata standards.<br>• Applies sensitivity labels and access policies for secure data usage. |
| **5. Real-Time Analytics** | • **KQL Database (Fabric Real-Time Analytics)**:<br> – Processes Eventstream data for sentiment scoring and trend detection.<br> – Outputs aggregated insights to Gold layer for reporting and AI consumption.<br>• **Data Activator / Logic Apps**: Triggers marketing campaigns or feature flags when sentiment thresholds are met. |
| **6. AI & Machine Learning** | • **Azure AI Foundry + OpenAI**:<br> – Generates complementary product suggestions using:<br>  • Content-based filtering (attributes, taxonomy).<br>  • RAG (Retrieval-Augmented Generation) for product guides.<br>• **Azure Machine Learning**:<br> – Trains personalization models (propensity, uplift).<br> – Deploys endpoints for real-time scoring.<br>• **AI Vision & AI Services**: Optional image analysis for social media content. |
| **7. Delivery Layer** | • **Container App / Web App**: Hosts APIs for personalized content blocks and recommendation engine.<br>• **Azure Front Door/CDN**: Ensures global, low-latency delivery of personalized experiences.<br>• **App Service Plan**: Provides scalable hosting for web applications. |
| **8. Insights & Reporting** | • **Power BI (Direct Lake Mode)**:<br> – Connects to Lakehouse in OneLake for real-time dashboards.<br> – Displays campaign performance, sentiment trends, and recommendation effectiveness.<br>• **Copilot**: Assists business users with natural language queries on data. |
| **9. Security & Monitoring** | • **Azure Key Vault**: Stores API keys, credentials, and secrets securely.<br>• **Azure Monitor & Application Insights**: Tracks pipeline health, model latency, and API performance. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
