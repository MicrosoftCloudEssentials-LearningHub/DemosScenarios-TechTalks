#  RAG (Retrieval-Augmented Generation) pattern - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-12-16

----------

<details>
<summary><b> List of References </b> (Click to expand)</summary>
   
- [What's Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search)
- [Indexer overview - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-indexer-overview)
- [Field mappings and transformations using Azure AI Search indexers](https://learn.microsoft.com/en-us/azure/search/search-indexer-field-mappings)
- [Azure AI Search Sample Data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main)
- [Add scoring profiles to boost search scores](https://learn.microsoft.com/en-us/azure/search/index-add-scoring-profiles)
- [Relevance in keyword search (BM25 scoring)](https://learn.microsoft.com/en-us/azure/search/index-similarity-and-scoring)
- [Tips for better performance in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-performance-tips)
- [Retrieval Augmented Generation (RAG) in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview)
- [Service limits in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)
- [Semantic ranking in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview)
- [Create a skillset in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset)
- [Skillset concepts in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-working-with-skillsets)
- [Custom AML skill in skillsets - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-aml-skill)
- [OCR skill - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-ocr)
- [Custom Web API skill in skillsets - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-custom-skill-web-api)
- [Language detection cognitive skill - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-language-detection)
- [Entity Recognition cognitive skill (v3) - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-entity-recognition-v3)
- [Key Phrase Extraction cognitive skill - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-keyphrases)
- [Image Analysis cognitive skill - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-image-analysis)
- [Text split skill - Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-textsplit)
- [AI Search by sku limits/quota](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)
  
</details>


<details>
<summary><b> Table of Content </b> (Click to expand)</summary>
   
- [Overview](#overview)
- [Search Service](#search-service)
- [Indexer](#indexer)
- [Semantic Ranker](#semantic-ranker)
- [Scoring profiles fine tune](#scoring-profiles-fine-tune)
- [Skillsets](#skillsets)
   - [Skillsets templates](#skillsets-templates)
   - [Workflow Example](#workflow-example)
   - [OCR in Azure AI Search](#ocr-in-azure-ai-search)
- [Schedulers](#schedulers)
- [Cost examples](#cost-examples)
- [Zero Trust](#zero-trust)

</details>

## Overview 

| **Step**       | **Description**                                                                                                                                                                                                 |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Retrieval**  | The system retrieves relevant documents or pieces of information from a knowledge base or external data source based on the input query. This step ensures that the model has access to up-to-date and specific information that can enhance the response. |
| **Augmentation** | The retrieved information is then used to augment the input query. This augmented input provides additional context and details that the generative model can use to produce a more informed response.                                                   |
| **Generation** | A generative model (such as GPT-4) processes the augmented input to generate a coherent and contextually relevant response. The output is a combination of the model's language generation capabilities and the retrieved factual information.               |

> Applications of RAG Pattern:
- **Question Answering**: Providing accurate answers by retrieving relevant documents and generating responses based on them.
- **Document Summarization**: Summarizing documents by retrieving key sections and generating concise summaries.
- **Conversational AI**: Enhancing chatbot responses with up-to-date information from external sources.

> Implementing RAG Pattern with Azure AI:

```mermaid
graph LR
    A[Set Up a Knowledge Base] --> B[Configure a Retrieval System] --> C[Integrate with a Generative Model]
```

1. **Set Up a Knowledge Base**: Store your documents in Azure Storage Blob Containers or another accessible data source.
2. **Configure a Retrieval System**: Use Azure AI Search to index and retrieve relevant documents based on user queries.
3. **Integrate with a Generative Model**: Use a generative model like GPT-4 to process the retrieved documents and generate responses.

> Traditional methods and the `Retrieval-Augmented Generation (RAG)` pattern:

| **Aspect**                | **Traditional Methods**                                                                 | **RAG Pattern**                                                                                   |
|---------------------------|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Model Type**            | Static, pre-trained models that rely on historical data. These models do not update dynamically and can become outdated. | Dynamic integration of retrieval and generative models, allowing for real-time data updates, keeping responses current and relevant. |
| **Data Freshness**        | Relies on pre-trained data, which may not reflect the latest information.                | Retrieves the most recent data from external sources, ensuring up-to-date information.            |
| **Context Understanding** | Often lacks the ability to fully understand the context of a query, leading to less accurate results. | Enhances context understanding by incorporating real-time information retrieval, providing richer context for responses. |
| **Retrieval Techniques**  | Uses keyword matching techniques like BM25 and TF-IDF, which may not capture the semantic meaning of queries. | Employs advanced semantic search techniques that better understand the intent behind queries, leading to more relevant results. |
| **Accuracy**              | May struggle with understanding context and semantic meaning, resulting in less accurate responses. | Improves accuracy by grounding responses in verified external knowledge, reducing the likelihood of errors. |
| **Risk of Hallucinations**| Higher risk of generating incorrect information as responses are based solely on training data. | Reduces this risk by grounding responses in real-time, verified information from external sources. |
| **Flexibility**           | Limited to specific data types and formats, which can restrict their applicability.      | Capable of handling various data types, including text, images, and videos, making it more versatile. |
| **Adaptability**          | Requires extensive retraining to incorporate new information, which can be time-consuming and costly. | More adaptable as it integrates real-time data without the need for frequent retraining.           |
| **Cost Efficiency**       | Can be resource-intensive due to the need for frequent retraining and large labeled datasets. | More cost-effective as it minimizes the need for extensive retraining and leverages existing data sources. |
| **Applications**          | Suitable for basic search and static content generation.                                | Ideal for complex applications such as healthcare, customer support, and content creation, where up-to-date and contextually relevant information is crucial. |

## Search Service 

> Azure AI Search (formerly known as Azure Cognitive Search) is a powerful, enterprise-ready search and retrieval system designed for high-performance applications. It integrates advanced search technologies to support both traditional and generative AI scenarios

![image](https://github.com/brown9804/SDLC-Cloud_Lpath/assets/24630902/bdaebc61-162f-4c0f-855f-6dc74de38397)

| **Category**        | **Details**                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Key Features**    | - `Full-Text Search`: Rich query syntax, fuzzy search, autocomplete, geo-search <br/> - `Vector Search`: Similarity searches using vector embeddings <br/> - `Hybrid Search`: Combines full-text and vector search |
| **Core Components** | - `Indexing`: Data ingestion, text tokenization, vectorization, AI skills <br/> - `Querying`: Executes traditional and vector queries, semantic ranking |

> Steps:
- Create a AI Search Resource, click on `Create a resource`
- Search for `ai search`, you can check `Azure Services only` for a faster search.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/7e9e34b9-73d5-4c94-944a-7cd020b471e7">

- Configure Search Service: Provide the necessary details
    - Name: Enter a name for your search service.
    - Resource Group: Use the same resource group as your Azure OpenAI resource.
    - Location: Use the same region for reduced latency.
    - Pricing Tier: Select a pricing tier based on your needs.
      
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/9420a863-f22c-4236-9687-9e3799af15c8">

## Indexer 

> Indexers in Azure AI Search are tools that automatically gather and organize data from various sources into a searchable index. <br/> Indexers can be scheduled to run at regular intervals or triggered on-demand, making them flexible for various data ingestion needs

   <img width="750" alt="image" src="https://github.com/user-attachments/assets/ec8972c1-25ea-4e6f-a0b4-a7c96a23ed41">


| **Key Function**       | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| **Data Extraction**    | Indexers pull data from supported data sources like Azure Blob Storage, Azure SQL Database, and Azure Cosmos DB. This process is often referred to as a `pull model` because the search service pulls data into the index without requiring custom code. |
| **Field Mapping**      | They map fields from the source data to the search index. This includes both implicit mappings (where field names and types match) and explicit mappings (where you define how fields should be mapped). |
| **Skillset Execution** | Indexers can apply AI skills to enrich the data during indexing. This includes tasks like optical character recognition (OCR), text translation, and key phrase extraction. |

> Stages of Indexing:
1. **Document Cracking**: Extracts text and metadata from documents.
2. **Field Mappings**: Maps source fields to index fields.
3. **Skillset Execution**: Applies AI skills for data enrichment.
4. **Output Field Mappings**: Maps enriched data to the final index fields.

| **Usage Scenario**            | **Description**                                                                 |
|-------------------------------|---------------------------------------------------------------------------------|
| **Single Data Source**        | Indexing content from one data source.                                          |
| **Multiple Data Sources**     | Combining content from various sources into a single index.                     |
| **Content Transformation**    | Using AI skills to transform and enrich data during indexing.                   |

> Steps:

- Add `Overview`, click on `Import Data`:
  
  <img width="1565" height="622" alt="image" src="https://github.com/user-attachments/assets/3d40a3b4-d8ff-4536-9051-9c619e8985cd" />

- In this example, let's choose `Azure Blob Storage`, and fill the required information:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/6dfc185b-b65d-4e14-bb66-3115ddae6526">

- Make sure you choose the right target index type, avoid using collections that way you will improve your search.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/f8cf2048-1a9f-4e89-940d-c4683061eab4">

## Semantic Ranker 

> Semantic rankers in Azure AI Search are advanced features that improve search relevance by using Microsoft's language understanding models to re-rank search results based on their semantic meaning. `This technology is particularly useful for content-rich and descriptive data, such as knowledge bases and online documentation`.

| **Step**               | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| Initial Ranking        | When a query is made, the search service first uses traditional ranking algorithms like `BM25` or `Reciprocal Rank Fusion (RRF)` to generate an initial set of results. |
| Semantic Ranking       | The initial results are then passed to the Semantic Ranker, which uses deep learning models adapted from Microsoft Bing. These models understand the context and semantic meaning of the query to re-rank the results based on their relevance. |
| Summarization and Scoring | - **Input Collection**: The system collects and summarizes inputs from the top 50 results. It focuses on text fields like titles, keywords, and content, trimming excessively long strings to fit model constraints. <br/> - **Scoring**: The summarized inputs are scored for semantic relevance. Each document receives a score from 0 to 4, with higher scores indicating greater relevance. |
| Output Generation      | The Semantic Ranker generates outputs that include: <br/> - **Semantic Captions**: Verbatim sentences and phrases that best summarize the content, with highlights over key passages. <br/> - **Semantic Answers**: Direct answers to queries posed as questions, extracted from the document text. |
| Efficiency and Performance | To ensure quick processing, the system consolidates and reduces inputs, allowing the reranking step to be completed within the expected query latency. |

In summary, Semantic rankers analyze the context and meaning of both the query and the documents, using deep learning models adapted from Microsoft Bing. This process involves:
- **Summarizing Inputs**: Collecting and summarizing the most relevant parts of documents.
- **Scoring Results**: Assigning relevance scores based on semantic understanding.
- **Outputting Enhanced Results**: Providing re-ranked results along with captions and answers.

| **Key Function**                  | **Description**                                                                 |
|-----------------------------------|---------------------------------------------------------------------------------|
| **Secondary Ranking**             | After an initial ranking using traditional methods like BM25, semantic rankers apply a secondary ranking to promote the most semantically relevant results. |
| **Semantic Captions and Highlights** | They extract and highlight key phrases and sentences from documents, making it easier for users to understand why a result is relevant. |
| **Semantic Answers**              | For queries that resemble questions, semantic rankers can provide direct answers extracted from the content. |

> Steps:

- Go to your `index`. It's under Search Management.
- Choose your index or create a new one.
- Under `semantic configurations`, create a new one or edit an existing one.

   <img width="953" alt="image" src="https://github.com/user-attachments/assets/e87f7fbf-1282-4a31-b68b-937f9ae90e98">

Normal Search: `historic hotel with good food`  <br/> 
Search with Semantic Ranker: <br/> 
```json
{
  "search": "historic hotel with good food",
  "answers": "extractive|count-3",
  "captions": "extractive|highlight-true",
  "queryLanguage": "en-us",
  "highlightPreTag": "<strong>",
  "highlightPostTag": "</strong>",
  "select": "HotelId, HotelName, Description, Category",
  "semanticConfiguration": "semantic-confi",
  "count": true,
  "queryType": "semantic"
}
```

| Normal Search | With Semantic Ranker | 
| --- | --- | 
| <img width="550" alt="image" src="https://github.com/user-attachments/assets/0e7ef3e5-ae9a-4891-a2e4-fa4c79127b82"> | <img width="700" alt="image" src="https://github.com/user-attachments/assets/bcf40166-01d9-493d-b109-e5c3bad4d639">|

## Scoring profiles (fine tune)

> Scoring profiles in Azure AI Search are `configurations that determine how search results are ranked based on relevance`. They allow you to customize the ranking algorithm to better suit your specific search requirements. BM25, or `Best Matching 25`, is a `ranking function used by search engines to estimate the relevance of documents to a given search query`. It’s an evolution of the TF-IDF (Term Frequency-Inverse Document Frequency) model and is part of the family of probabilistic information retrieval models.

> [!NOTE]
> By using scoring profiles, you can fine-tune the search experience to ensure that the most relevant and useful results are presented to users.

| **Key Component**       | **Description**                                                                 |
|-------------------------|---------------------------------------------------------------------------------|
| **Text Scoring**        | Adjusts the importance of specific fields in the search index. For example, you can give more weight to matches in the "title" field than in the "description" field. |
| **Magnitude Scoring**   | Boosts results based on numeric values in the index. For instance, you can prioritize products with higher ratings. |
| **Freshness Scoring**   | Prioritizes newer content by boosting documents based on date fields.           |
| **Distance Scoring**    | Enhances results based on geographical proximity, useful for location-based searches. |

> How Scoring Profiles Work: 
- **Field Weights**: Assign different weights to fields to influence the ranking of search results.
- **Boost Functions**: Apply functions to boost scores based on field values, such as boosting newer documents or those with higher ratings.
- **Custom Scoring**: Combine multiple scoring functions to create a tailored ranking strategy that meets your specific needs.

| **Step**               | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| Definition and Setup   | - **Scoring Profile Definition**: A scoring profile is defined within the index schema. It includes weighted fields and functions that determine how scores are adjusted. <br/> - **Weighted Fields**: These are specific fields in your documents that you want to give more importance to. For example, you might want matches in the `title` field to be more relevant than those in the `content` field. <br/> - **Functions**: These are used to boost scores based on numeric data, such as dates, ranges, or geographic coordinates. Functions include `distance`, `freshness`, `magnitude`, and `tag`. |
| Application            | - **Query Execution**: When a search query is executed, the scoring profile is applied to adjust the relevance scores of the search results. <br/> - **Boosting Criteria**: The profile boosts the scores of documents that meet the specified criteria. For example, a document closer to a specified location might receive a higher score if a `distance` function is used. |
| Scoring Process        | - **Initial Scoring**: The search service first uses traditional ranking algorithms like BM25 to generate an initial set of results. <br/> - **Profile Application**: The scoring profile is then applied to these results. Weighted fields and functions adjust the scores based on the defined criteria. <br/> - **Final Ranking**: The adjusted scores are used to produce the final ranked list of search results. |
| Efficiency and Performance | - **Optimization**: The system optimizes the application of scoring profiles to ensure quick processing and minimal impact on query latency. <br/> - **Iterative Testing**: Profiles are often tested iteratively to fine-tune the boosting criteria and ensure they improve search relevance effectively. |

> Steps to create a scoring profile:
- Click on `Add scoring profile`, add your `profile name` and the `fields and weights`. Those numbers are based on your criteria.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/91b326f6-c4fa-473b-8db3-a8cfc62e22d4">

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/02089d51-d894-4e87-86ca-1f7411a479ca">

- You can add a different scoring function:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/0d95afe7-654f-4417-a980-3d90999ea97c">

- Just make sure to add all the required information:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/53b3d20e-8bc9-4e19-9007-8b0f3743ae33">
  
- At the end you will have something like this:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/551970b5-95c1-4f45-84d3-e96d8fb8d198">

## Skillsets 

> Skillsets in Azure AI Search are collections of AI-powered skills that enhance and transform data during the indexing process. They are designed to enrich documents by extracting meaningful information, which can then be used to improve search relevance and user experience.

   <img width="700" alt="image" src="https://github.com/user-attachments/assets/635c68da-2a97-42fe-9e26-5dd39c62192a">

| Key Concepts | Details |
| --- | --- |
| **Skillset Definition** | A skillset is a reusable object attached to an indexer. It contains one or more skills that perform specific tasks on the data retrieved from an external source. |
| **Enrichment Tree** |  An enriched document is a temporary, tree-like data structure created during skillset execution. It collects all the changes introduced through skills, representing them as a hierarchy of nodes. |
| **Indexer Definition** | An indexer pulls data from a data source, processes it through the skillset, and then indexes the enriched data. The indexer configuration includes mappings that set the data path to fields in a search index. |

> How Skillsets Work

1. **Data Extraction**:The indexer extracts raw data from the data source, such as text and images.
2. **Skill Execution**: Skills in the skillset process the extracted data. Each skill reads from and writes to the enriched document, adding structure and substance to the data. Skills can execute independently or in sequence, depending on their configuration.
3. **Enrichment**: Skills perform various enrichment tasks, such as OCR for extracting text from images, entity recognition for identifying entities in text, and text translation.
4. **Output Mapping**: The enriched data is mapped to the fields in the search index. This mapping determines what content is ingested into the index and how it is structured.

### Skillsets templates

> Predefined configurations that streamline the process of adding various AI capabilities to your search solutions. These templates allow you to integrate a range of AI skills, such as text analysis, image recognition, and custom machine learning models, into your search index. By using skillset templates, you can easily enhance your search functionality with features like language detection, key phrase extraction, entity recognition, and more. This helps in transforming raw content into enriched, searchable information, making it easier to derive insights and improve the overall search experience.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/e2e2c083-c914-4055-a326-67a88525e880">

| Skill Name                             | Description                                                                                   |
|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Azure Machine Learning (AML)           | Integrates custom Azure Machine Learning models into AI enrichment workflows. Allows for building, training, and deploying machine learning models, and using them to enhance data processing. Useful for tasks like predictive analytics and anomaly detection.          |
| Custom Web API Skill                   | Allows integration of custom web APIs into the AI search workflow. This skill can call out to a Web API endpoint to perform custom operations and return enriched data. Ideal for extending functionality with bespoke processing logic.                            |
| Custom Web API Skill - Azure Functions | Enables the use of Azure Functions as custom web APIs in the AI search process. This allows for serverless computing and scalable custom operations, making it easier to manage and deploy custom logic.               |
| Image Analysis Skill                   | Analyzes images to extract information such as objects, faces, and text. It can generate captions, tags, and identify celebrities and landmarks. Useful for enhancing image metadata and enabling visual search capabilities.                      |
| OCR Skill                              | Optical Character Recognition skill that extracts printed and handwritten text from images. Supports various image formats and languages. Essential for digitizing text from scanned documents and images.                           |
| Entity Recognition Skill (V3)          | Identifies and categorizes entities within text data, such as people, organizations, locations, and more. Uses machine learning models from Azure AI Language. Useful for structuring unstructured text data and enhancing search relevance.                                         |
| Entity Linking Skill (V3)              | Links recognized entities to a knowledge base, providing additional context and information about the entities. Useful for enriching text with structured data and improving search accuracy. |
| Key Phrase Extraction Skill            | Extracts key phrases from text to identify main points or topics. Useful for summarizing and understanding the main concepts in a document, making it easier to index and search large text corpora.                             |
| Language Detection Skill               | Detects the language of a given text input and provides a language code and confidence score. Useful for multilingual content processing and routing text to appropriate language-specific processing pipelines.                                                   |
| Merge Skill                            | Combines multiple inputs into a single output for further processing. Useful for merging text from different sources or combining related data into a cohesive format.                         |
| Split Skill                            | Splits a single input into multiple outputs based on specified criteria or patterns, such as sentences or pages. Useful for breaking down large texts for detailed analysis or processing in manageable chunks.          |
| Sentiment Skill                        | Analyzes text to determine sentiment (positive, negative, neutral). Useful for understanding the emotional tone of a document, which can be applied in customer feedback analysis and social media monitoring.                           |
| Translation                            | Translates text from one language to another using translation services. Supports multiple languages and provides accurate translations. Useful for making content accessible to a global audience.                      |
| Custom Entity Lookup (V3)              | Searches for specific entities within a dataset based on custom criteria or definitions. Useful for identifying domain-specific entities and enhancing search precision.      |
| PII Detection Skill                    | Identifies and redacts Personally Identifiable Information (PII) in text data. Helps ensure data privacy and compliance with regulations like GDPR.                |
| Azure OpenAI Embedding Skill           | Integrates OpenAI's embedding capabilities for advanced natural language understanding tasks. Useful for semantic search, text similarity, and enhancing search relevance with contextual understanding. |
| Shaper Skill                           | Transforms and shapes data into a desired format, making it easier to work with in downstream processes. Useful for data normalization and preparation. |
| Conditional Skill                      | Applies conditional logic to data processing, allowing for dynamic and context-aware transformations. Useful for creating complex processing workflows that adapt based on data characteristics. |
| Document Extraction Skill              | Extracts structured data from documents, such as forms and invoices, using predefined templates. Useful for automating data entry and processing structured information from scanned documents. |

### Workflow Example

1. **Define Skillset**:
   - Create a skillset with the necessary skills, such as OCR and entity recognition. Under `Skillsets`, click on `+ Add skillset`:
     
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/e64f6ee6-f342-4493-8fe9-03daabab2ce8">

   - Example JSON configuration:

       ```json
        {
          "name": "ocr-skillset",
          "skills": [
            {
              "@odata.type": "#Microsoft.Skills.Vision.OcrSkill",
              "description": "Extract text from images",
              "context": "/document",
              "inputs": [
                {
                  "name": "image",
                  "source": "/document/normalized_images/*"
                }
              ],
              "outputs": [
                {
                  "name": "text",
                  "targetName": "ocrText"
                }
              ]
            }
          ],
          "cognitiveServices": {
            "@odata.type": "#Microsoft.Azure.Search.CognitiveServicesByKey",
            "description": "mycogsvcs",
            "key": ""
          }
        }
        ```
  - If needed, you can click `+ Add new skill` to add a new template to the skillset:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/7131d5af-533e-4a68-b5eb-d5d0c7e995fa">

2. **Create Indexer**:
   - Configure an indexer to use the skillset and specify the data source and target index.
   - Example JSON configuration:
     ```json
     {
       "name": "my-indexer",
       "dataSourceName": "my-data-source",
       "targetIndexName": "my-index",
       "skillsetName": "ocr-skillset",
       "schedule": {
         "interval": "PT2H"
       },
       "parameters": {
         "batchSize": 50,
         "maxFailedItems": 0,
         "maxFailedItemsPerBatch": 0
       }
     }
     ```

3. **Run Indexer**: Execute the indexer to start processing documents and applying the skills.
4. **Verify Enrichment**: Check the enriched data in the search index to ensure the skills have been applied correctly.

### OCR in Azure AI Search

> `Optical Character Recognition (OCR)` is a skill in Azure AI Search that extracts text from images. 

Here's how it works:
1. **Skill Parameters**:
   - **detectOrientation**: Detects the orientation of the image.
   - **defaultLanguageCode**: Specifies the language of the input text.
2. **Skill Inputs**: `image` The image field from which text is to be extracted.
3. **Skill Outputs**:
   - **text**: The plain text extracted from the image.
   - **layoutText**: Structured text with information about the location of the text in the image.
4. **Execution**:
   - The OCR skill uses machine learning models from Azure AI Vision to recognize printed and handwritten text in various image formats (JPEG, PNG, BMP, TIFF).
   - The extracted text is added to the enrichment tree and can be used for further processing or directly indexed.

## Schedulers 

> Used to automate the execution of indexers at specified intervals. This is particularly useful when your source data changes over time or when dealing with large datasets that need to be indexed regularly.

| **Aspect**          | **Description**                                                                                                                                                                                                 |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Scheduling Intervals** | You can set the interval for how often the indexer should run. The smallest interval allowed is 5 minutes, and the longest is 24 hours. This is defined using an ISO 8601 duration format, such as `PT15M` for every 15 minutes or `PT2H` for every two hours. |
| **Start Time**      | You can specify a start time for the scheduler in UTC. If omitted, the current time is used. This allows you to control when the first execution occurs.                                                                 |
| **Use Cases**       | Schedulers are beneficial in scenarios where: <ul><li>Source data is frequently updated, and you want the indexer to process these changes automatically.</li><li>The dataset is very large, requiring a recurring schedule to index all content gradually.</li><li>Multiple sources are used to populate an index, and you need to stagger the indexing jobs to avoid conflicts.</li></ul> |
| **Configuration**   | You can configure schedules through the Azure portal, REST APIs, or Azure SDKs. In the portal, you can set the schedule by navigating to the indexer's settings and choosing the desired interval and start time. |
| **Behavior**        | Once an indexer is scheduled, it will continue to run at the specified intervals until the schedule is cleared or the indexer is disabled. If an indexer is still running when the next scheduled execution time arrives, the pending execution is postponed until the current job finishes. |

## Cost examples 

> General idea of the costs associated with different tiers and features in Azure AI Search. For a more precise estimate, you can use the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/details/search/) to input your expected usage and get a detailed cost breakdown.

| **Tier**                  | **Cost**                  | **Features**                                                                                          | **Use Case**                                                                                         |
|---------------------------|---------------------------|-------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Free Tier**             | \$0/month                 | Limited to 3 indexes, 50 MB storage, basic search capabilities                                        | Ideal for small projects or testing purposes                                                         |
| **Basic Tier**            | \$73.73/month per SU      | Up to 15 indexes, 15 GB storage, moderate search capabilities                                         | Suitable for small to medium-sized applications with moderate search requirements                    |
| **Standard S1 Tier**      | \$245.28/month per SU     | Up to 50 indexes, 160 GB storage, enhanced search capabilities                                        | Ideal for medium to large applications needing robust search functionality                           |
| **Standard S2 Tier**      | \$981.12/month per SU     | Up to 200 indexes, 512 GB storage, high-performance search capabilities                               | Suitable for large applications with high search demands and large datasets                          |
| **Standard S3 Tier**      | \$1,962.24/month per SU   | Up to 200 indexes (or 1,000 in high-density mode), 1 TB storage, premium search capabilities          | Best for enterprise-level applications with extensive search needs and very large datasets           |
| **Storage Optimized L1**  | \$2,802.47/month per SU   | Up to 10 indexes, 2 TB storage, optimized for large-scale storage and search                          | Ideal for applications requiring extensive storage and optimized search performance                  |
| **Storage Optimized L2**  | \$5,604.21/month per SU   | Up to 10 indexes, 4 TB storage, maximum storage optimization                                          | Suitable for applications with massive storage needs and high search performance requirements        |
| **Additional Costs**      |                    | <ul><li>**Custom Entity Lookup**: \$1 per 1,000 text records for the first million records, with decreasing rates for higher volumes</li><li>**Image Extraction**: \$1 per 1,000 images for the first million images, with decreasing rates for higher volumes</li><li>**Semantic Ranker**: First 1,000 requests per month are free, then \$1 per 1,000 additional requests</li></ul> | Applicable for specific advanced features and additional processing needs                            |

## Zero Trust 

> Zero Trust AI architecture in Microsoft Azure is a `security framework designed to protect data, applications, and infrastructure by assuming that threats can come from both inside and outside the network`. This model operates on the principle of "never trust, always verify", meaning `every access request is thoroughly authenticated and authorized based on all available data points, regardless of its origin. The architecture integrates multiple layers of security, including strong identity verification, device compliance checks, and least privilege access, ensuring that only authorized users and devices can access sensitive resources`. By continuously monitoring and validating each request, Zero Trust AI architecture helps organizations minimize risks and enhance their overall security posture

Click [here](https://github.com/brown9804/MicrosoftCloudEssentialsHub/tree/main/0_Azure/3_AzureAI/0_AISearch/demos/1_ZeroTrustRAG) for a quick guidance.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
