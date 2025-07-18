#  RAG: Zero Trust Architecture - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> For Azure AI Search and OpenAI in a Retrieval-Augmented Generation (RAG) setup, find below an example of how these components are interconnected within a secure Azure environment.

<details>
<summary><b> References </b> (Click to expand)</summary>
   
- [RAG Microsoft Enterprise RAG Solution Accelerator (GPT-RAG) - github repo](https://github.com/Azure/GPT-RAG)
- [Overview – Apply Zero Trust principles to Azure IaaS](https://learn.microsoft.com/en-us/security/zero-trust/azure-infrastructure-overview)
- [Zero Trust defined](https://www.microsoft.com/en-us/security/business/zero-trust?msockid=38ec3806873362243e122ce086486339)
- [Zero Trust Essentials eBook](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/final/en-us/microsoft-brand/documents/zero-trust-essentials-ebook.pdf)
  
</details>

## Overview

> As Microsoft defined Zero Trust:

![image](https://github.com/user-attachments/assets/da80a334-e6a0-4d53-aa9f-9b81029980fe) <br/>
From [Microsoft Security](https://www.microsoft.com/en-us/security/business/zero-trust?msockid=38ec3806873362243e122ce086486339)


## Components

1. **Azure Services Subscription**: The overarching subscription under which all services are organized.
2. **Resource Group (RG) for RAG**: A logical container that holds related resources, ensuring they are managed and secured together.
3. **Storage Account**: Used to store data securely.
4. **AI + Machine Learning Services**: This includes:
   - **Azure AI Search**: For indexing and searching documents.
   - **Azure OpenAI**: For generating responses based on retrieved documents.
   - **Azure Key Vault**: For securely storing secrets like API keys and connection strings.
5. **Virtual Network (VNet)**: Provides network isolation and security. It contains subnets such as:
   - **AI-services-subnet**: Hosts AI-related services.
   - **app-service-subnet**: Hosts application services.
6. **VM for Data Science**: A virtual machine used for data science tasks within the AI-services-subnet.
7. **App Service Plan and Web App**: Part of the app-service-subnet, used to host web applications.

## Workflow in Zero Trust Architecture

> Network Interface & Network Security Groups: 

![nic-nsg-detailed](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/3_AzureAI/0_AISearch/demos/1_ZeroTrustRAG/docs/0_nic-nsg-detailed.png)

> Zero trust: Initial Phase

![zero-trust-phase0](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/3_AzureAI/0_AISearch/demos/1_ZeroTrustRAG/docs/1_zero-trust-phase0.png) 

> Microsoft Enterprise RAG Solution Accelerator: 

1. **User Interaction**: The user initiates a request from their device.
2. **Azure Front Door and WAF**: The request is routed through Azure Front Door and Web Application Firewall (WAF) for initial security checks.
3. **App Service (Frontend)**: The request reaches the frontend application hosted on Azure App Service via a private endpoint.
4. **Orchestrator (Azure Function)**: The frontend communicates with an orchestrator function within the VNet, which manages the flow of data.
5. **Database Access**: The orchestrator accesses Azure Cosmos DB to retrieve conversation history.
6. **Vector Embedding**: The orchestrator requests Azure OpenAI to generate vector embeddings from the user’s query.
7. **Key Vault Access**: The orchestrator retrieves the AI Search API key from Azure Key Vault.
8. **Document Retrieval**: The orchestrator queries Azure AI Search to retrieve relevant documents.
9. **Response Generation**: The orchestrator uses Azure OpenAI to generate a response based on the retrieved documents.
10. **Response Delivery**: The response is sent back to the user through the same secure path.

![Microsoft-RAG_Azure-Template](https://github.com/brown9804/MicrosoftCloudEssentialsHub/blob/main/0_Azure/3_AzureAI/0_AISearch/demos/1_ZeroTrustRAG/docs/2_Microsoft-RAG_Azure-Template.png) <br/> 
From [Zero Trust Architecture Deployment](https://github.com/Azure/GPT-RAG?tab=readme-ov-file#zero-trust-architecture-deployment)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
