# Demo: configure the Microsoft Fabric (Power BI) MCP connector in Copilot Studio

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-09-29

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Copilot Studio MCP Catalog](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-microsoft-mcp-servers)
- [Connect to an existing Model Context Protocol (MCP) server](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-add-existing-server-to-agent)
- [Microsoft Copilot Studio - MCP](https://github.com/microsoft/mcsmcp) - GitHub repo
- [Consume a Fabric Data Agent in Microsoft Copilot Studio (preview)](https://learn.microsoft.com/en-us/fabric/data-science/data-agent-microsoft-copilot-studio) - Agent
- [Connect to an existing Model Context Protocol (MCP) server](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-add-existing-server-to-agent) - MCP
- [Connecting an Agent in Copilot Studio to an MCP Server](https://techcommunity.microsoft.com/blog/microsoft365copilotblog/connecting-an-agent-in-copilot-studio-to-an-mcp-server/4448362) - blog 
- [Connect AI Agents to Fabric API for GraphQL with a local Model Context Protocol (MCP) server](https://learn.microsoft.com/en-us/fabric/data-engineering/api-graphql-local-model-context-protocol)
- [Fabric data agent concepts (preview)](https://learn.microsoft.com/en-us/fabric/data-science/concept-data-agent)
- [How to create a Fabric data agent (preview)](https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent)
- [Fabric data agent example with the AdventureWorks dataset (preview)](https://learn.microsoft.com/en-us/fabric/data-science/data-agent-scenario): `This example sets up a Fabric data agent to enable conversational AI over enterprise data`. It connects to a lakehouse with the AdventureWorks dataset and allows users to ask natural language questions. The agent interprets queries, accesses data from sources like warehouses, semantic models, and KQL databases, and returns insights. It simplifies data interaction without requiring code or SQL.

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Prepare your data](#prepare-your-data)
- [Use Fabric Data Agent Preferred for Semantic Models](#use-fabric-data-agent-preferred-for-semantic-models)
- [Fabric Data linked to Copilot Studio MCP](#fabric-data-linked-to-copilot-studio-mcp)

</details>

<img width="1141" height="891" alt="MedallionArch-Fabric_Databricks-databricks+data-agents+copilot-Studio drawio" src="https://github.com/user-attachments/assets/2c4f94c6-de41-4b59-b812-0c122483ff53" />

> [!NOTE]
> About the licensing: [Microsoft 365 Copilot Pricing – AI Agents | Copilot Studio](https://www.microsoft.com/en-us/microsoft-365-copilot/pricing/copilot-studio?msockid) <br/>
> Copilot Credit consumption rates:
> - Regular (non-generative AI) = 1 Copilot Credit; and
> - Generative AI (answers over your data) = 2 Copilot Credits.
> Customers can use a mix of classic and generative AI messages with the capacity. [Learn more](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp//microsoft/bade/documents/products-and-services/en-us/bizapps/Power-Platform-Licensing-Guide-September-2025.pdf)
> - Copilot Credits are offered via prepaid Copilot Credit pack subscription licenses. One Copilot Credit pack = 25,000 Copilot Credits.
> - The Copilot Studio pay-as-you-go meter allows you to post-pay based on the actual number of Copilot Credits consumed in a month.

<img width="1309" height="944" alt="image" src="https://github.com/user-attachments/assets/c633ed23-55dd-46a0-855b-df11894bd324" />

## Prepare your data

> [Medallion Architecture](./AzurePortal/1_MedallionArch/): Explore the structured approach to data management.

 <div align="center">
   <img src="https://github.com/user-attachments/assets/2c5141ea-4f3a-4054-b8bd-313efde24ff0" alt="Centered Image" style="border: 2px solid #4CAF50; border-radius: 2px; padding: 2px; width: 900px; height: auto;"/>
 </div>

> Or if you need to handle `complex data transformations and large-scale data processing`, you can use our combined solution of **Fabric + Databricks**. This powerful combination leverages the strengths of both platforms to provide a robust data processing pipeline. This workshop on [Fabric with Databricks for Data Analytics](https://microsoft.github.io/TechExcel-Fabric-with-Databricks-for-Data-Analytics/) offers a comprehensive step-by-step guide on developing Medallion Architecture using Fabric and Databricks. <br/>

<p align="center">
  <img width="650" alt="image" src="https://github.com/user-attachments/assets/58431d3b-e294-46fe-89a4-92a046168ec4" />
</p>

Click [here to read more about Azure Databricks + Fabric](https://github.com/MicrosoftCloudEssentials-LearningHub/DemosScenarios-TechTalks/blob/main/0_Azure/2_AzureAnalytics/3_Databricks/1_demos/0_MedallionArch_Fabric%2BDatabricks/README.md) `better together`

## Use Fabric Data Agent (Preferred for Semantic Models)

> AI skills in Microsoft Fabric enable users to `create conversational AI experiences that answer questions about data stored
> in lakehouses, warehouses, Power BI semantic models, and KQL databases`. These skills make data insights accessible and
> actionable, allowing users to `interact with data naturally and receive relevant answers without needing technical expertise`.
> You can create custom Q&A systems using generative AI, guiding the AI with instructions and examples to ensure it understands your organization's context and data.

Key Features:

- Customizable Q&A Systems: Tailor the AI to answer specific questions relevant to your organization.
- Generative AI: Leverage advanced AI to interact with your data, enhancing data-driven decision-making.
- Ease of Use: Once set up, users can simply ask questions and get accurate answers without needing deep technical knowledge.

E.g: 

<img width="1886" height="831" alt="image" src="https://github.com/user-attachments/assets/79f455c8-da0e-4187-b370-f98aff2985ed" />

<img width="1897" height="837" alt="image" src="https://github.com/user-attachments/assets/3e92d177-c0e6-456c-b965-980aff12a16d" />

<details>
<summary><b> Setup required</b> (Click to expand)</summary>

1. Please ensure you read all the [prerequisites](https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent#prerequisites)
2. **Tenant switch enabled**: These features must be activated as mentioned here [prerequisites](https://learn.microsoft.com/en-us/fabric/data-science/how-to-create-data-agent#prerequisites)
 
    <https://github.com/user-attachments/assets/f0df6fb9-e139-4c97-9b68-a6ea05eb6584>

3. **F2 Fabric capacity or higher**: Ensure you have the appropriate Fabric capacity.
4. **Workspace configured with Fabric Capacity**:

    <img width="200" height="300" alt="image" src="https://github.com/user-attachments/assets/7fbfb16d-a32a-4540-bd03-e6b3c0412a5b">

    <img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/1cb31d49-6138-4c95-835a-a61ccb08661b">

5. At least one of these: A warehouse, a lakehouse, one or more Power BI semantic models, or a KQL database with data.

</details>

<details>
<summary><b> How it works (Click to expand)</summary>

1. Go to the `workspace`, click on `+ New item`, search for `Data agent`, and select it.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/42ff0a1c-3e61-4e24-8bb5-e56db6fe9b7e" />

2. Choose the name for the Data agent instance:
   
     <https://github.com/user-attachments/assets/752734e4-f7f6-44a3-8ccb-069ac005a410>

3. Add data:
   
     <https://github.com/user-attachments/assets/9800e74e-cbca-45ff-a712-bb2e8a095bb5>

4. Relate tables, and start asking!

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/77d5ddbe-8230-440d-9617-d937da48b3cd" />

</details>

> [!NOTE]
> Or use: MCP Server (For Custom Integrations) you create it and connect via Power Platform for example.

<details>
<summary><b> Examples of what to ask (Click to expand)</summary>

| **Question**                                                                 | **Example of it looks**                                                                                       |
|------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **Data Exploration**                                                         |                                                                                                               |
| - Can you provide an overview of this dataset?  <br/> - Are there any missing values or anomalies in this dataset?                               |            <img width="500" alt="image" src="https://github.com/user-attachments/assets/2a43117e-3b29-46f8-98b7-f097df425429">                                                                                                    |
|  What are the key variables in this data?                                   |       <img width="500" alt="image" src="https://github.com/user-attachments/assets/621c6237-7c79-4c67-981a-e9d7afccf29f">|
| **Data Insights**                                                            |                                                                                                               |
| What patterns or trends can you identify in this data?                     |<img width="500" alt="image" src="https://github.com/user-attachments/assets/899653c3-fa41-4834-8606-37759a7f1ad6">               |
| Can you highlight any correlations between variables?                      | <img width="500" alt="image" src="https://github.com/user-attachments/assets/a9442f38-ade1-45ee-9cb6-4adf8bdbf0f7">              |
| What are the outliers in this dataset?                                     | <img width="500" alt="image" src="https://github.com/user-attachments/assets/1c0d07b2-91fe-4335-9760-886c10e77bb9">                 |

</details>

## Fabric Data linked to Copilot Studio (MCP)

1. Create a Data Agent in Microsoft Fabric and connect it to your semantic model.
2. Publish the agent and verify that it is running successfully.
3. In Copilot Studio, go to `Agents → Add an agent`, then `select your Fabric Data Agent from the list.`
4. Test the integration by running sample queries such as: `What was the revenue last quarter?`

<img width="1898" height="993" alt="image" src="https://github.com/user-attachments/assets/94620e12-61df-4233-93db-b04af1bdd294" />

https://github.com/user-attachments/assets/bdb581c2-ccc9-48b1-a4ce-6b3c465f10bc

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
