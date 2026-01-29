# Optimizing Chatbot Efficiency

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------


<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [General Overview](#general-overview)
- [Set Up Your Azure Environment](#set-up-your-azure-environment)
- [Set Up a Database for Context Storage](#set-up-a-database-for-context-storage)
- [Implement Contextual Memory in the Application](#implement-contextual-memory-in-the-application)
- [Example](#example)
- [Other considerations:](#other-considerations)
- [Wiki](#wiki)
 
</details>

      
> Find below strategies to enhance process efficiency, these approaches can significantly reduce computational demands and enhance model efficiency in chatbot applications.

- [Contextual Memory](#implement-contextual-memory-in-the-application): Implement a server-side system that retains conversation context. This allows for sending only new user requests to the model, with the server adding necessary context before the API call.
- **Prompt Compression**: Apply techniques to shorten the prompt by removing non-essential words, simplifying sentences, and concentrating on key context and instructions.
- **Batch Processing**: For multiple queries, group them into a single API call to decrease request numbers and boost efficiency.
- **Parameterization**: Use a parameterized format for prompts to allow dynamic input substitution, reducing prompt size while keeping it flexible.
- **Preprocessing**: Clean and preprocess input data to eliminate unnecessary whitespace, punctuation, and formatting issues, optimizing prompt processing efficiency.

## General Overview 
### Set Up Your Azure Environment

| **Task**                    | **Steps**|
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Create an Azure OpenAI Resource** | 1. **Sign in to the Azure Portal**: <br> - Go to the Azure Portal. <br> - Sign in with your Azure account. <br> 2. **Create a Resource**: <br> - Click on `Create a resource`. <br> - Search for `Azure OpenAI`. <br> - Select `Azure OpenAI` and click `Create`. <br> 3. **Configure the Resource**: <br> - Fill in the required details such as Subscription, Resource Group, Region, and Name. <br> - Choose the appropriate pricing tier. <br> - Click `Review + create` and then `Create`. |
| **Deploy a Model**          | 1. **Navigate to Azure OpenAI Studio**: <br> - Go to Azure OpenAI Studio. <br> - Sign in with your Azure credentials. <br> 2. **Create a Deployment**: <br> - Select your Azure OpenAI resource. <br> - Click on `Deployments` and then `Create new deployment`. <br> - Choose the model you want to deploy (e.g., GPT-4). <br> - Configure the deployment settings and click `Create`. |

### Set Up a Database for Context Storage

> Using Azure SQL Database: 

1. Create an Azure SQL Database:
    - In the Azure Portal, click on `Create a resource`.
    - Search for `SQL Database` and select it.
    - Fill in the required details such as Subscription, Resource Group, Database Name, and Server.
    - Configure the database settings and click `Review + create` and then `Create`.
2. Configure the Database:
    - Set up the firewall rules to allow your application to connect to the database.
    - Create a table to store conversation context.
    
    ```sql 
    CREATE TABLE context (
        user_id NVARCHAR(50) PRIMARY KEY,
        conversation NVARCHAR(MAX)
    );
    ```

## Implement Contextual Memory in the Application

> To implement contextual memory, you'll need to store and manage the conversation context on the server. This way, you only have to send the user's most recent request with each request. Here's a step-by-step guide to getting started:

- Set Up a Server: To store the conversation context. This can be done using a web server with a database.
- Store Conversation Context: When a user sends a message, store the conversation context in a database. This context can include the user’s previous messages, the bot’s responses, and any other relevant information.
- Retrieve Context: When a new message is received, retrieve the stored context from the database. Combine this context with the new user message to form the prompt for the model.
- Update Context: After generating a response, update the stored context with the new user message and the bot’s response.

### Example

> Here’s a simplified example using Python and a database like Azure SQL. For more information on how to connect to the SQL database click [here](https://learn.microsoft.com/en-us/azure/azure-sql/database/azure-sql-python-quickstart?view=azuresql&tabs=windows%2Csql-auth#add-code-to-connect-to-azure-sql-database). For more about Azure OpenAI On Your Data API click [here](https://learn.microsoft.com/en-us/azure/ai-services/openai/references/on-your-data?tabs=python)

```python
import pyodbc

# Define the connection string for Azure SQL database
# Please replace the placeholders with your actual Azure SQL database credentials
connection_string = (
    "Driver={ODBC Driver 17 for SQL Server};"
    "Server=your_server.database.windows.net;"
    "Database=your_database;"
    "Uid=your_username;"
    "Pwd=your_password;"
    "Encrypt=yes;"
    "TrustServerCertificate=no;"
    "Connection Timeout=30;"
)

def get_db_connection():
    ## Establish a connection to the Azure SQL database.## 
    try:
        conn = pyodbc.connect(connection_string)
        return conn
    except pyodbc.Error as e:
        print(f"Error connecting to database: {e}")
        return None

def create_table():
    ## Create the context table if it doesn't exist.## 
    with get_db_connection() as conn:
        if conn:
            with conn.cursor() as cursor:
                cursor.execute('''
                IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'context')
                BEGIN
                    CREATE TABLE context (
                        user_id NVARCHAR(255) PRIMARY KEY,
                        conversation NVARCHAR(MAX)
                    )
                END
                ''')
                conn.commit()

def store_context(user_id, conversation):
    ## Store the conversation context in the database.## 
    with get_db_connection() as conn:
        if conn:
            with conn.cursor() as cursor:
                cursor.execute('''
                MERGE INTO context AS target
                USING (SELECT ? AS user_id, ? AS conversation) AS source
                ON (target.user_id = source.user_id)
                WHEN MATCHED THEN 
                    UPDATE SET conversation = source.conversation
                WHEN NOT MATCHED THEN 
                    INSERT (user_id, conversation) VALUES (source.user_id, source.conversation);
                ''', (user_id, conversation))
                conn.commit()

def retrieve_context(user_id):
    ## Retrieve the conversation context from the database.## 
    with get_db_connection() as conn:
        if conn:
            with conn.cursor() as cursor:
                cursor.execute('SELECT conversation FROM context WHERE user_id = ?', (user_id,))
                result = cursor.fetchone()
                return result[0] if result else ""
```

> Integrating with Azure OpenAI:

> [!TIP]
> Use the Azure OpenAI API to send the prompt and receive the response. Click [here](https://learn.microsoft.com/en-us/azure/ai-services/openai/quickstart?tabs=command-line%2Cpython-new&pivots=programming-language-python) if want to see more.

```python
import os
from openai import AzureOpenAI
    
client = AzureOpenAI(
    api_key=os.getenv("AZURE_OPENAI_API_KEY"),  
    api_version="2024-02-01",
    azure_endpoint = os.getenv("AZURE_OPENAI_ENDPOINT")
    )

#This will correspond to the custom name you chose for your deployment when you deployed a model. 
deployment_name='REPLACE_WITH_YOUR_DEPLOYMENT_NAME'

# Function to send prompt to the model
# Send a completion call to generate an answer
def send_to_model(prompt):
    print('Sending a test completion job')
    start_phrase = 'Write a tagline for an ice cream shop. '
    response = client.completions.create(model=deployment_name, prompt=start_phrase, max_tokens=10)
    print(start_phrase+response.choices[0].text)
    return response.choices[0].text.strip()

# Example usage
user_id = "user123"
new_message = "Hello, how are you?"

# Retrieve existing context
context = retrieve_context(user_id)

# Combine context with new message
full_prompt = context + "\nUser: " + new_message

# Send full_prompt to the model and get response
response = send_to_model(full_prompt)

# Update context
new_context = full_prompt + "\nBot: " + response
store_context(user_id, new_context)
```

### Other considerations:

- To enhance context management, consider truncating older parts of the conversation, summarizing previous discussions, and using tokens effectively to manage prompt size.
- For security and privacy, ensure the stored context is secure and adheres to privacy laws by encrypting sensitive data, implementing access controls, and ensuring compliance with data protection regulations like GDPR and CCPA.

## Wiki

- [Create and deploy an Azure OpenAI Service resource](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/create-resource?pivots=web-portal)
- [Quickstart: Get started generating text using Azure OpenAI Service](https://learn.microsoft.com/en-us/azure/ai-services/openai/quickstart?tabs=command-line%2Cpython-new&pivots=programming-language-python)
- [How To Set Up and Configure a GPT Deployment Using the Azure OpenAI Service](https://aka.ms/setup-gpt-aoai)
- [Choose the right chatbot solution for your use case](https://learn.microsoft.com/en-us/azure/bot-service/bot-overview?view=azure-bot-service-4.0)
- [How to build chatbots that deliver better customer experiences and help support a surge in inquiries](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/how-to-build-chatbots-that-deliver-better-customer-experiences/ba-p/1374659)
- [Baseline OpenAI End-to-End Chat Reference Architecture](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/baseline-openai-e2e-chat): This article provides a comprehensive architecture for building and deploying enterprise chat applications using Azure OpenAI Service language models. It includes details on using Azure Machine Learning prompt flow to create executable flows.
- [No-Code Chatbot Creation Guide](https://techcommunity.microsoft.com/t5/startups-at-microsoft/how-to-set-up-the-microsoft-chatbot-template-and-azure-openai/ba-p/3849936): This step-by-step guide walks you through creating a professional chatbot without any coding knowledge using the Microsoft Azure OpenAI Service Chatbot Template.
- [Simple Chat Application using Azure OpenAI](https://learn.microsoft.com/en-us/samples/azure-samples/openai-chat-app-quickstart/openai-chat-app-quickstart/): This repository includes a Python app that uses Azure OpenAI to generate responses to user messages. It covers all the infrastructure and configuration needed to provision Azure OpenAI resources and deploy the app to Azure Container Apps.
- [Build language model pipelines with memory](https://learn.microsoft.com/en-us/azure/architecture/ai-ml/openai/guide/language-model-pipelines)

  <img width="800" alt="image" src="https://github.com/user-attachments/assets/ccf7893d-53e6-4bbd-980a-192c5f8340fe">

- [Strategies for Optimizing High-Volume Token Usage with Azure OpenAI](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/strategies-for-optimizing-high-volume-token-usage-with-azure/ba-p/4007751)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
