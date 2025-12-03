# How to Save and Reuse Parameter Settings in Azure OpenAI & AI Studio Variants

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Tune prompts using variants in Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/flow-tune-prompts-using-variants)
- [Prompt tool for flows in Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/prompt-flow-tools/prompt-tool)
  
</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [How to Save and Reuse Parameter Settings in Azure OpenAI & AI Studio Variants](#how-to-save-and-reuse-parameter-settings-in-azure-openai--ai-studio-variants)
    - [Wiki](#wiki)
    - [Content](#content)
    - [GUI approach over Azure OpenAI](#gui-approach-over-azure-openai)
    - [Variants Approach over Azure OpenAI](#variants-approach-over-azure-openai)
        - [Create an Azure OpenAI Resource](#create-an-azure-openai-resource)
        - [Setup your project](#setup-your-project)
        - [Indexing Your Data](#indexing-your-data)
        - [Deploy a Model](#deploy-a-model)
        - [Configure the prompt flow:](#configure-the-prompt-flow)
        - [Add an LLM Node](#add-an-llm-node)
        - [Configuring Variants in Azure AI Studio](#configuring-variants-in-azure-ai-studio)
            - [Create Variants](#create-variants)
            - [Configure Parameters for Each Variant](#configure-parameters-for-each-variant)
        - [Run and Evaluate Variants](#run-and-evaluate-variants)
        - [Monitor and Adjust](#monitor-and-adjust)
        - [Example Code Snippet](#example-code-snippet)

</details>

## GUI approach over Azure OpenAI 

> You can use the export option:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/0f061e1a-27a6-466a-94ff-4b093fadbbc9">

> Which will look like this:

```json
{
    "systemPrompt": "You are an AI assistant that helps people find information.",
    "fewShotExamples": [],
    "chatParameters": {
        "deploymentName": "gpt-4o-mini",
        "maxResponseLength": 800,
        "temperature": 0.7,
        "topProbablities": 0.95,
        "stopSequences": [],
        "pastMessagesToInclude": 10,
        "frequencyPenalty": 0,
        "presencePenalty": 0
    }
}
```

> Import the configuration:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/20d0f55c-a138-4dd9-8d51-623e8b46d5ac">

## Variants Approach over Azure OpenAI

```mermaid
graph TD
    A[Create Azure OpenAI Resource] --> B[Configure Environment Variables]
    B --> C[Prepare Data]
    C --> D[Create Index in AI Studio]
    D --> E[Index Data]
    E --> F[Deploy Model in AI Studio]
    F --> G[Configure Variants]
    G --> H[Run and Evaluate Variants]
    H --> I[Interact with Model]
    I --> J[Monitor and Adjust]

    subgraph Indexing Phase
        direction TB
        C[Prepare Data]
        noteC[Ensure your data is in a suitable format and upload it to a supported storage service.]
        D[Create Index in AI Studio]
        noteD[Set up the index with parameters like chunk size, embedding model, and search type.]
        E[Index Data]
        noteE[Use the configured settings to index your data, creating embeddings.]
    end

    subgraph Deployment Phase
        direction TB
        F[Deploy Model in AI Studio]
        noteF[Set up your model deployment with parameters like model version, temperature, and top_p.]
        G[Configure Variants]
        noteG[Create and manage different versions of your prompt settings for fine-tuning.]
        H[Run and Evaluate Variants]
        noteH[Test different variants to determine the best configuration.]
        I[Interact with Model]
        noteI[Use the model with the selected variant settings.]
        J[Monitor and Adjust]
        noteJ[Continuously monitor performance and make adjustments as needed.]
    end

    subgraph Environment Configuration
        direction TB
        B[Configure Environment Variables]
        noteB[Set up your environment variables for your key and endpoint. This can be done in your development environment or directly in Azure AI Studio.]
    end
```

### Create an Azure OpenAI Resource
 - Go to the Azure portal.
 - Navigate to `Create a resource` and search for `Azure OpenAI`.
 - Follow the prompts to create your resource.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/785c4fc2-ff0a-452f-ae3c-346de1de0c3c">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/b779c283-b919-4b60-9b2f-7b6af466fd12">

### Setup your project
 
- **Navigate to Azure AI Studio**: Go to the Azure AI Studio and open your project.
   
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/d2713134-9cfd-4e67-b614-7484bdf9afd0">

- Create a project:
   
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/3c74f587-678b-4f86-9cdc-e487d6be396d">

### Indexing Your Data

- **Prepare Your Data**:
   - Ensure your data is in a suitable format (e.g., text, PDF).
   - Upload your data to Azure Blob Storage or another supported storage service.

   > If you don't have any yet see steps below:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/97584a49-e101-4851-b2c0-003db036e26d">

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/2ed7d569-1103-48a6-8952-28414d7e75ae">

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/8737301c-c560-4822-ae6c-bdfd61dcd2f2">

- **Index Your Data**:
   - Use the configured settings to index your data.
   - This process will break down your documents into smaller chunks and create embeddings.

    > Use AI Search directly:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/2b2b27e0-a203-48b0-9fa0-857a6b45251a">

    <img width="953" alt="image" src="https://github.com/user-attachments/assets/bcb0e547-04b4-41bc-8fa4-d3daca9368e2">

    > Create a new connection if it's required, for e.g you can use Access key or SAS (Shared Access Signature):
            
    <img width="143" alt="image" src="https://github.com/user-attachments/assets/1caa6937-9e97-4acd-95ba-cee79a2be318">

   > Follow the process:

   <img width="472" alt="image" src="https://github.com/user-attachments/assets/9a6cc9ed-2f01-4e0a-b134-425e942f99b9">

   > In Azure AI Studio:

   - Navigate to the `Indexes` section.
   - Select `Create Index` and configure the parameters such as chunk size, embedding model, and search type.
   - Save these settings for future use.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/821d06c9-5512-45c3-aa2b-e53c13ff25cd">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/f5ff72ed-9506-4674-b888-319ebb99d335">

### Deploy a Model
- In Azure AI Studio, go to the `Deployments` section.
- Select `Create Deployment` and choose your model (e.g., GPT-4).

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/1ee35693-3efa-45d2-b272-65890d9079a6">

- Configure deployment parameters like model version, temperature, and top_p.
- Save these deployment settings.

  <img width="331" alt="image" src="https://github.com/user-attachments/assets/fac5d4fb-c393-4d6f-ac0c-a4c84cca3e1f">

- Add your index data to the model:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/9fb56aad-842a-4767-aa4b-c7f5d7101c0b">

### Configure the prompt flow

> From the chat playground

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/96b0c8a8-5703-41ea-84c0-1d56e23295ff">

> Or you can:

 - Go to the `Prompt flow` section within your project.
 - Click on `Create` to start a new flow.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/ac29d845-5659-4c67-b7ca-218c865db3fb">

### Add an LLM Node

> [!NOTE]
> If you used `Prompt flow` section within your project, you need to add the LLM model but if you add the prompt flow from the chat playground you will see the LLM added, and other required elements as base for you.

> How to add the LLM:
 - In the flow creation wizard, add an LLM (Large Language Model) node.
 - Configure the initial settings for this node, such as the prompt and connection settings.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/95d1300d-1892-4fa0-a5b2-6113f1203d96">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/c1f9f7cf-abdc-4535-b0e7-30f709a91b93">

> How it looks from giving starting point:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/15e4e472-b03f-452d-8d51-e18978d82513">


### Configuring Variants in Azure AI Studio

> [!Note]
> Set up your environment variables for your key and endpoint. This can be done in your `development environment` or `directly in Azure AI Studio`.

> Using the approach of AI Studio

- **Show Variants**: Once your LLM node is set up, click on the `Show variants` button at the top right of the node. This will allow you to create and manage different variants of your prompt.
  
    <img width="504" alt="image" src="https://github.com/user-attachments/assets/229ba216-44cc-4e44-b3d3-cda6de347011">

#### Create Variants

> This allows you to fine-tune and test different configurations.

 - The existing LLM node will be labeled as `variant_0` by default.
 - Click on the `Clone` button on `variant_0` to generate `variant_1`.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/db8aced3-2f56-4c17-a0cc-1d1918c00ebc">

 - Configure `variant_1` with different parameters or update the prompt as needed.
 - Repeat this step to create additional variants (e.g., `variant_2`, `variant_3`, etc.).

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/bd952bd2-ee7f-44ee-ab77-78e3244357e7">

#### Configure Parameters for Each Variant
   - For each variant, you can adjust parameters such as temperature, top_p, and the prompt content.
   - Example configurations:
     - **Variant 0**: `Temperature = 1`, `Prompt: "Summarize the following text: {{input_text}}"`
     - **Variant 1**: `Temperature = 0.7`, `Prompt: "Summarize the following text: {{input_text}}"`
     - **Variant 2**: `Temperature = 1`, `Prompt: "What is the main point of this article? {{input_text}}"`
     - **Variant 3**: `Temperature = 0.7`, `Prompt: "What is the main point of this article? {{input_text}}"`


### Run and Evaluate Variants

 - After configuring your variants, use Azure AI Studio or API calls to interact with your deployed model. You can run the flow with different inputs to test how each variant performs.
 - Use the "Run" button to execute the flow and select the LLM node with variants to test.
 - Evaluate the outputs to determine which variant produces the best results for your use case.

### Monitor and Adjust

 - Continuously monitor the performance of each variant.
 - Make adjustments as needed based on the results to optimize your prompt configurations.


### Example Code Snippet

Here’s a simple example of how you might set up and use these settings programmatically:

```python
import openai

# Set up your environment variables
openai.api_key = "your-api-key"
endpoint = "https://your-endpoint.openai.azure.com/"

# Define your index settings
index_settings = {
    "chunk_size": 1024,
    "embedding_model": "text-embedding-ada-002",
    "search_type": "semantic"
}

# Define your deployment settings
deployment_settings = {
    "model": "gpt-4",
    "temperature": 0.7,
    "top_p": 0.9
}

# Save these settings for reuse
def save_settings(settings, filename):
    with open(filename, 'w') as file:
        json.dump(settings, file)

save_settings(index_settings, 'index_settings.json')
save_settings(deployment_settings, 'deployment_settings.json')

# Load and use the settings
def load_settings(filename):
    with open(filename, 'r') as file:
        return json.load(file)

index_settings = load_settings('index_settings.json')
deployment_settings = load_settings('deployment_settings.json')

# Use the settings in your API calls
response = openai.Completion.create(
    engine=deployment_settings["model"],
    prompt="Your prompt here",
    temperature=deployment_settings["temperature"],
    top_p=deployment_settings["top_p"]
)

print(response.choices[0].text)
```

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
