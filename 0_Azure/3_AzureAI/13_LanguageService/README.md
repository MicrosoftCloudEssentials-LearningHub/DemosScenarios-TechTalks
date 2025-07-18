# Language Service - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Azure Language Service is part of Azure AI, is cloud-based service that provides a suite of Natural Language Processing (NLP) features for understanding and analyzing text. It helps build intelligent applications using the web-based Language Studio, REST APIs, and client libraries, offering a comprehensive suite of AI services and tools for developers to build intelligent natural language solutions. <br/> 
> It leverages state-of-the-art language models, including Z-Code++ and fine-tuned GPT models.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What’s new in Azure AI Language | BUILD 2024](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/what-s-new-in-azure-ai-language-build-2024/ba-p/4147399)
- [What's new in Azure AI Language?](https://learn.microsoft.com/en-us/azure/ai-services/language-service/whats-new?tabs=csharp)
- [azurerm_cognitive_account - terraform doc](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/cognitive_account)

</details>

## Overview

> Azure Language Service unifies several previously available Azure AI services, including: <br/> 
> Text Analytics <br/> 
> QnA Maker <br/>
> Language Understanding (LUIS)

<img width="550" alt="image" src="https://github.com/user-attachments/assets/73f65004-72ea-4cf8-bf7d-f56240cbbd67">

| **Feature** | **Description** |
|-------------|-----------------|
| **Unified Experience** | Supports a unified experience in Azure AI Studio, integrating with other Azure AI services like Speech and Vision. |
| **Azure AI Studio** | Provides playgrounds for trying out features like Summarization and PII detection. |
| **Prompt Flow** | A development tool in Azure AI Studio to streamline the development cycle of AI applications. |
| **Prebuilt Capabilities** | Includes summarization, PII detection, and text analytics for various domains, such as healthcare. |
| **Custom Features** | Enhanced capabilities in Conversational Language Understanding (CLU) for intent identification and entity extraction. |
| **Summarization** | Uses extractive text summarization to produce summaries of documents and conversation transcriptions. |
| **Conversation Summarization** | Supports 12 additional languages and improved chapter title features. |
| **Personally Identifiable Information (PII) Detection** | Identifies and redacts sensitive information such as phone numbers, email addresses, and forms of identification. |
| **Conversational PII Redaction** | Now generally available for English-language contexts. |
| **Named Entity Recognition (NER)** | Categorizes entities (words or phrases) in unstructured text across predefined categories like people, events, places, and dates. |
| **Custom Named Entity Recognition** | Allows users to train custom models to recognize domain-specific entities. |
| **Key Phrase Extraction** | Evaluates and returns the main concepts in unstructured text as a list. |
| **Entity Linking** | Disambiguates the identity of entities found in unstructured text and returns links to Wikipedia. |
| **Language Detection** | Detects the language of a document and returns a language code for a wide range of languages. |
| **Expanded Language Detection** | Supports additional scripts according to the ISO 15924 standard. |
| **Sentiment Analysis and Opinion Mining** | Analyzes text to determine positive or negative sentiment and associates it with specific aspects of the text. |
| **Text Analytics for Health** | Extracts and labels relevant medical information from unstructured text, such as clinical notes and medical literature. |
| **Custom Text Classification** | Enables users to train models to classify text into custom categories based on their specific needs. |
| **Data Augmentation for Diacritics** | Useful for generating variations of training data for languages with diacritic variations. |

## Use Cases

| **Use Case** | **Description** |
|--------------|-----------------|
| **Healthcare** | Text analytics for extracting healthcare-specific entities from unstructured text. |
| **Security** | PII detection and redaction to protect sensitive information. |
| **Customer Service** | Conversational intent identification to improve customer interactions. |
| **Text Analytics** | Extract insights from text data for business intelligence. |
| **Customer Support** | Automate responses and improve customer service with sentiment analysis and entity recognition. |
| **Content Moderation** | Detect and redact sensitive information in user-generated content. |
| **Document Summarization** | Automatically generate summaries for long documents and transcripts. |
| **Legal Document Analysis** | Extract key information and summarize legal documents to assist legal professionals. |
| **Market Research** | Analyze customer feedback and social media to gain insights into market trends and consumer sentiment. |
| **Education** | Automatically grade essays and provide feedback on student writing. |
| **E-commerce** | Enhance product search and recommendation systems by understanding customer queries and reviews. |
| **Human Resources** | Analyze employee feedback and survey responses to improve workplace culture and policies. |
| **Financial Services** | Extract and analyze financial data from reports and documents to support decision-making. |

## Services

| **Service**                          | **Description**                                                                                       |
|--------------------------------------|-------------------------------------------------------------------------------------------------------|
| `Academic`                           | Provides academic knowledge and research data, enabling access to scholarly articles and academic resources. |
| `AnomalyDetector`                    | Detects anomalies in time-series data using machine learning algorithms, helping to identify unusual patterns and trends. |
| `Bing.Autosuggest`                   | Provides autocomplete suggestions for search queries, enhancing user experience by predicting search terms. |
| `Bing.Autosuggest.v7`                | Updated version of Bing Autosuggest with improved algorithms and features for better search term predictions. |
| `Bing.CustomSearch`                  | Customizable search engine that allows developers to tailor search results to specific needs and preferences. |
| `Bing.Search`                        | General web search capabilities, providing comprehensive search results from the web. |
| `Bing.Search.v7`                     | Updated version of Bing Search with enhanced search algorithms and features for more accurate search results. |
| `Bing.Speech`                        | Converts speech to text and vice versa, enabling voice recognition and text-to-speech functionalities. |
| `Bing.SpellCheck`                    | Checks and corrects spelling in text, improving the accuracy of written content. |
| `Bing.SpellCheck.v7`                 | Updated version of Bing SpellCheck with enhanced spelling correction algorithms. |
| `CognitiveServices`                  | A suite of AI services for vision, speech, language, and decision-making, providing pre-built and customizable models. |
| `ComputerVision`                     | Analyzes visual content to extract information, such as object detection, image classification, and OCR. |
| `ContentModerator`                   | Moderates text, image, and video content to detect and filter inappropriate or harmful content. |
| `ContentSafety`                      | Ensures content safety by detecting harmful content in text, images, and videos, helping to maintain a safe environment. |
| `CustomSpeech`                       | Customizable speech recognition models that can be tailored to specific vocabularies and environments. |
| `CustomVision.Prediction`            | Customizable image classification models for prediction, allowing developers to create and deploy custom vision models. |
| `CustomVision.Training`              | Customizable image classification models for training, enabling the creation of custom vision models with specific datasets. |
| `Emotion`                            | Detects emotions in images, providing insights into the emotional state of individuals based on facial expressions. |
| `Face`                               | Detects and recognizes faces in images, offering features like face verification, identification, and analysis. |
| `FormRecognizer`                     | Extracts information from forms and documents using AI, automating data entry and document processing tasks. |
| `ImmersiveReader`                    | Helps users read and comprehend text by providing tools for text-to-speech, translation, and text highlighting. |
| `LUIS`                               | Language Understanding Intelligent Service for natural language processing, enabling the creation of conversational AI applications. |
| `LUIS.Authoring`                     | Tools for authoring LUIS models, allowing developers to create and manage language understanding models. |
| `MetricsAdvisor`                     | Monitors metrics and diagnoses issues using AI, helping to identify and resolve performance problems. |
| `OpenAI`                             | Provides access to OpenAI's language models for various tasks, such as content generation, summarization, and natural language understanding. |
| `Personalizer`                       | Delivers personalized experiences for users by using reinforcement learning to make real-time decisions. |
| `QnAMaker`                           | Creates a question-and-answer layer over your data, enabling the creation of conversational bots and knowledge bases. |
| `Recommendations`                    | Provides product recommendations based on user behavior and preferences, enhancing the user experience. |
| `SpeakerRecognition`                 | Identifies and verifies speakers based on their voice, offering features like speaker identification and verification. |
| `Speech`                             | Converts speech to text and vice versa, enabling voice recognition and text-to-speech functionalities. |
| `SpeechServices`                     | Comprehensive suite of speech services including recognition, synthesis, and translation, providing end-to-end speech solutions. |
| `SpeechTranslation`                  | Translates spoken language in real-time, enabling cross-language communication through speech translation. |
| `TextAnalytics`                      | Analyzes text for sentiment, key phrases, entities, and language, providing insights into textual data. |
| `TextTranslation`                    | Translates text between languages, enabling multilingual communication and content localization. |
| `WebLM`                              | Provides language models for web-based applications, enhancing natural language processing capabilities for web services. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
