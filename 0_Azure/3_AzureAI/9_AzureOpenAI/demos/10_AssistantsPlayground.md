# Assistants Playground - Overview 

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------

> Azure OpenAI Assistants (Preview) allows you to create AI assistants that meet your needs using custom instructions and advanced tools such as code interpreters and custom functions.

> [!NOTE]
> Currently, there is no specific timeline for the full release of Azure OpenAI Assistants. It is typical for Azure services to stay in the preview phase for several months. During this period, we collect feedback and make necessary improvements.

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>
  
- [Quickstart: Get started using Azure OpenAI Assistants (Preview)](https://learn.microsoft.com/en-us/azure/ai-services/openai/assistants-quickstart?tabs=command-line%2Cjavascript-keyless%2Ctypescript-keyless&pivots=programming-language-ai-studio)
- [Getting started with Azure OpenAI Assistants (Preview)](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/assistant)
- [Azure OpenAI Assistants API (Preview)](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/assistants)
- [Azure OpenAI Service quotas and limits](https://learn.microsoft.com/en-us/azure/ai-services/openai/quotas-limits)
- [I am using Azure Assistant API its in beta version, is it safe to use it in production?](https://learn.microsoft.com/en-us/answers/questions/2072066/i-am-using-azure-assistant-api-its-in-beta-version)
 
</details>


## Overview

| **Feature**                                | **Description**                                                                                                                                                                                                 |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Custom Instructions**                    | You can provide detailed instructions to shape the behavior and responses of your AI assistant. This allows for a high degree of customization to meet your specific requirements.                                |
| **Advanced Tools - Code Interpreter**      | This tool provides a sandboxed Python environment where the assistant can write, test, and execute code. It's particularly useful for tasks that require data analysis, visualization, or other computational tasks. |
| **Advanced Tools - Custom Functions**      | You can define your own functions to extend the capabilities of the assistant. These functions can be used to perform specific tasks or integrate with other systems.                                             |
| **File Search and Vector Store - File Search** | The assistant can search through up to 10,000 files, making it efficient for handling large datasets. It supports parallel queries and features enhanced reranking and query rewriting.                           |
| **File Search and Vector Store - Vector Store** | This feature allows files to be parsed, chunked, and embedded for efficient searching. Vector stores can be shared across assistants and threads, simplifying file management.                                     |
| **Assistants Playground**                  | This no-code environment lets you prototype and test your AI assistants quickly. It's a great way to experiment with different configurations and see how your assistant performs.                                |


<img width="550" alt="image" src="https://github.com/user-attachments/assets/293160fb-bc83-48ee-94d3-b4f3f9feb4d9">


### Setting Up Your First Assistant

> You can use the `Azure OpenAI Studio or programmatically set up your assistant using programming languages like Python, C#, JavaScript, etc`.

Example:

>  `Imagine you need an assistant to help with data visualization`. You can create an assistant with instructions to generate visualizations using the code interpreter. `The assistant can write and execute Python code to create charts and graphs based on user input`

1. **Create an Assistant**: Define the assistant's name, instructions, and tools it will use (e.g., code interpreter).
2. **Create a Thread**: This represents a conversation session between the assistant and a user.
3. **Add Messages**: Add user messages to the thread to simulate interactions.
4. **Run the Assistant**: Activate the assistant to process the thread and generate responses based on the provided instructions and tools.

### Limitations and Considerations

- **Preview Status**: As the service is in preview, it `may not be fully stable and is subject to changes while we gather feedback and make improvements`. They may not have undergone the necessary testing and validation for production use. `It's recommended to use it for testing and development rather than production.`
`If you choose to use the Azure OpenAI Assistant API in a production environment, it is advisable to closely monitor the API's performance and have a plan in place to address any issues`. It is also important to `stay updated with any changes or updates to the API and adjust your implementation accordingly`. You can refer to the Azure OpenAI Service release notes for updates on the [What's new in Azure OpenAI Service](https://learn.microsoft.com/en-us/azure/ai-services/openai/whats-new) page.

    Alternatives:
    > - To provide the model with specific instructions on its behavior and context, you can use the `Give the model instructions and context` feature within the `Chat playground`. This allows you to describe the assistant’s personality, specify what it should and shouldn’t answer, give the model context, add other sections (e.g., examples, variables), and dictate response formatting. `There is no token limit for this section, but it will be included with every API call, counting against the overall token limit`.
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/9e0f2ede-7ca3-49b9-8f75-379d1e4f4486">
    
    > - Using the Azure OpenAI Assistants API to build custom solutions using Azure’s GPT-4 model integrated with other Azure services (e.g., Azure Logic Apps, Azure Functions) for enhanced functionality. This approach enables you to build assistants with custom workflows, tool integration, code execution capabilities, custom instructions, code interpreters, and custom functions.  
- **Storage Limits**: The current limit for uploaded files is 100GB, but you can request an increase through Azure support if needed through Azure support channels.


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
