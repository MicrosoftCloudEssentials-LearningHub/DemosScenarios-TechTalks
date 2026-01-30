# Azure OpenAI: Models Deployment Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Overview: Deploy AI models in Azure AI Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/deployments-overview)
- [Getting started with Azure OpenAI batch deployments](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/batch?tabs=global-batch%2Cstandard-input%2Cpython-secure&pivots=ai-foundry-portal)

</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Overview](#overview)
- [How to](#how-to)
- [Example API Call](#example-api-call)

</details>

## Overview

> `Deployments` in Azure OpenAI Studio involve making AI models, workflows, and applications available for use in production environments. This includes hosting models on servers or in the cloud and creating APIs or other interfaces for users to interact with the models.

Types of deployments available in Azure OpenAI Studio:

| **Deployment Method**       | **Description**                                                                 | **Billing Model**                      | **Deployment Process**                                                                 |
|-----------------------------|---------------------------------------------------------------------------------|----------------------------------------|----------------------------------------------------------------------------------------|
| **Serverless API**          | Deploy models as serverless APIs, accessible via endpoints without managing infrastructure. | Pay-as-you-go (per token/request)      | 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Configure deployment settings.<br/>7. Click `Deploy`.<br/>8. Use the generated API endpoint to integrate the model. |
| **Models as a Service (MaaS)** | Managed service where models are hosted and maintained by Azure.                | Pay-as-you-go (per token)              | 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Configure deployment settings.<br/>7. Click `Deploy`.<br/>8. Use the generated API endpoint to integrate the model. |
| **Models as a Platform (MaaP)** | Deploy models on dedicated virtual machines (VMs) for more control over resources. | Billed as VMs per-hour                 | 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Choose VM specifications.<br/>7. Configure deployment settings.<br/>8. Click `Deploy`.<br/>9. Use the generated API endpoint to integrate the model. |
| **Flows and Web Applications** | Deploy models as part of larger workflows or web applications.                  | Varies based on usage                  | 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Configure deployment settings.<br/>7. Integrate the model into your workflow or web application.<br/>8. Click `Deploy`.<br/>9. Use the generated API endpoint to integrate the model. |
| **Managed Compute**         | Use Azure's managed compute resources to deploy and run models.                 | Combination of compute and storage costs| 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Choose managed compute resources.<br/>7. Configure deployment settings.<br/>8. Click `Deploy`.<br/>9. Use the generated API endpoint to integrate the model. |
| **Provisioned-Managed**     | Ensures consistent performance by allocating specific throughput capacity using PTUs. | Billed based on the number of PTUs provisioned. | 1. Create a project in Azure OpenAI Studio.<br/>2. Navigate to the project dashboard.<br/>3. Click on `Deployments`.<br/>4. Click `+ Deploy model`.<br/>5. Select a model from the catalog.<br/>6. Configure deployment settings, including the number of PTUs.<br/>7. Click `Deploy`.<br/>8. Use the generated API endpoint to integrate the model. |

1. **Create a Project**: Go to Azure OpenAI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy a Model**: Navigate to the project, select `Deployments`, and click `+ Deploy model`.
3. **Select a Model**: Choose a model from the model catalog, such as an Azure OpenAI model.
4. **Configure Deployment**: Specify the deployment name and modify settings as needed.
5. **Deploy**: Click `Deploy` to make the model available as an API.
6. **Integrate and Use**: Use the generated API endpoint to integrate the deployed model with your applications.

## How to 
1. Create an Azure OpenAI Resource
    - Sign in to the [Azure portal](https://portal.azure.com).
    - Navigate to **Create a resource** and search for **Azure OpenAI**.
    - Follow the prompts to create your resource, ensuring it's in a region that supports the models you need.

      <img width="500" alt="image" src="https://github.com/user-attachments/assets/7719500c-9f47-4afe-983e-19fa3027138e">
      
> [!NOTE]
> When creating your Azure OpenAI resource, ensure you select a resource group and region that supports the specific model versions you want to use. This can affect latency and availability.

2. Deploy the Model
    - Once your resource is created, go to the **Azure OpenAI Studio**.
    - Select **Deployments** and click on **Create**.
    - Choose the model version you want to deploy (e.g., `gpt-4o-mini-2024-07-18`).

      <img width="500" alt="image" src="https://github.com/user-attachments/assets/e4f11fff-7ab2-4bb5-bfbb-eaab13d88932">

> [!NOTE]  
> After deploying the model, you'll receive an API key. Keep this key secure and manage it through Azure's Key Vault for added security. <br/>
> Be aware of the usage quotas and pricing associated with each model. You can monitor your usage and set up alerts in the Azure portal to avoid unexpected costs.

3. Configure the Model
    - **Fine-tuning (Optional)**: If you need to fine-tune the model, you can do so by preparing your training data and following the fine-tuning workflow in the Azure OpenAI Studio.
    - **Structured Outputs**: For the GPT-4o-2024-08-06 model, you can specify JSON Schemas within your API calls to ensure the AI output adheres to your defined structure.

> [!NOTE]
> **Temperature and Max Tokens**: Adjust the `temperature` parameter to control the randomness of the output and `max_tokens` to limit the length of the response. <br/>
> **Top-p and Frequency Penalty**: Use `top_p` to control the diversity of the output and `frequency_penalty` to reduce repetitive responses.

4. Integration and Testing
    - Integrate the deployed model into your application using the provided API endpoints.
    - Test thoroughly to ensure the model meets your requirements and adheres to any specified output formats.

> [!NOTE]
> Implement robust error handling in your application to manage API rate limits, timeouts, and other potential issues.
> Use logging to track API calls and responses for debugging and performance monitoring.

## Example API Call

Here's a basic example of how you might call the model using Python:

```python
import openai

openai.api_key = "YOUR_API_KEY"

response = openai.Completion.create(
  model="gpt-4o-2024-08-06",
  prompt="Your prompt here",
  max_tokens=100
)

print(response.choices[0].text)
```

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
