# Accessing Semantic Model from Sharepoint 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> A semantic index is an `advanced framework used to organize, interpret, and retrieve information based on its meaning` rather than just keyword matching.

## Wiki 
- [Working with SharePoint sites in Microsoft Graph](https://learn.microsoft.com/en-us/graph/api/resources/sharepoint?view=graph-rest-beta)
- [Microsoft Graph API for SharePoint Pages is now generally available](https://devblogs.microsoft.com/microsoft365dev/microsoft-graph-api-for-sharepoint-pages-is-now-generally-available/)
- [Semantic Index for Copilot | Microsoft Learn](https://learn.microsoft.com/en-us/microsoftsearch/semantic-index-for-copilot)
- [Expanding Copilot for Microsoft 365 to businesses of all sizes](https://www.microsoft.com/en-us/microsoft-365/blog/2024/01/15/expanding-copilot-for-microsoft-365-to-businesses-of-all-sizes/)
- [Azure AI Search: SharePoint Online indexer (preview) - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-howto-index-sharepoint-online#configure-the-sharepoint-online-indexer)
- [Announcing the Semantic Index for Copilot - M365 Admin](https://m365admin.handsontek.net/announcing-the-semantic-index-for-copilot/)
- [Microsoft 365 Copilot Wave 2: AI Innovations in SharePoint and OneDrive](https://techcommunity.microsoft.com/t5/microsoft-365-copilot/microsoft-365-copilot-wave-2-ai-innovations-in-sharepoint-and/ba-p/4245159)
- [Create a Semantic Model from a SharePoint List - Power BI](https://learn.microsoft.com/en-us/power-bi/connect-data/create-dataset-sharepoint-online-list)
- [How Microsoft 365 Copilot Can Work with Your External Data](https://techcommunity.microsoft.com/t5/microsoft-mechanics-blog/how-microsoft-365-copilot-can-work-with-your-external-data/ba-p/3937645)
- [Semantic Link: OneLake Integrated Semantic Models | Microsoft Fabric](https://support.fabric.microsoft.com/en-us/blog/semantic-link-onelake-integrated-semantic-models?ft=All)

## What is a Semantic Index?

| Feature                  | Description                                                                                                                |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Meaning-Based Retrieval  | Unlike traditional indexing, which relies on exact keyword matches, a semantic index understands the context and relationships between words and data points. This allows it to retrieve information that is semantically related, even if the exact keywords aren't present. |
| Vectorization            | It uses vectors, which are numerical representations of data points (like words, images, or other types of data). These vectors are arranged in a multi-dimensional space where semantically similar data points are clustered together. |
| Contextual Understanding | By leveraging natural language processing (NLP) and machine learning, a semantic index can understand the nuanced meanings and intentions behind text, making it possible to provide more relevant search results. |
| Scalability              | Semantic indexing can handle large volumes of data efficiently, making it suitable for big data applications. |
| Real-Time Processing     | Capable of processing and indexing data in real-time, allowing for up-to-date search results and insights. |
| Application Areas        | Used in various fields such as search engines, recommendation systems, and data analysis tools to improve accuracy and relevance. |

> The SharePoint Semantic Index is a feature within Microsoft 365 that enhances data retrieval and search capabilities specifically for SharePoint content. <br/>
> - **Data Mapping**: The SharePoint Semantic Index creates a map of your SharePoint data, identifying relationships and making important connections between different pieces of information. <br/>
> - **Vectorization**: It uses vectors (numerical representations of data points) to cluster semantically similar data points together. This allows for more advanced search capabilities beyond simple keyword matching. <br/>
> - **Contextual Relevance**: By understanding the context and relationships between data points, the semantic index helps provide more relevant and personalized search results.

## Overview 

| Category       | Information                                                                                                                                                                                                 |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Benefits       | - **Improved Search Results**: Provides more accurate and contextually relevant search results.<br/> - **Personalization**: Tailors search results based on individual user interactions and preferences.<br/> - **Efficiency**: Helps users find the information they need more quickly and efficiently.<br/> - **Intelligent Summarization**: Can generate summaries of lengthy documents by understanding core themes and key points.<br/> - **Context-Aware Assistance**: Offers contextually relevant suggestions and recommendations when drafting documents, emails, or presentations. |
| How it Works   | - **Content Categorization**: Categorizes and tags content based on themes, topics, and entities, creating a structured representation of the information.<br/> - **Relationship Mapping**: Maps relationships between different pieces of information, linking related documents, emails, and other data based on their content and context.<br/> - **Continuous Learning**: Utilizes machine learning algorithms to continuously learn from user interactions and feedback, improving its accuracy and relevance over time.<br/> - **Integration with Microsoft Graph**: Generated from content in Microsoft Graph, which includes data from SharePoint Online.<br/> - **Enhanced Search**: Supports enhanced search experiences by allowing users to find relevant content based on keywords, personal preferences, and social connections.<br/> - **Security and Compliance**: Respects organizational boundaries and is built on Microsoft’s comprehensive approach to security, compliance, and privacy. |
| Applications   | - **Enhanced Search Engines**: Used in search engines to provide more relevant results based on user queries.<br/> - **AI Assistants**: Powers AI assistants like Microsoft Copilot to understand and respond to user queries more effectively.<br/> - **Data Analysis**: Helps in organizing and analyzing large volumes of data by understanding the relationships and context within the data. |

## How to build the Semantic Model from Sharepoint 

> Review first:

- Go to search and offline availability:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/d51d7d72-071e-4f9b-a493-3977867eb7a7">

  - Make sure you have all permissions, required:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/a9261c2f-1605-4656-af43-4e6da93ba289">

## How to accessing the Semantic Index 

Find below more information about how to access the Semantic Index, like within your custom chatbots or through Copilot:

1. **Using Azure AI Search**: Azure AI Search can be used to index SharePoint content and provide semantic search capabilities.
   - Set Up Azure AI Search: Create an Azure Cognitive Search service in the Azure portal.
   - Configure SharePoint Indexer:
        - Set up a SharePoint Online indexer to automate the indexing of document library content.
        - Click [here](https://learn.microsoft.com/en-us/azure/search/search-howto-index-sharepoint-online) for detailed steps on configuring the indexer in Sharepoint.
   - Define Index Schema: Define the schema for your index, specifying the fields and their data types.
   - Run the Indexer:
        - Run the indexer to start indexing your SharePoint content.
        - Use the Azure portal to monitor the indexing process and ensure it completes successfully.
   - Query the Index: Use the Azure Cognitive Search API to query the indexed data and retrieve relevant results.
2. `Microsoft 365 Copilot`: Create `Copilot Agents` within SharePoint to automate tasks and answer questions based on the semantic index. This feature allows you to build custom agents without coding, making it easier to integrate with your workflows.
3. `Custom Chatbots`:
   - `Microsoft Bot Framework`: Create a bot using the Microsoft Bot Framework, integrate it with Microsoft Graph API to access SharePoint data, and use the semantic search capabilities provided by the Semantic Index to enhance the bot's responses.
        - Create a bot using the Microsoft Bot Framework.
        - Integrate the bot with Microsoft Graph API to access SharePoint data.
        - Use the semantic search capabilities provided by the Semantic Index to enhance the bot's responses.
   - `Power Virtual Agents`: Create a chatbot using Power Virtual Agents, connect it to SharePoint using Power Automate flows, and leverage the Semantic Index to provide more accurate and contextually relevant responses.
        - Create a chatbot using Power Virtual Agents.
        - Connect the bot to SharePoint using Power Automate flows.
        - Leverage the Semantic Index to provide more accurate and contextually relevant responses.
4. `Using Microsoft Graph API` to access the Semantic Index for SharePoint: Set up a Microsoft Graph Connector for SharePoint to index your SharePoint content and bring the semantic index data into your custom applications. You can use methods like the Power Bi, SemPy library, data pipelines, or Power Automate
 
  > Conditions for Viability: 
  > - API Availability: Ensure the Microsoft Graph API supports the specific functionality you need. While the API for accessing SharePoint Pages is generally available, specific features like querying the semantic index might still be in development or limited to certain environments. <br/> 
  > - Permissions: Your application must have the necessary permissions to access SharePoint data. This involves registering your application in the Azure AD portal and configuring the appropriate permissions. <br/> 
  > - Environment: The API's functionality can vary based on the environment (e.g., standard multi-tenant cloud, GCC, GCC High, DoD). Verify that the API features you need are supported in your specific environment. <br/> 
  > - Authentication: Proper authentication using OAuth 2.0 is required to obtain an access token that grants permission to query the semantic index. <br/> 
  > - Configuration: Ensure your SharePoint and Microsoft 365 setup allows access to the semantic index. This includes enabling and properly configuring the necessary indexing and search capabilities in your tenant. 

Steps:
- Register an Application
    - Go to the Azure AD portal.
    - Register a new application to obtain the necessary permissions for accessing SharePoint data.
- Authenticate and Get Access Token
    - Use OAuth 2.0 to authenticate your application.
    - Obtain an access token that grants permission to query the semantic index.
- Query the Semantic Index
    - Use the Microsoft Graph API to send queries to the semantic index.
    - Retrieve the desired data from SharePoint.
5. From `Microsoft Fabric`
    1. `Using Power BI`: You can create a semantic model from a SharePoint list and use Power BI to analyze the data.
        - Export SharePoint List to Power BI:
            - Open your SharePoint list.
            - In the actions bar, select **Export > Export to Power BI**.
            - Power BI will open, and a dialog will ask you to name the semantic model and choose a workspace to save it in.
        - Create Reports and Dashboards: Use Power BI to create reports and dashboards based on the semantic model.
    2. Using `SemPy Library`
         - Install SemPy:
            - Open your Fabric notebook.
            - Install the SemPy library using the following command:
    
            ```python
            !pip install sempy
            ```
        - Connect to Power BI Dataset: Import the SemPy library and connect to your Power BI dataset
    
            ```python
            from sempy import SemPy
            sempy = SemPy('your_workspace_id', 'your_dataset_id')
            ```
        - Retrieve Data: Use SemPy to query and retrieve data from your semantic model
    
            ```python
            query = "EVALUATE SUMMARIZECOLUMNS('Table'[Column])"
            data = sempy.execute_query(query)
            print(data)
            ```
    3. `Data Pipelines`
        - Create a Data Pipeline
            - In Microsoft Fabric, go to the Data Pipelines section.
            - Create a new pipeline and name it appropriately.
        - Add a Data Source
            - Add SharePoint as a data source.
            - Configure the connection by providing the URL of your SharePoint site and the necessary credentials.
        - Define Data Flow
            - Define the data flow from SharePoint to your desired destination in Fabric.
            - You can use transformations to clean and prepare the data as needed.
        - Schedule and Run the Pipeline
            - Schedule the pipeline to run at your preferred intervals.
            - Run the pipeline to ensure data is being transferred correctly.
    4. `Power Automate`
        - Create a Flow:
            - Go to Power Automate and create a new flow.
            - Choose a trigger, such as `When an item is created` in a SharePoint list.
        - Add Actions:
            - Add actions to extract data from SharePoint. For example, use the `Get items` action to retrieve list items.
            - Add actions to store the data in a location accessible from Fabric, such as a OneDrive folder.
        - Configure and Test:
            - Configure the flow with the necessary details and test it to ensure it works as expected.
            - Save and activate the flow.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-366-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->