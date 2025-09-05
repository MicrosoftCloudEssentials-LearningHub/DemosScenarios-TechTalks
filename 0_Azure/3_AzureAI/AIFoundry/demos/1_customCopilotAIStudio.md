# Building a Custom AI Copilot with Azure AI Studio

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Azure OpenAI Service models available + preview)](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models)
- [Create and manage prompt flow compute sessions in Azure AI Studio](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/create-manage-compute-session)
- [Troubleshoot guidance for prompt flow](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/prompt-flow-troubleshoot)
- [Tutorial: Deploy an Enterprise Chat web app](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/deploy-chat-web-app)
- [Tutorial: Part 1 - Create resources for building a custom chat application with the prompt flow SDK](https://learn.microsoft.com/en-us/azure/ai-studio/tutorials/copilot-sdk-create-resources)
- [How to add and manage data in your Azure AI Studio project](https://learn.microsoft.com/en-us/azure/ai-studio/how-to/data-add)
- [8 steps to building an Azure OpenAI Copilot for your startup](https://startups.microsoft.com/blog/8-steps-to-building-an-azure-openai-copilot-for-your-startup/)
- [Build a RAG-based copilot solution with your own data using Azure AI Studio](https://learn.microsoft.com/en-us/training/modules/build-copilot-ai-studio/)

</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Creating an Azure AI Studio Resource with Azure Open Studio](#creating-an-azure-ai-studio-resource-with-azure-open-studio)
- [Create Compute](#create-compute)
- [Create a New Project in Azure AI Studio](#create-a-new-project-in-azure-ai-studio)
- [Choose a Model](#choose-a-model)
- [Add Your Data](#add-your-data)
- [Create a Prompt Flow](#create-a-prompt-flow)
- [Customize with Multiple Data Sources](#customize-with-multiple-data-sources)
- [Evaluate and Test](#evaluate-and-test)
- [Deploy Your Copilot](#deploy-your-copilot)
- [Monitor and Update](#monitor-and-update)

</details>

  
Find below some of the trending AI models in Azure AI Studio. You can use `model benchmarks` for guidance, to `assess model performance with evaluated metrics`.

| **Model Name**       | **Provider** | **Strengths**                                                                 |
|----------------------|--------------|-----------------------------------------------------------------------------|
| **o1-preview**       | OpenAI       | Excels in complex coding, math reasoning, brainstorming, and comparative analysis|
| **o1-mini**          | OpenAI       | Optimized for shorter context tasks, efficient in instruction following and workflow management|
| **gtp4o-mini**       | OpenAI       | Compact version of GPT-4, ideal for lightweight applications and faster response times|
| **GPT-4**            | OpenAI       | Large multimodal model, excels in text and image inputs, human-level performance on various benchmarks|
| **GPT-4o**           | OpenAI       | Multimodal model with real-time reasoning across audio, vision, and text, faster and more cost-effective|
| **Phi-2**            | Microsoft    | Efficient for general-purpose language tasks with better latency and lower costs|
| **Phi-3**            | Microsoft    | Most capable and cost-effective small language models, outperforming models of the same size and next size up across various benchmarks|
| **Phi-3-mini**       | Microsoft    | Small language model with a context window of up to 128K tokens, optimized for instruction following|
| **Phi-3-small**      | Microsoft    | 7B parameter model, excels in language, reasoning, coding, and math tasks|
| **Phi-3-medium**     | Microsoft    | 14B parameter model, offering high performance across a variety of tasks|
| **Orca 2**           | Microsoft    | Advanced language understanding and generation, suitable for nuanced text tasks|
| **Meta Llama 3**     | Meta         | Large-scale NLP tasks, pre-trained with billions of parameters for diverse applications|
| **Command R+**       | Cohere       | Retrieval-augmented generation, enhancing information retrieval and text generation|
| **Stable Diffusion 2.1** | Stability AI | High-quality image generation, robust for creative and design tasks|
| **JAIS**             | Core42       | Leading Arabic language model, optimized for Arabic NLP tasks|
| **Nixtla**           | Nixtla       | Specialized in time-series forecasting and anomaly detection|

## Creating an Azure AI Studio Resource with Azure Open Studio

- Sign in to Azure Portal
  1. Go to the Azure Portal.
  2. Sign in with your Azure subscription credentials.
- Create a New Resource
  1. In the Azure Portal, select `Create a resource`.
  2. Search for `Azure AI Studio` in the search bar.
  3. Select `Azure AI Studio` from the search results and click `Create`.
- Configure the Resource
  1. `Subscription:` Choose your Azure subscription.
  2. `Resource Group:` Select an existing resource group or create a new one.
  3. `Region:` Choose a region where the desired model is available.
  4. `Name:` Provide a unique name for your Azure AI Studio resource.
  5. `Pricing Tier:` Select the appropriate pricing tier (Standard is typically available).
- Configure how data will be stored: Is used as the default datastore for the AI hub. You may create a new Azure Storage resource or select an existing one in your subscription.
- Network Configuration: Choose the appropriate network security option:
   - `All networks:` Allows access from any network.
   - `Selected networks:` Restricts access to specific virtual networks.
   - `Disabled:` No network access (private endpoint connections only).
- Review and Create
  1. Review your configurations.
  2. Click `Create` to deploy the resource.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/b9e5b4c2-2d74-4d50-9be9-31b31d4f4694">

<img width="550" alt="image" src="https://github.com/user-attachments/assets/de646a19-be04-4fe8-8350-92d613043d79">

## Create Compute

- Make sure to create you compute, with your specifications and region availability of features considered.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/2159b327-718b-4e31-96fc-87583c74aa3d">

## Create a New Project in Azure AI Studio

- **Navigate to AI Studio**: Go to the Azure AI Hub created, anc launch the Azure AI Studio from the Azure portal.
    
    <img width="300" alt="image" src="https://github.com/user-attachments/assets/f491d6d5-a332-4518-ba14-7f931f4c9be9">

- **Create Project**: Click on `Create new project` and provide the necessary details like project name and description.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/b4e5c8f3-298d-4ab9-bb8e-7087d974e77a">

## Choose a Model

- **Model Catalog**: Browse the model catalog in Azure AI Studio.
- **Select Model**: Choose a model that fits your use case, for example gpt-4o-mini.
  
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/d7e96dd0-7e18-4bb4-9226-63a345632b1b">

## Add Your Data

- **Data Integration**: Integrate your own data into the model. This can include:
    - **Product Information**: Upload product catalogs or databases.
    - **Customer Data**: Include customer interaction logs or CRM data.

    | **Step**               | **Description**                                                                 |
    |------------------------|---------------------------------------------------------------------------------|
    | **Identify Data Sources** | - Product Information: Gather product catalogs, databases, or any relevant product data. <br/> - Customer Data: Collect customer interaction logs, CRM data, or any other customer-related information. |
    | **Prepare Data**       | - Format Data: Ensure your data is in a compatible format (e.g., CSV, JSON, SQL databases). <br/> - Clean Data: Remove any inconsistencies or irrelevant information to improve data quality. |
    | **Upload Data**        | - Azure Blob Storage: Upload your data to Azure Blob Storage for easy access and integration. <br/> - Azure Data Lake: Alternatively, use Azure Data Lake for large-scale data storage and analytics. |

- **Data Sources**: Use Azure Data Factory or other data integration tools to connect your data sources.

  | **Method**               | **Description**                                                                 |
  |------------------------|---------------------------------------------------------------------------------|
  | **Use Azure Data Factory**       | - Create Data Pipelines: Set up data pipelines in Azure Data Factory to automate the data integration process. <br/>   - Connect Data Sources: Use built-in connectors to link various data sources (e.g., SQL databases, Blob Storage, REST APIs). <br/>   - Transform Data: Apply data transformation steps as needed to prepare the data for integration. |
  | **Direct Integration** | - APIs: Use APIs to directly integrate data from external sources into your Azure AI Studio project. <br/>   - Custom Scripts: Write custom scripts (e.g., in Python) to fetch and process data before integrating it into the model. |
  | `Data Validation`   | - Check Data Quality: Validate the integrated data to ensure it meets the required standards. <br/>   - Test Integration: Run tests to confirm that the data is correctly integrated and accessible by the model. |

- Add your data: Create the connection if required, if you already have it, you can you can select your data.

  <img width="650" alt="image" src="https://github.com/user-attachments/assets/b0c50db6-c16c-48fd-98ff-c68354de030d">

- Validate your data was uploaded:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/6b350e0c-6c0b-41d7-aa10-e948c20f06db">

## Create a Prompt Flow

>  You can use the prompt flow feature to design how your copilot will interact with users.

- **Design Interaction**
  1. **Open Prompt Flow Designer**: In Azure AI Studio, navigate to the Prompt Flow Designer.
  2. **Define User Scenarios**: Identify the key scenarios and user intents your copilot will handle.
  3. **Map User Journey**: Outline the user journey, including initial greetings, main interactions, and possible end points.
      - Set Up Prompts:
        1. **Initial Prompts**: Define the initial prompts that will greet the user and set the context.
           - Example: "Hello! How can I assist you today?"
        2. **Expected Responses**: Specify the expected user responses and how the copilot should handle them.
           - Example: If the user asks for product information, the copilot should provide details from the product catalog.
    
        <img width="650" alt="image" src="https://github.com/user-attachments/assets/5674399a-387c-4460-9204-3638fd81259b">
  
      - Branching Logic
        1. **Create Branches**: Set up branches for different user inputs and scenarios.
           - Example: If the user asks about order status, branch to the order status flow.
        2. **Conditional Logic**: Use conditional logic to handle various user inputs and direct the conversation accordingly.
           - Example: If the user provides an order number, fetch the order status; if not, prompt for the order number.

        <img width="650" alt="image" src="https://github.com/user-attachments/assets/ea16950b-bdc8-48ce-bae2-b7b828417297">

        <img width="650" alt="image" src="https://github.com/user-attachments/assets/bcd8a863-b4a7-4658-b057-93950c793119">

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/21e506bb-b16f-483f-a06d-c48b7cb86e2b">

## Customize with Multiple Data Sources

- Enhance Responses: Integrate multiple data sources to provide more accurate and comprehensive responses.
    1. **Identify Data Sources**: Determine which data sources will enhance your copilot's responses.
      - Example: Product catalogs, customer databases, FAQs.
    2. **Integrate Data**: Use APIs or data connectors to integrate these data sources into your copilot.
- Enhance search: 
    - Azure AI Search: To index and search your data.
        1. **Set Up AI Search**: Create an Azure AI Search resource.
        2. **Index Data**: Index your data sources to make them searchable.
          - Example: Index product information, customer queries, and knowledge base articles.
    - Hybrid Search: Combine semantic search with traditional keyword search for better results.
        1. **Combine Searches**: Implement hybrid search to combine semantic search with traditional keyword search.
        2. **Optimize Search Results**: Fine-tune the search algorithms to provide the most relevant results.
          - Example: Use semantic search for understanding user intent and keyword search for specific terms.

## Evaluate and Test

- Evaluation Dataset: Use a question and answer evaluation dataset to test your copilot's performance.
    1. **Create Dataset**: Compile a dataset of questions and answers to evaluate your copilot.
    2. **Upload Dataset**: Upload this dataset to Azure AI Studio for evaluation purposes.
- Testing methods:
    - Manual Testing: Test the copilot with various queries.
        1. **Simulate User Queries**: Manually test the copilot by simulating various user queries.
        2. **Review Responses**: Evaluate the copilot's responses for accuracy and relevance.
    - Automated Testing: To continuously evaluate performance.
        1. **Set Up Tests**: Create automated tests to continuously evaluate the copilot's performance.
        2. **Run Tests Regularly**: Schedule regular test runs to ensure ongoing performance.
- Adjustments: Make necessary adjustments based on test results to improve accuracy and relevance. 
    1. **Analyze Results**: Analyze test results to identify areas for improvement.
    2. **Make Adjustments**: Adjust the prompt flows, data integration, and search algorithms as needed.

## Deploy Your Copilot

- Deployment Endpoint: **Create Endpoint**: Deploy your copilot to an endpoint for user access.
   - Example: Use Azure Functions to create a serverless endpoint.

    <img width="650" alt="image" src="https://github.com/user-attachments/assets/6fdea045-0016-4e23-864b-9473bf64e60d">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/93b84375-b404-4ce5-97bc-8015bf6fdc68">

    <img width="650" alt="image" src="https://github.com/user-attachments/assets/6a4e0ab5-b02c-488b-a9b6-7cf2f70ce7e7">

- Azure Functions: To create a serverless endpoint
  1. **Set Up Functions**: Create Azure Functions to handle specific tasks, such as fetching data or processing user inputs.
  2. **Integrate with Copilot**: Ensure these functions are integrated with your copilot's prompt flow.
- API Management: Manage and secure your API with Azure API Management.
  1. **Create API**: Use Azure API Management to create and manage your copilot's API.
  2. **Secure API**: Implement security measures, such as API keys and authentication, to protect your API.

## Monitor and Update

- Performance Monitoring: Continuously monitor your copilot's performance using Azure Monitor.
  1. **Set Up Monitoring**: Use Azure Monitor to track your copilot's performance.
  2. **Define Metrics**: Identify key metrics to monitor, such as response time, accuracy, and user satisfaction.
- Metrics and Logs: Track key metrics and logs to identify issues.
  1. **Track Metrics**: Continuously track the defined metrics to identify any issues.
  2. **Analyze Logs**: Review logs to understand user interactions and identify potential improvements.
- Alerts: Set up alerts for critical issues.
  1. **Set Up Alerts**: Configure alerts for critical issues, such as downtime or performance degradation.
  2. **Respond to Alerts**: Quickly respond to alerts to maintain optimal performance.
- Regular Updates: Update your copilot with new data or improved prompt flows as needed.
  1. **Incorporate Feedback**: Regularly update your copilot based on user feedback and new data.
  2. **Refine Prompt Flows**: Continuously refine the prompt flows to improve user interactions.
- Feedback Loop: Incorporate user feedback to refine and enhance the copilot.
  1. **Collect Feedback**: Implement mechanisms to collect user feedback.
  2. **Iterate and Improve**: Use this feedback to iteratively improve your copilot.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
