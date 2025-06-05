# Azure AI Foundry

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-02

----------

> You can create and manage Azure resources for Azure AI Studio via the Azure portal. 

> [!IMPORTANT]
> Please be aware that prior to being named AI Studio, AI Foundry introduced new components and optimized the backend operations.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Introducing Meta Llama 3 Models on Azure AI Model Catalog](https://techcommunity.microsoft.com/t5/ai-machine-learning-blog/introducing-meta-llama-3-models-on-azure-ai-model-catalog/ba-p/4117144)
- [Meta’s next generation model, Llama 3.1 405B is now available on Azure AI](https://techcommunity.microsoft.com/t5/ai-ai-platform-blog/meta-s-next-generation-model-llama-3-1-405b-is-now-available-on/ba-p/4198379)
- [Model benchmarks in Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/model-benchmarks)
- [What are Azure AI services?](https://learn.microsoft.com/en-us/azure/ai-services/what-are-ai-services)
- [Azure AI Studio architecture](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/architecture)
- [Role-based access control in Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/rbac-ai-studio)
- [Collaboratively build AI apps and share resources with hubs and projects](https://techcommunity.microsoft.com/t5/ai-ai-platform-blog/collaboratively-build-ai-apps-and-share-resources-with-hubs-and/ba-p/4153938)
- [Deploy models, flows, and web apps with Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/deployments-overview)
- [How to deploy Azure OpenAI models with Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/deploy-models-openai)
- [How to evaluate generative AI models and applications with Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/evaluate-generative-ai-app)
- [What is Azure AI Foundry?](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry#which-type-of-project-do-i-need) - Which type of project do I need? Hub or Project

</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Overview](#overview)
   - [Model Catalog](#model-catalog)
   - [Model Benchmarks](#model-benchmarks)
   - [Azure AI Services](#azure-ai-services)
- [Architecture](#architecture)
   - [AI Hub](#ai-hub)
   - [Projects](#projects)
   - [AI Studio SDK](#ai-studio-sdk)
   - [RBAC and Permissions](#rbac-and-permissions)
   - [Networking](#networking)
- [Project playground](#project-playground)
   - [Chat](#chat)
   - [Assistants](#assistants)
   - [Images](#images)
   - [Completions](#completions)
- [Tools](#tools)
   - [Code](#code)
   - [Prompt Flow](#prompt-flow)
   - [Tracing](#tracing)
   - [Evaluation](#evaluation)
   - [Fine-tunning](#fine-tunning)
- [Components](#components)
   - [Data](#data)
   - [Indexes](#indexes)
   - [Content Filter](#content-filter)
   - [Deployments](#deployments)

</details>

## Overview 

- Provides a trusted and inclusive platform that empowers developers of all abilities and preferences to innovate with AI and shape the future.
- Seamlessly explore, build, test, and deploy using cutting-edge AI tools and ML models, grounded in responsible AI practices.
- Build together as one team.
- Improve customer experiences, reduce organizational risk, improve work quality, enhance productivity and efficiency.
- Built-in security and compliance investing USD20 billion in cybersecurity.
- 8,500 security and threat intelligence experts compliance certification portfolios.

  <img width="709" alt="image" src="https://github.com/brown9804/MSCloudEssentials_LPath/assets/24630902/ad165c2c-94ee-455d-8c90-55f56fb119b9"> 
  
  [image from](https://www.slideshare.net/slideshow/azure-ai-platform-automated-ml-workshop/133115961)

  | **Feature** | **Azure AI Foundry** | **Azure OpenAI** |
  |-------------|----------------------|------------------|
  | **Scope** | Comprehensive platform for building, testing, and deploying generative AI applications | Specific service providing access to OpenAI's models |
  | **Model Catalog** | Includes models from OpenAI, Hugging Face, Meta, and more | Focuses on OpenAI models like GPT-4, Codex, and DALL-E |
  | **Collaboration** | Provides a collaborative environment with shared files and connections to pretrained models, data, and compute resources | Offers a playground for experimenting with OpenAI models |
  | **Tools** | Supports LLMOps for generative AI solutions, including evaluation, connection management, and flow logic | Allows users to manage deployments and models directly through the Azure OpenAI Studio |
  | **Use Cases** | Suitable for a wide range of AI applications, including text, image, and document processing | Primarily for text generation, summarization, translation, and question answering |

### Model Catalog 

> The Model Catalog in Azure AI Foundry is a `central hub where you can discover, evaluate, and deploy a wide range of AI models`. It includes models from various providers such as Azure OpenAI Service, Mistral, Meta, Cohere, NVIDIA, and Hugging Face, as well as models trained by Microsoft.

<p float="left">
  <img src="https://github.com/user-attachments/assets/5d83afb8-9924-49f1-aebc-3ce90c58c58f" width="450" height="250" />
  <img src="https://github.com/user-attachments/assets/ab6f3f19-dafb-413f-8b9d-fe73dc4dd420" width="450" height="250" />
</p>

The model catalog offers two distinct `ways to deploy models` for your use:
- Managed Compute
- Serverless API.
  
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/1f6d2b05-be72-46ed-bb2a-4141c4eadf6b">

| **Type of Model**            | **Description**                                                                 | **Examples**                          |
|------------------------------|---------------------------------------------------------------------------------|---------------------------------------|
| Curated by Azure AI          | Popular non-Microsoft models optimized for Azure AI platform.                   | Models from Hugging Face, NVIDIA      |
| Azure OpenAI Models          | Exclusive models available through Azure OpenAI Service, supported by Microsoft.| GPT-4, Codex, DALL-E                  |
| Open Models from Hugging Face| Hundreds of models from the Hugging Face hub, available for real-time inference. | Various NLP and vision models         |

### Model Benchmarks

> Model Benchmarks in Azure AI Studio is a feature that allows users to compare the performance of various AI models. This tool helps you make informed decisions about which model best suits your specific task by providing a comprehensive comparison of benchmarking metrics.

| Key Aspect                  | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| Comparison of Models        | Compare LLMs and SLMs based on metrics like accuracy, coherence, fluency, and GPT (Generative Pre-trained Transformer) similarity this metric is particularly useful when comparing the performance of different language models. |
| Quality and Embeddings Benchmarks | Evaluate models based on quality and embeddings benchmarks.              |
| Efficiency                  | Reduce development time and infrastructure costs by identifying the most suitable model quickly. |
| User-Friendly               | Accessible within the same environment where you build, train, and deploy AI solutions. |

### Azure AI Services

> Azure AI Services is a comprehensive suite of AI tools and services provided by Microsoft to help developers and organizations build intelligent applications.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/823714d5-ccda-43c8-9fc8-3188c5fa5a7c">

| Service                     | Description                                                                 | Use Cases                                                                                  |
|-----------------------------|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| **Azure OpenAI Service**    | Provides access to powerful language models like GPT-3 and GPT-4.           | Text generation, summarization, translation, conversational AI.                            |
| **Azure AI Vision**         | Offers image and video analysis capabilities, including OCR and object detection. | Image tagging, content moderation, automated document processing.                          |
| **Azure AI Speech**         | Converts speech to text, text to speech, and offers speech translation and speaker recognition. | Voice assistants, transcription services, real-time translation.                           |
| **Azure AI Language**       | Tools for natural language understanding, including sentiment analysis and entity recognition. | Chatbots, sentiment analysis for customer feedback, multilingual support.                  |
| **Azure AI Search**         | Enhances search capabilities with AI-powered indexing and retrieval.        | Enterprise search solutions, e-commerce search, knowledge management.                      |
| **Azure AI Content Safety** | Detects and filters offensive or inappropriate content in text and images.  | Content moderation for social media platforms, forums, online communities.                 |
| **Azure AI Translator**     | Real-time translation of text and documents across more than 100 languages. | Multilingual communication, document translation, global customer support.                 |
| **Azure AI Document Intelligence** | Extracts text, key-value pairs, tables, and structures from documents. | Automated data entry, document digitization, information extraction.                       |
| **Azure AI Video Indexer**  | Analyzes video content to extract insights and metadata.                    | Video content management, automated tagging, content search.                               |
| **Azure Bot Services**      | Develops intelligent, enterprise-grade bots.                                | Customer service bots, virtual assistants, interactive chatbots.                           |
| **Azure Custom Vision**     | Customizes image classification and object detection models.                | Specialized image recognition tasks, custom object detection.                              |
| **Azure Face API**          | Detects and recognizes human faces in images.                               | Facial recognition, emotion detection, identity verification.                              |
| **Azure Immersive Reader**  | Improves reading comprehension with tools that read text aloud, translate, and highlight. | Education, accessibility, language learning.                                               |

## Architecture 

### AI Hub

> The AI Hub is the central resource in Azure AI Studio. It provides a unified experience for AI developers and data scientists to build, evaluate, and deploy AI models. The hub manages security configurations, compute resources, and connections to other Azure services like Azure OpenAI and Azure AI services. It offers several key features:

| Feature                        | Description                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------|
| **Security Configuration**     | The hub manages security settings, including virtual network setups, customer-managed keys, managed identities, and policies. |
| **Compute Resources**          | It provides compute resources for interactive development, fine-tuning, open-source, and serverless model deployments. |
| **Connections to Azure Services** | The hub can connect to other Azure services like Azure OpenAI, Azure AI services, and Azure AI Search. These connections are shared with projects created from the hub. |
| **Project Management**         | A hub can manage multiple child projects, each inheriting the hub's security settings and shared resource access. |

> Setting Up an AI Hub:

1. **Navigate to Azure AI Studio**: Open the Azure portal and go to Azure AI Studio.
2. **Create a New Hub**:
   - Click on `Create a resource` and search for `AI Hub`.
   - Select `AI Hub` and click `Create`.
3. **Configure Basic Settings**:
   - Enter the hub name, subscription, and resource group.
   - Choose the region where you want to deploy the hub.
4. **Set Up Security**: Configure virtual networks, managed identities, and customer-managed keys as needed.
5. **Add Connections**: Connect to other Azure services like Azure OpenAI, Azure AI services, and Azure AI Search.
6. **Review and Create**: Review your settings and click `Create` to deploy the hub.
     
### Projects

> Projects are child resources of the AI Hub. They act as workspaces where you can develop and deploy AI systems. Projects inherit the security settings and shared resource access from the hub, allowing for consistent and secure development environments. Key aspects include:

| Key Aspect                     | Description                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------|
| **Development Tools**          | Projects provide access to tools for building and customizing AI applications. |
| **Reusable Components**        | They offer reusable components such as datasets, models, and indexes. |
| **Isolated Containers**        | Projects have isolated containers for data upload, ensuring data security and privacy. |
| **Project-Scoped Connections** | These connections allow project members to access specific data and resources without affecting other projects. |

>  Creating a Project within an AI Hub:

1. **Navigate to Your AI Hub**: Open the AI Hub you created.
2. **Create a New Project**:
   - Click on `New Project`.
   - Enter the project name and description.
3. **Configure Project Settings**:
   - Select the compute resources and storage options.
   - Set up any necessary connections to datasets or models.
4. **Set Permissions**: Assign roles to team members (e.g., Contributor, Reader).
5. **Review and Create**: Review your settings and click `Create` to set up the project.
   
### AI Studio SDK

> The AI Studio SDK provides tools and libraries for developers to interact programmatically with Azure AI Studio. It allows for the automation of tasks such as model training, deployment, and management, making it easier to integrate AI capabilities into applications. It supports:

| Key Aspect     | Description                                                                                          |
|----------------|------------------------------------------------------------------------------------------------------|
| **Automation** | Automate tasks like model training, deployment, and management.                                      |
| **Integration**| Easily integrate AI capabilities into applications, streamlining the development process.            |
| **Flexibility**| The SDK supports various programming languages and frameworks, making it adaptable to different development environments. |

> Using the AI Studio SDK:
1. **Install the SDK**: Use pip to install the SDK: `pip install azure-ai-studio-sdk`.
2. **Authenticate**: Set up authentication using Azure CLI or a service principal.
3. **Initialize the SDK**:
   ```python
   from azure.ai.studio import AIStudioClient
   client = AIStudioClient(subscription_id, resource_group, hub_name)
   ```
4. **Perform Operations**: Example: Train a model
     ```python
     model = client.models.create_or_update(model_name, model_config)
     client.models.train(model)
     ```
     
### RBAC and Permissions

> Role-Based Access Control (RBAC) in Azure AI Studio is used to manage access to resources. There are built-in roles like Owner, Contributor, and Azure AI Developer, each with specific permissions. The hub and projects have different levels of access, ensuring that users can only perform actions they are authorized for. Key points include:

| Key Aspect              | Description                                                                                          |
|-------------------------|------------------------------------------------------------------------------------------------------|
| **Built-in Roles**      | There are built-in roles such as Owner, Contributor, and Azure AI Developer, each with specific permissions. |
| **Owner**               | Full access to the hub, including managing and creating new hubs and assigning permissions.           |
| **Contributor**         | Full access to the hub, but cannot manage hub permissions.                                            |
| **Azure AI Developer**  | Can perform all actions except creating new hubs and managing hub permissions.                        |
| **Hub vs. Project Access** | The hub manages infrastructure and security, while projects focus on development and deployment.       |

> Setting Up RBAC:
1. **Navigate to Your AI Hub**: Open the AI Hub in the Azure portal.
2. **Access IAM (Identity and Access Management)**: Click on `Access control (IAM)`.
3. **Add Role Assignments**:
   - Click on `Add` and select `Add role assignment`.
   - Choose a role (e.g., Owner, Contributor, Azure AI Developer).
   - Assign the role to a user or group.
4. **Review and Save**: Review the role assignment and click `Save`.
   
### Networking

> Networking in Azure AI Studio involves setting up secure connections between the hub, projects, and other Azure services. This includes configuring virtual networks, managed identities, and policies to ensure secure and efficient communication between resources. This includes:

| Key Aspect            | Description                                                                                          |
|-----------------------|------------------------------------------------------------------------------------------------------|
| **Virtual Networks**  | Configuring virtual networks to ensure secure communication between resources.                       |
| **Managed Identities**| Using managed identities for secure access to resources without managing credentials.                |
| **Policies**          | Implementing policies to control and monitor network traffic, ensuring compliance and security.       |

> Configuring Networking:
1. **Set Up Virtual Networks**:
   - In the Azure portal, navigate to `Virtual networks` and create a new virtual network.
   - Configure subnets and network security groups as needed.
2. **Integrate with AI Hub**:
   - Go to your AI Hub and click on `Networking`.
   - Select the virtual network you created.
3. **Configure Managed Identities**: Enable managed identities for secure access to resources.
4. **Set Up Policies**: Implement policies to control and monitor network traffic.

## Project playground 

> The `Project Playground` in Azure AI Studio is a feature that `allows developers and data scientists to experiment with and fine-tune AI models in a controlled environment`. The playground helps users understand how models behave and allows for iterative testing and development before integrating these models into production applications. It provides a unified interface for interacting with various AI capabilities, such as: 

| Feature     | Key Features                                                                 |
|-------------|------------------------------------------------------------------------------|
| **Chat**    | Real-time interaction, speech-to-text, text-to-speech, customizable responses|
| **Assistants** | Pre-built models, customizable behavior, integration with other services   |
| **Images**  | Image generation from text prompts, customizable parameters, high-quality outputs |
| **Completions** | Text generation, prompt-based completions, customizable settings          |

### Chat

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy a Chat Model**: Navigate to the project, select `Deploy Model`, and choose an Azure OpenAI model.
3. **Configure Chat Playground**: Go to `Playground` > `Chat`, select your deployed model, and configure settings.
4. **Enable Speech Features**: In `Playground Settings`, enable `Speech to Text` and `Text to Speech` if needed.
5. **Start a Chat Session**: Use the microphone button to speak to the assistant or type your message and send.

### Assistants

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy an Assistant Model**: Navigate to the project, select `Deploy Model`, and choose an assistant model.
3. **Configure Assistant Settings**: Go to `Playground` > `Assistants`, select your deployed model, and configure settings.
4. **Customize Responses**: Use the settings to customize the assistant's responses and behavior.
5. **Test the Assistant**: Interact with the assistant in the playground to ensure it behaves as expected.

### Images

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy an Image Model**: Navigate to the project, select `Deploy Model`, and choose an image generation model.
3. **Configure Image Playground**: Go to `Playground` > `Images`, select your deployed model, and configure settings.
4. **Generate Images**: Enter prompts or parameters to generate images using the model.
5. **Review and Save**: Review the generated images and save or adjust the prompts as needed.

### Completions

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy a Completion Model**: Navigate to the project, select `Deploy Model`, and choose a completion model.
3. **Configure Completion Playground**: Go to `Playground` > `Completions`, select your deployed model, and configure settings.
4. **Generate Text Completions**: Enter prompts or text snippets to generate completions using the model.
5. **Review and Adjust**: Review the generated completions and adjust the prompts or settings as needed.


## Tools 

| Tool          | Description                                                                 | Key Features                                                                                       |
|---------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **Code**      | The `Code` tool allows you to write, test, and debug code directly within Azure AI Studio. | - `Interactive Development`: Write, test, and debug code. <br> - `Integration with Notebooks`: Use Jupyter Notebooks for interactive data analysis and model development. <br> - `Version Control`: Integrate with Git for version control and collaboration. |
| **Prompt Flow** | `Prompt Flow` provides a visual interface for creating and managing AI workflows. | - `Visual Workflow`: Create and manage AI workflows using a visual interface. <br> - `Prompt Engineering`: Design and test prompts for large language models (LLMs). <br> - `Flow Variants`: Create and compare multiple prompt variants to optimize performance. |
| **Tracing**   | `Tracing` is a debugging and performance monitoring tool.                   | - `Debugging`: Trace the execution of your AI workflows to identify and fix issues. <br> - `Logging`: Capture detailed logs of workflow execution for analysis. <br> - `Performance Monitoring`: Monitor the performance of your AI models and workflows. |
| **Evaluation**| The `Evaluation` tool offers built-in and custom evaluators to assess the performance and quality of your AI models. | - `Built-in Evaluators`: Use built-in evaluators to assess model performance. <br> - `Custom Evaluators`: Create custom evaluators tailored to your specific needs. <br> - `Comprehensive Metrics`: Evaluate models using a variety of metrics, including accuracy, relevance, and safety. |
| **Fine-Tuning**| `Fine-Tuning` allows you to customize pre-trained models to better fit your specific use case. | - `Model Customization`: Fine-tune pre-trained models to better fit your specific use case. <br> - `Data Integration`: Use your own datasets to fine-tune models. <br> - `Performance Improvement`: Enhance model performance by tailoring it to your data. |

### Code

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Open the Code Editor**: Navigate to the project and select `Code` from the menu.
3. **Write Your Code**: Use the integrated code editor to write and test your code.
4. **Run and Debug**: Execute your code and use debugging tools to troubleshoot any issues.
5. **Save and Version Control**: Save your code and commit changes to your Git repository if integrated.

### Prompt Flow

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Open Prompt Flow**: Navigate to the project and select `Prompt Flow` from the menu.
3. **Create a New Flow**: Click on `New Flow` and choose a template or start from scratch.
4. **Design Your Flow**: Use the visual editor to add and configure nodes, including prompts and actions.
5. **Test and Iterate**: Run your flow, test different prompt variants, and iterate based on results.
   
### Tracing

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Enable Tracing**: Navigate to the project settings and enable tracing for your workflows.
3. **Run Your Workflow**: Execute your AI workflow and let tracing capture the execution details.
4. **Analyze Logs**: Review the captured logs to identify any issues or performance bottlenecks.
5. **Debug and Optimize**: Use the insights from tracing to debug and optimize your workflows.

### Evaluation

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy a Model**: Navigate to the project, select `Deploy Model`, and choose a model to evaluate.
3. **Open Evaluation**: Go to `Evaluation` in the project menu.
4. **Select Evaluators**: Choose built-in or custom evaluators to assess your model.
5. **Run Evaluation**: Execute the evaluation and review the results to understand your model's performance.

### Fine-tunning

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Upload Your Data**: Navigate to the project and upload your dataset.
3. **Select a Model**: Choose a pre-trained model to fine-tune.
4. **Configure Fine-Tuning**: Set up the fine-tuning parameters, including learning rate, epochs, and batch size.
5. **Run Fine-Tuning**: Execute the fine-tuning process and monitor the progress.
6. **Evaluate and Deploy**: Evaluate the fine-tuned model and deploy it if it meets your performance criteria.

## Components 

| Component       | Description                                                                 | Key Features                                                                                       |
|-----------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **Data**        | Manages and utilizes datasets for AI model training and evaluation.         | - **Data Ingestion**: Import data from various sources, including Azure Blob Storage, SQL databases, and external APIs. <br> - **Data Preprocessing**: Clean, transform, and prepare data using built-in tools and custom scripts. <br> - **Data Storage**: Securely store datasets with support for versioning and access control. |
| **Indexes**     | Organizes and retrieves data efficiently, especially for search tasks.      | - **Index Creation**: Create indexes on various data fields to optimize search and retrieval. <br> - **Search Capabilities**: Perform fast and accurate searches across indexed data. <br> - **Integration**: Integrate indexes with other Azure services, such as Azure Cognitive Search. |
| **Content Filter** | Ensures that the content generated by AI models is safe and appropriate.  | - **Default Content Filter**: Automatically detect and block harmful content. <br> - **Custom Content Filters**: Create and configure custom content filters. <br> - **Language Support**: Supports multiple languages, including English, German, Japanese, Spanish, French, Italian, Portuguese, and Chinese. |
| **Deployments** | Makes AI models, workflows, and applications available for production use.  | - **Model Deployment**: Deploy large language models (LLMs) and other AI models as APIs. <br> - **Serverless Deployment**: Deploy models as serverless APIs, billed per usage. <br> - **Managed Infrastructure**: Host models on managed infrastructure with virtual machines and capacity management. <br> - **Integration**: Integrate deployed models with other applications and services. |

### Data 

> The `Data` component in Azure AI Studio is essential for managing and utilizing datasets for AI model training and evaluation. It provides tools for data ingestion, preprocessing, and storage, ensuring that your data is ready for AI workflows.

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Upload Data**: Navigate to the project, select `Data`, and click `Upload Data`. Choose your data source and follow the prompts to import your dataset.
3. **Preprocess Data**: Use the built-in tools or custom scripts to clean and transform your data as needed.
4. **Store Data**: Save your processed data within the project, ensuring it is versioned and access-controlled.

### Indexes 

> `Indexes` in Azure AI Studio are used to organize and retrieve data efficiently. They are particularly useful for search and retrieval tasks, enabling quick access to relevant information within large datasets.

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Upload Data**: Navigate to the project, select `Data`, and upload your dataset.
3. **Create an Index**: Go to `Indexes`, click `Create Index`, and select the fields you want to index.
4. **Configure Search**: Set up search parameters and options to optimize retrieval.
5. **Test and Use**: Perform searches on your indexed data to ensure it meets your requirements.

### Content Filter

> The `Content Filter` component in Azure AI Studio is designed to ensure that the content generated by AI models is safe and appropriate. It uses classification models to detect and filter harmful content in both input prompts and output completions.

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Navigate to Content Filters**: In your project, go to the `Content Filters` tab.
3. **Create a Content Filter**: Click `Create Content Filter`, enter a name, and select a connection.
4. **Configure Input Filters**: Set the action and severity level threshold for each filter type on the input prompt.
5. **Configure Output Filters**: Set the action and severity level threshold for each filter type on the output content.
6. **Save and Apply**: Save your content filter settings and apply them to your model deployments.


### Deployments 

> `Deployments` in Azure AI Studio involve making AI models, workflows, and applications available for use in production environments. This includes hosting models on servers or in the cloud and creating APIs or other interfaces for users to interact with the models.

Types of deployments available in Azure AI Studio:

| **Deployment Method**       | **Description**                                                                 | **Billing Model**                      |
|-----------------------------|---------------------------------------------------------------------------------|----------------------------------------|
| Serverless API              | Deploy models as serverless APIs, accessible via endpoints without managing infrastructure. | Pay-as-you-go (per token/request)      |
| Models as a Service (MaaS)  | Managed service where models are hosted and maintained by Azure.                | Pay-as-you-go (per token)              |
| Models as a Platform (MaaP) | Deploy models on dedicated virtual machines (VMs) for more control over resources. | Billed as VMs per-hour                 |
| Flows and Web Applications  | Deploy models as part of larger workflows or web applications.                  | Varies based on usage                  |
| Managed Compute             | Use Azure's managed compute resources to deploy and run models.                 | Combination of compute and storage costs|

1. **Create a Project**: Go to Azure AI Studio, select `New Project`, enter a name, and choose a hub.
2. **Deploy a Model**: Navigate to the project, select `Deployments`, and click `+ Deploy model`.
3. **Select a Model**: Choose a model from the model catalog, such as an Azure OpenAI model.
4. **Configure Deployment**: Specify the deployment name and modify settings as needed.
5. **Deploy**: Click `Deploy` to make the model available as an API.
6. **Integrate and Use**: Use the generated API endpoint to integrate the deployed model with your applications.

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
