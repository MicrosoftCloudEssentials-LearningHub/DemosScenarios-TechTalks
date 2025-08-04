# AI Foundry: AI Model Management with Software Development Life Cycle (SDLC) 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!NOTE]
> If you require additional information on Cloud and the SDLC process, please visit this [repository](https://github.com/brown9804/CloudDevOps_LPath?tab=readme-ov-file#cloud-devops---learning-path). It contains content not only on SDLC but also on DevOps practices.

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Create a project in Azure AI Foundry portal](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/create-projects)
- [Overview: Deploy AI models in Azure AI Foundry portal](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/deployments-overview)
- [What is Azure role-based access control (Azure RBAC)?](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview)
- [Role-based access control in Azure AI Foundry portal](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/rbac-ai-studio)
- [5 Ways to Implement Enterprise Security with Azure AI Foundry](https://techcommunity.microsoft.com/blog/aiplatformblog/5-ways-to-implement-enterprise-security-with-azure-ai-foundry/4253221)
- [Baseline OpenAI end-to-end chat reference architecture](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/baseline-openai-e2e-chat)
- [Azure OpenAI chat baseline architecture in an Azure landing zone - Tech Community](https://techcommunity.microsoft.com/blog/azurearchitectureblog/azure-openai-chat-baseline-architecture-in-an-azure-landing-zone/4149124)
- [Azure OpenAI chat baseline architecture in an Azure landing zone - MS article](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/azure-openai-baseline-landing-zone)
- [GenAIOps with prompt flow and Azure DevOps](https://learn.microsoft.com/en-us/azure/machine-learning/prompt-flow/how-to-end-to-end-azure-devops-with-prompt-flow?view=azureml-api-2)
- [Integrate prompt flow with DevOps for LLM-based applications](https://learn.microsoft.com/en-us/azure/machine-learning/prompt-flow/how-to-integrate-with-llm-app-devops?view=azureml-api-2&tabs=cli)
- [GenAIOps with prompt flow and GitHub](https://learn.microsoft.com/en-us/azure/machine-learning/prompt-flow/how-to-end-to-end-llmops-with-prompt-flow?view=azureml-api-2)
- [What is Azure AI Foundry?](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry#which-type-of-project-do-i-need) - Which type of project do I need? Hub or Project

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>
    
- [Overview](#overview)
- [Demo](#demo)
    - [Create a Resource Group](#create-a-resource-group)
    - [Set Up AI Foundry](#set-up-ai-foundry)
    - [Deploy AI Models on AI Foundry](#deploy-ai-models-on-ai-foundry)
    - [Set Up Azure API Management](#set-up-azure-api-management)
    - [Flexible Model Modification (RBAC for Approach 1)](#flexible-model-modification-rbac-for-approach-1)
    - [Ready-to-Use API (for Approach 2)](#ready-to-use-api-for-approach-2)
    - [Implement Monitoring and Analytics](#implement-monitoring-and-analytics)

</details>

> [!IMPORTANT]
> This overview provides an example of how to create an infrastructure that enables efficient and secure delivery of AI models into different solutions. By setting up AI Foundry with RBAC, using Azure API Management, and implementing monitoring and analytics, you can ensure your AI models are accessible, manageable, and perform well across different environments. Please ensure to adjust the infrastructure, networking, and other configurations as required. <br/>
> 1. **Set Up Resource Group and AI Foundry Hub**: Create a centralized hub for managing your AI resources. <br/>
> 2. **Create Projects for Different Environments**: Organize your AI models into development, testing, and production projects. <br/>
> 3. **Implement RBAC**: Assign roles to users based on their profile to manage access and permissions. <br/>
> 4. **Expose Models as APIs**: Use Azure API Management to make your AI models accessible via APIs. <br/>
> 5. **Provide Documentation and Support**: Ensure users have the necessary resources and support to integrate the APIs. <br/>
> 6. **Implement Monitoring and Analytics**: Track the performance and usage of your AI models to ensure they meet your needs.

## Overview 

```mermaid
graph TD
    A[AI Hub] -->|Contains| B[Project 1]
    A[AI Hub] -->|Contains| C[Project 2]
    A[AI Hub] -->|Contains| D[Project 3]
    B[Project 1] -->|Manages| E[AI Model 1]
    B[Project 1] -->|Manages| F[AI Model 2]
    C[Project 2] -->|Manages| G[AI Model 3]
    C[Project 2] -->|Manages| H[AI Model 4]
    D[Project 3] -->|Manages| I[AI Model 5]
    D[Project 3] -->|Manages| J[AI Model 6]
    E[AI Model 1] -->|Deployed to| K[Development Environment]
    F[AI Model 2] -->|Deployed to| L[Test Environment]
    G[AI Model 3] -->|Deployed to| M[Production Environment]
    H[AI Model 4] -->|Deployed to| N[Development Environment]
    I[AI Model 5] -->|Deployed to| O[Test Environment]
    J[AI Model 6] -->|Deployed to| P[Production Environment]
```
1. **AI Hub**:
   - The AI Hub serves as the `central repository for all AI-related resources and activities`.
   - It provides a unified interface for managing AI models, deployments, and related services.
2. **Project-Based Structure**:
   - AI Foundry works by organizing resources into projects.
   - `Each project can contain multiple AI models, deployments, and configurations`.
   - Projects help in `segregating different AI initiatives, making it easier to manage and track progress`.
3. **Model Deployment**:
   - Users can choose from existing models for deployment, eliminating the need for manual uploads.
   - The platform supports deploying base models, fine-tuned models, and custom models.
   - Deployment configurations can be tailored to specific environments such as development, testing, and production.
4. **Management and Monitoring**:
   - AI Foundry provides tools for managing model versions, ensuring that updates and changes are tracked effectively.
   - Integrated monitoring and analytics help in tracking the performance and usage of deployed models.
5. **User Flexibility**:
   - The platform caters to both technical and non-technical users.
   - Technical users can leverage advanced features for model customization and fine-tuning.
   - Non-technical users can easily deploy and use pre-configured models through a user-friendly interface.

> Delivering your AI models via API, catering to different levels of flexibility for users.

| Approach                  | Description                                                                                       | Components                                                                                           |
|---------------------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Flexible Model Modification** | This approach allows customers to modify and fine-tune the AI models according to their specific needs. | 1. **AI Foundry**: Use AI Foundry to host and manage your AI models. This platform provides tools for customers to modify and fine-tune models.<br>2. **Azure API Management**: Expose the models as APIs, allowing customers to integrate them into their systems.<br>3. **RBAC in AI Foundry**: Implement RBAC to manage permissions and ensure security. Assign roles based on user profile.<br>4. **Monitoring and Analytics**: Use Azure Monitor and Application Insights to track usage, performance, and modifications made by customers. |
| **Ready-to-Use API**      | This approach provides customers with a ready-to-use API, requiring no modifications.              | 1. **AI Foundry**: Host the pre-trained models on AI Foundry.<br>2. **Azure API Management**: Expose these models as APIs, ensuring they are easy to integrate into customer systems.<br>3. **Documentation and Support**: Provide comprehensive documentation and support to help customers integrate the API into their systems without needing to modify the models.<br>4. **Monitoring and Analytics**: Use Azure Monitor and Application Insights to track API usage and performance. |

## Demo 

> Please follow the general setup for both approaches. You will then notice a distinction between these approaches in the subsequent subsections. Click [here to access the template arch diagram](https://github.com/brown9804/MicrosoftCloudEssentialsHub/tree/main/0_Azure/3_AzureAI/AIFoundry/demos/2_AIFoundrySDLCStrategy/docs)

<p style="text-align: center">
    <img width="750" alt="image" src="https://github.com/user-attachments/assets/5aad6eea-e355-4c82-ac34-4e45b8df7934">
</p>

### Create a Resource Group

1. **Navigate to Azure Portal**: Go to the [Azure Portal](https://portal.azure.com/#create/Microsoft.ResourceGroup).
2. **Create Resource Group**:
   - Click on `Resource groups` in the left-hand menu.
   - Click `Create`.
   - Enter a name for your resource group (e.g., `RG-AI-Models`).
   - Select your subscription and region.
   - Click `Review + create` and then `Create`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/dfdec16b-62bf-4908-afbe-adc7cd790b21" />

### Set Up AI Foundry

1. **Deploy AI Foundry**:
   - Search for `AI Foundry` in the Azure Marketplace.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/ae229839-94a6-4113-a97d-9d2775d1c28f" />

   - Click `Create` and fill in the required details (e.g., name, resource group).
   - Configure the settings as needed and click `Review + create` and then `Create`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/81e4b637-4058-412e-a252-aef5aaa3d9f3" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/9a7e2469-9636-4b1e-8574-2d6d9c2529fc" />

2. Create a project: AI Hub with AI Foundry is a powerful platform designed to streamline the deployment and management of AI models. `It operates on a project-based structure`, allowing for organized and efficient handling of AI initiatives.
  
    - Navigate to your `AI Foundry` instance.
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/fa32b6b5-af32-416c-836d-28a8c9c1823c" />
    
    > If you don't have a hub, you'll need to create one.
    
    - Click `+ Create project`.
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/54a96184-b55f-4c95-8a15-d787990d2738" />
    
    - Enter a name for your project (e.g., `AIModelProject-Dev`).
    - Select your hub from the dropdown. If you don't have one, create a new hub as described above.
    - Click `Create`.
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/598e1f2a-8f3b-481f-af39-6f803310306e" />
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/06f54a42-c38b-473f-87be-e8ca8a582299" />

### Deploy AI Models on AI Foundry

> [!NOTE]
> If you are not sure about which model is required, you can compare them by going to the `Model catalog`, and `Compare models`:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/37774e6f-f080-4706-9f2a-65598404c489" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/70ab5985-e163-471f-b47e-5ff43f346282" />

1. **Choose Models for Deployment**:
   - Navigate to your project, under `My assets`, `Models+ endpoints`.
   - Click on `Deploy model`, `Deploy base model`, or `Deploy fine-tuned model`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/9f97ffd0-3480-4bde-bcdb-b61d5d304cf9" />

   - Select the model you want to deploy from the available options.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/9cb03fbb-9d1c-4009-bdcf-051d4902c00a" />

2. **Configure Deployment**:
   - Follow the prompts to configure your deployment settings.
   - Click `Deploy` to initiate the deployment process.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/bd03bdbb-9156-4789-b44f-f1122e9cbaee" />

   - Specify the version, deployment environment (e.g., dev, test, prod), and any other necessary parameters.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/f808a8d9-32c4-4a06-b066-e04d65b1485e" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/031eb581-c81a-4a58-8725-b64a49da4361" />

> [!IMPORTANT]
> Please perform all necessary tuning and evaluation as required. This serves as an end-to-end example of how to integrate AI into multiple services using two approaches: one that is more flexible for those familiar with model configuration and tuning, and another that provides ready-to-use APIs for users needing a secure API for their applications.

### Set Up Azure API Management

> **Azure API Management** will be used to expose your AI models as APIs. This allows your customers to integrate the AI models into their systems seamlessly. Here are the key roles it plays: <br/> 
> 1. **API Exposure**: It helps in creating and managing APIs for your AI models, making them accessible to your customers. <br/>
> 2. **Security**: It provides robust security features to protect your APIs, including authentication, authorization, and rate limiting. <br/>
> 3. **Scalability**: It ensures that your APIs can handle varying levels of traffic, scaling up or down as needed. <br/>
> 4. **Monitoring and Analytics**: It offers tools to monitor API usage, performance, and health, providing valuable insights for optimization. <br/>
> 5. **Documentation**: It allows you to create and publish comprehensive documentation for your APIs, helping customers understand how to use them effectively.

1. **Create API Management Service**:
   - Search for `API Management` in the Azure Marketplace.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/fb0f913c-4926-4de0-83ff-f8bce064eb22" />

   - Click `Create` and fill in the required details (e.g., name, resource group).
   - Configure the settings and click `Review + create` and then `Create`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/475c29d2-d117-4c9e-8361-a559ff7319f9" />

2. **Expose AI Models as APIs**:
   - Navigate to your `API Management` instance.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/1fb9d44b-9f00-4351-9548-4abdf8920e73" />

   - In the API Management instance, click on `APIs` in the left-hand menu.
   - **Define the API**:

       - **HTTP**: Choose this option if you want to expose your AI model as an HTTP API.
       - **WebSocket**: Select this for full-duplex communication over a single TCP connection.
       - **GraphQL**: Use this if you want to expose your API using GraphQL.
       - If you have an existing API definition, you can use options like `OpenAPI`, `WADL`, `WSDL`, or `GraphQL Schema` to import the API definition.

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/8158db35-57fc-4746-bac4-48dcaa290710" />

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/80ac17f7-0012-4b89-a3d2-8eb4fef90c29" />

   - Configure the endpoints and security settings.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/b16cfb63-4fe0-415b-935d-a190d5936c74" />

### Flexible Model Modification (RBAC for Approach 1)

> Implement RBAC (Role-Based Access Control)

1. **Set Up AI Foundry Projects**:
   - Create projects for development, testing, and production within AI Foundry.
   - Assign roles based on user profile:
       - **Project Owner**: Full access to manage and modify models.
       - **Project Contributor**: Access to modify and fine-tune models but cannot manage project settings.
       - **Project Developer**: Access to develop and test models, including making modifications and running experiments.
       - **Project Reader**: View-only access for users who need to monitor models without making changes.
   - Go to `Management center`:
     
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/15bfb87f-e98a-4217-9031-8b61d5875b8b" />

   - Make sure you create the remaining projects for the stages: development, testing, and production accordingly.
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/5994cef2-adf3-41d3-8e8d-f43eda75048e" />

   -  Click on each project to manage users and roles. Under `Overview`, go to `Project users` and click on `View all`. To add the necessary personas.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/0107c650-91d0-4abb-8dd7-2ad2950a6b15" />

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/c081ba94-5a21-45e9-84dc-70b5bafa3d65" />

2. **Configure RBAC**:
   - Navigate to your AI Foundry instance.
   - Go to `Access control (IAM)` and assign roles to users or groups based on their skill levels and responsibilities.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/6c48b098-de99-4764-b7fe-84db7b2daecd" />

###  Ready-to-Use API (for Approach 2)

> Provide Documentation and Support 

1. **Create Documentation**:
   - Develop comprehensive documentation for integrating the API.
   - Include examples, use cases, and troubleshooting tips.
2. **Set Up Support Channels**:
   - Provide support channels (e.g., email, chat) for customer queries and issues.

### Implement Monitoring and Analytics 

1. **Set Up Azure Monitor**:
   - Navigate to `Azure Monitor` in the Azure Portal.
   - Create alerts and dashboards to monitor the performance and usage of your AI models.
2. **Integrate Application Insights**:
   - Navigate to `Application Insights` in the Azure Portal.
   - Create an `Application Insights` resource and integrate it with your AI models and APIs.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
