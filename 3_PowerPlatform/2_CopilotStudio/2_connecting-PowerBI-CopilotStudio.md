# Demo: configure the Microsoft Fabric (Power BI) MCP connector in Copilot Studio

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Copilot Studio MCP Catalog](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-microsoft-mcp-servers)
- [Connect to an existing Model Context Protocol (MCP) server](https://learn.microsoft.com/en-us/microsoft-copilot-studio/mcp-add-existing-server-to-agent)
- [Microsoft Copilot Studio - MCP](https://github.com/microsoft/mcsmcp) - GitHub repo
- [Consume a Fabric Data Agent in Microsoft Copilot Studio (preview)](https://learn.microsoft.com/en-us/fabric/data-science/data-agent-microsoft-copilot-studio)
- [Connecting an Agent in Copilot Studio to an MCP Server](https://techcommunity.microsoft.com/blog/microsoft365copilotblog/connecting-an-agent-in-copilot-studio-to-an-mcp-server/4448362) - blog 
- [Connect AI Agents to Fabric API for GraphQL with a local Model Context Protocol (MCP) server](https://learn.microsoft.com/en-us/fabric/data-engineering/api-graphql-local-model-context-protocol)

</details>

## Step 1: Prepare Your Environment

Before you begin, make sure you have:
- Access to **Microsoft Copilot Studio**: https://studio.copilot.microsoft.com
- Access to **Power Platform**: https://make.powerapps.com
- A **Power BI dataset** published in **Microsoft Fabric**
- An **Azure subscription** (for secure deployment)
- Admin rights to create **custom connectors**

## Step 2: Deploy the Fabric MCP Server

Microsoft provides a Fabric MCP server that supports:
- Listing workspaces and datasets
- Executing DAX queries
- Triggering dataset refreshes 

You can deploy it using Azure Container Apps or run it locally using Docker.

> To deploy:
1. Clone the official repo:  
   [Microsoft Fabric MCP GitHub](https://github.com/snahrup/microsoft-fabric-mcp) 
2. Follow the instructions in the `README.md` for:
   - Local development
   - Azure deployment
   - Authentication setup (OAuth 2.0 recommended)

## Step 3: Create a Custom Connector in Power Platform

1. Go to https://make.powerapps.com
2. In the left menu:
   - Click **More** → **Discover all**
   - Under **Data**, pin **Custom connectors**
3. Click **Custom connectors** → **New custom connector** → **Create from blank**
4. Name your connector (e.g., `FabricMCPConnector`) → Click **Continue**

## Step 4: Configure the Connector
1. Toggle **Swagger editor**
2. Paste the OpenAPI (Swagger) YAML from the MCP repo:
   - Replace `dummyurl.azurewebsites.net` with your deployed MCP server URL
3. Click **Create connector**

## Step 5: Add the MCP Connector to Copilot Studio

1. Go to https://studio.copilot.microsoft.com
2. Open your **agent**
3. Go to **Tools** → **Add a tool**
4. Choose **Model Context Protocol (MCP)**
5. Fill in:
   - **Name**: Fabric MCP
   - **Description**: Connects to Power BI datasets via Fabric
   - **Server URL**: `https://your-mcp-server-url/mcp`
6. Choose **Authentication**:
   - Use **OAuth 2.0** with Azure AD App credentials
7. Click **Create**

## Step 6: Test the Integration

1. In Copilot Studio, create a **topic** like “Ask about sales data”
2. Use the MCP tool to invoke:
   - `tools/list` → to list available datasets
   - `tools/query` → to run DAX queries
3. Validate responses and format them using adaptive cards or plain text



<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
