# Automated PDF Invoice Processing using <br/> Azure Storage + Document Intelligence + Cosmos DB

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-26

----------

> How to parse PDFs from an Azure Storage Account, process them using Azure Document Intelligence, and store the results in Cosmos DB. <br/> <br/>
> 1. Upload your PDFs to an Azure Blob Storage container. <br/>
> 2. An Azure Function is triggered by the upload, which calls the Azure Document Intelligence API to analyze the PDFs.  <br/>
> 3. The extracted data is parsed and subsequently stored in a Cosmos DB database, ensuring a seamless and automated workflow from document upload to data storage. 

> [!NOTE]
> Advantages of Document Intelligence for organizations handling with large volumes of documents: <br/>
> - Utilizes natural language processing, computer vision, deep learning, and machine learning. <br/>
> - Handles structured, semi-structured, and unstructured documents. <br/>
> - Automates the extraction and transformation of data into usable formats like JSON or CSV

<img width="550" alt="image" src="https://github.com/user-attachments/assets/21ec5d04-1c9b-4273-ad98-7b46186de78e">

## Wiki 

<details>
<summary><b>Table of Wiki</b> (Click to expand)</summary>

- [Azure AI Document Intelligence documentation](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/?view=doc-intel-4.0.0)
- [Get started with the Document Intelligence Sample Labeling tool](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/v21/try-sample-label-tool?view=doc-intel-2.1.0#prerequisites-for-training-a-custom-form-model)
- [Document Intelligence Sample Labeling tool](https://fott-2-1.azurewebsites.net/)
- [Assign an Azure role for access to blob data](https://learn.microsoft.com/en-us/azure/storage/blobs/assign-azure-role-data-access?tabs=portal)
- [Build and train a custom extraction model](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/how-to-guides/build-a-custom-model?view=doc-intel-2.1.0)
- [Compose custom models - Document Intelligence](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/how-to-guides/compose-custom-models?view=doc-intel-2.1.0&tabs=studio)
- [Deploy the Sample Labeling tool](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/v21/deploy-label-tool?view=doc-intel-2.1.0)
- [Train a custom model using the Sample Labeling tool](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/v21/label-tool?view=doc-intel-2.1.0)
- [Train models with the sample-labeling tool](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/v21/supervised-table-tags?view=doc-intel-2.1.0)
- [Azure Cosmos DB - Database for the AI Era](https://learn.microsoft.com/en-us/azure/cosmos-db/introduction)
- [Consistency levels in Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels)
- [Azure Cosmos DB SQL API client library for Python](https://learn.microsoft.com/en-us/python/api/overview/azure/cosmos-readme?view=azure-python)
- [CosmosClient class documentation](https://learn.microsoft.com/en-us/python/api/azure-cosmos/azure.cosmos.cosmos_client.cosmosclient?view=azure-python)
- [Cosmos AAD Authentication](https://learn.microsoft.com/en-us/python/api/overview/azure/cosmos-readme?view=azure-python#aad-authentication)
- [Cosmos python examples](https://learn.microsoft.com/en-us/python/api/overview/azure/cosmos-readme?view=azure-python#examples)
- [Use control plane role-based access control with Azure Cosmos DB for NoSQL](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/security/how-to-grant-control-plane-role-based-access?tabs=built-in-definition%2Ccsharp&pivots=azure-interface-portal)
- [Use data plane role-based access control with Azure Cosmos DB for NoSQL](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/security/how-to-grant-data-plane-role-based-access?tabs=built-in-definition%2Ccsharp&pivots=azure-interface-cli)
- [Create or update Azure custom roles using Azure CLI](https://learn.microsoft.com/en-us/azure/role-based-access-control/custom-roles-cli)

</details>

## Content 

- [Wiki](#wiki)
- [Content](#content)
- [Overview](#overview)
- [Step 1: Set Up Your Azure Environment](#step-1-set-up-your-azure-environment)
- [Step 2: Set Up Azure Blob Storage for PDF Ingestion](#step-2-set-up-azure-blob-storage-for-pdf-ingestion)
  - [Create a Storage Account:](#create-a-storage-account)
  - [Create a Blob Container](#create-a-blob-container)
  - [Allow storage account key access](#allow-storage-account-key-access)
- [Step 3: Set Up Azure Cosmos DB](#step-3-set-up-azure-cosmos-db)
  - [Create a Cosmos DB Account:](#create-a-cosmos-db-account)
  - [Create a Database and Container](#create-a-database-and-container)
- [Step 4: Set Up Azure Document Intelligence](#step-4-set-up-azure-document-intelligence)
  - [Create Document Intelligence Resource](#create-document-intelligence-resource)
  - [Configure Models](#configure-models)
      - [Using Prebuilt Models](#using-prebuilt-models)
      - [Training Custom Models](#training-custom-models-optionalif-needed) (optional/if needed)
- [Step 5: Set Up Azure Functions for Document Ingestion and Processing](#step-5-set-up-azure-functions-for-document-ingestion-and-processing)
  - [Create a Function App](#create-a-function-app)
  - [Configure/Validate the Environment variables](#configurevalidate-the-environment-variables)
  - [Develop the Function](#develop-the-function)
- [Step 6: Test the solution](#step-6-test-the-solution)

## Overview 

> `Azure Document Intelligence`, formerly known as **Form Recognizer**, is a powerful AI service that extracts structured data from documents. It `uses machine learning models to analyze and process various types of documents, such as invoices, receipts, business cards`, and more.

| Key Features | Details |
| --- | --- |
| **Prebuilt Models** | - **Invoice Model**: Extracts fields like invoice ID, date, vendor information, line items, totals, and more.<br/>- **Receipt Model**: Extracts merchant name, transaction date, total amount, and line items.<br/>- **Business Card Model**: Extracts contact information such as name, company, phone number, and email. |
| **Custom Models** | - **Training**: You can train custom models using labeled data. This involves uploading a set of documents and manually labeling the fields you want to extract.<br/>- **Model Management**: Manage versions of your custom models, retrain them with new data, and evaluate their performance. |
| **APIs and SDKs** | - **REST API**: Provides endpoints for analyzing documents, managing models, and retrieving results.<br/>- **SDKs**: Available in multiple languages (e.g., Python, C#, JavaScript) to simplify integration into your applications. |

> [!IMPORTANT]
> Regarding `Networking`, this example will cover `Public access configuration`, and `system-managed identity`. However, please ensure you `review your privacy requirements and adjust network and access settings as necessary for your specific case`.

## Step 1: Set Up Your Azure Environment

> An Azure `Resource Group` is a `container that holds related resources for an Azure solution`.
> It can include all the resources for the solution or only those you want to manage as a group.
> Typically, resources that share the same lifecycle are added to the same resource group, allowing for easier deployment, updating, and deletion as a unit.
> Resource groups also store metadata about the resources, and you can apply access control, locks, and tags to them for better management and organization.

1. **Create an Azure Account**: If you don't have one, sign up for an Azure account.
2. **Create a Resource Group**:
   - Go to the Azure portal.
   - Navigate to **Resource groups**.
   - Click **+ Create**.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/56d1e99f-0a22-4492-bd6f-d4e3a76aedd8">

   - Enter the Resource Group name (e.g., `RGContosoAIDoc`) and select a region (e.g., `East US 2`). You can add tags if needed.
   - Click **Review + create** and then **Create**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/288d05ca-e5e3-47f7-9c0d-3ddb0fffe518">

## Step 2: Set Up Azure Blob Storage for PDF Ingestion

### Create a Storage Account:

> An `Azure Storage Account` provides a `unique namespace in Azure for your data, allowing you to store and manage various types of data such as blobs, files, queues, and tables`. It serves as the foundation for all Azure Storage services, ensuring high availability, scalability, and security for your data. <br/> <br/>

- In the Azure portal, navigate to your **Resource Group**.
- Click **+ Create**.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/1998660c-bb80-4ea7-9865-b6cdfa125d02">

- Search for `Storage Account`.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/0bde893e-a40e-4dd6-bf55-964c33109e33">

- Select the Resource Group you created.
- Enter a Storage Account name (e.g., `invoicecontosostorage`).
- Choose the region and performance options, and click `Next` to continue.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/bb5aeccc-e35f-45f2-a2a5-1000d92aa73a">

- If you need to modify anything related to `Security, Access protocols, Blob Storage Tier`, you can do that in the `Advanced` tab.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/a478525f-6028-4f12-8b99-a441ed99fe0f">

- Regarding `Networking`, this example will cover `Public access` configuration. However, please ensure you review your privacy requirements and adjust network and access settings as necessary for your specific case.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/0273e197-6e5b-4a1c-93cc-7597730c384b">

- Click **Review + create** and then **Create**. Once is done, you'll be able to see it in your Resource Group.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/a168a63b-2d15-4643-8200-34bf8335a0fe">

### Create a Blob Container

> A `Blob Container` is a `logical grouping of blobs within an Azure Storage Account, similar to a directory in a file system`. Containers help organize and manage blobs, which can be any type of unstructured data like text or binary data. Each container can store an unlimited number of blobs, and you must create a container before uploading any blobs.

Within the Storage Account, create a Blob Container to store your PDFs.

- Go to your Storage Account.
- Under **Data storage**, select **Containers**.
- Click **+ Container**.
- Enter a name for the container (e.g., `pdfinvoices`) and set the public access level to **Private**.
- Click **Create**.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/27b024f8-0390-4331-bc34-59c3831d9bd1">

### Allow storage account key access

> If you plan to use access keys, please ensure that the setting "Allow storage account key access" is enabled. When this setting is disabled, any requests to the account authorized with Shared Key, including shared access signatures (SAS), will be denied. Click [here to learn more](https://learn.microsoft.com/en-us/azure/storage/common/shared-key-authorization-prevent?tabs=portal)

<img width="550" alt="image" src="https://github.com/user-attachments/assets/47e74073-1b58-4d4a-b898-7be91b9314b7">

## Step 3: Set Up Azure Cosmos DB

### Create a Cosmos DB Account:

> `Azure Cosmos DB` is a globally distributed,` multi-model database service provided by Microsoft Azure`. It is designed to offer high availability, scalability, and low-latency access to data for modern applications. Unlike traditional relational databases, Cosmos DB is a `NoSQL database, meaning it can handle unstructured, semi-structured, and structured data types`. `It supports multiple data models, including document, key-value, graph, and column-family, making it versatile for various use cases.` <br/> <br/>

- In the Azure portal, navigate to your **Resource Group**.
- Click **+ Create**.
- Search for `Cosmos DB`, click on `Create`:
  
   <img width="550" alt="image" src="https://github.com/user-attachments/assets/ecdb9a17-5623-4dc0-a607-92448950b7a0">

- Choose your desired API type, for this will be using `Azure Cosmos DB for NoSQL`. This option supports a SQL-like query language, which is familiar and powerful for querying and analyzing your invoice data. It also integrates well with various client libraries, making development easier and more flexible.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/db942359-8a81-4289-9ea7-91234b4c3802">

- Please enter an account name (e.g., `contosoinvoiceaicosmos`). As with the previously configured resources, we will use the `Public network` for this example. Ensure that you adjust the architecture to include your networking requirements.
- Select the region and other settings.
- Click **Review + create** and then **Create**.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/47948255-3988-42f3-8e4e-80291aefaf5b">

### Create a Database and Container

> An `Azure Cosmos DB container` is a `logical unit` within a Cosmos DB database where data is stored. `Containers are schema-agnostic, meaning they can store items with different structures. Each container is automatically partitioned to scale out across multiple servers, providing virtually unlimited throughput and storage`. Containers are the primary scalability unit in Cosmos DB, and they use a partition key to distribute data efficiently across partitions.

- Go to your Cosmos DB account.
- Under **Data Explorer**, click **New Database**.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/d0130cf2-aaf8-4a63-9786-4c65bc700812">

- Enter a database name (e.g., `ContosoDBDocIntellig`) and click **OK**.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/7839be4d-8d4d-476e-9d81-203b0fd2426f">

- Click **New Container**.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/24e08dca-3399-40d2-a91d-95a6569156ad">

- Enter a container name (e.g., `Invoices`) and set the partition key (e.g., `/transactionId`).
- Click **OK**.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/96ffc93a-078b-49f9-ad4a-470e73540c30">

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/203f4e0d-6697-4200-83bc-65f0023addb5">

## Step 4: Set Up Azure Document Intelligence

> `Azure Document Intelligence` offers robust capabilities for `extracting structured data from various document types using advanced machine learning models`. Technically, it provides `prebuilt models` for `common documents like invoices, receipts, and business cards, which can quickly extract key information without custom training. For more specific needs`, it allows `training custom models using labeled data, enabling precise extraction tailored to unique document formats`. The service is accessible via `REST APIs and SDKs` in multiple languages, facilitating seamless integration into applications. It supports `key-value pair extraction`, `table recognition`, and `text extraction`, making it a powerful tool for automating data entry, enhancing document management systems, and streamlining business processes.

### Create Document Intelligence Resource

- Go to the Azure Portal.
- **Create a New Resource**:
   - Click on `Create a resource` and search for `document intelligence`.
   - Select `Document Intelligence` and click `Create`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/e8783321-9bf3-42e2-83af-4d1c555205e3">

- **Configure the Resource**:
   - **Subscription**: Select your Azure subscription.
   - **Resource Group**: Choose an existing resource group or create a new one.
   - **Region**: Select the region closest to your location.
   - **Name**: Provide a unique name for your Form Recognizer resource.
   - **Pricing Tier**: Choose the pricing tier that fits your needs (e.g., Standard S0).
- Review your settings and click `Create` to deploy the resource.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/08335330-e9f5-455b-be22-6b938b979d99">

### Configure Models

#### Using Prebuilt Models
- **Access Form Recognizer Studio**:
   - Navigate to your Form Recognizer resource in the Azure Portal.
   - Check your `Resource Group` if needed:

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/d3559dc5-dbcb-44e6-b56d-d097d1719576">

   - Under `Overview`, click on `Go to Document Intelligence Studio`: 

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/286545a3-574d-48d4-80de-66a58e5b5405">

- **Select Prebuilt Models**: Choose the prebuilt model that matches your document type (e.g., "Invoices" for your PDF example).

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/61b8fc8c-4fe2-4b28-a8bc-8459eb6bc9c3">

- If the service resource for usage and billing is not configured, a window will appear requesting the resource information. In this case, we will use the one we recently created.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/f88bce37-d7f3-4312-9053-e06f0743cdb3">

- **Analyze Document**:
   - Upload your PDF document to the Form Recognizer Studio.
     
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/575cb5d1-8e3b-4855-8f15-246ee1ea13b8">

   - Click on `Run analysis`, the prebuilt model will automatically extract fields such as invoice ID, date, vendor information, line items, and totals.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/483ff4a5-73d3-4dcd-b35d-766f34a648b2">

   - Validate your results:

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/a945bd72-ea1c-4d33-9699-f9257a2ceffa">

  #### Training Custom Models (optional/if needed):
- **Prepare Training Data**:
   - Collect a set of sample documents similar to your PDF example.
   - Label the fields you want to extract using the [Form Recognizer Labeling Tool](https://fott-2-1.azurewebsites.net/). Click [here for more information about to use it](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/v21/try-sample-label-tool?view=doc-intel-2.1.0#prerequisites-for-training-a-custom-form-model).

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/94fca855-ec1b-444c-91f0-e05de13600df">

- **Upload Training Data**: Upload the labeled documents to an Azure Blob Storage container.
- Grant the necessary role (`Storage Blob Data Reader`) to the Document Intelligence Account for the Storage Account to access the information. Otherwise, you may encounter an error like this:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/16feb31b-2a0e-4060-8e57-c870240a5109">

   - For this example we'll be using the system assigned identity to do that. Under `Identy` within your `Document Intelligence Account`, change the status to `On`, and click on `Save`:

      > A system assigned managed identity is restricted to `one per resource and is tied to the lifecycle of this resource`. `You can grant permissions to the managed identity by using Azure role-based access control (Azure RBAC). The managed identity is authenticated with Microsoft Entra ID, so you don’t have to store any credentials in code`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/4be26e42-b9d4-4f04-ae5e-e8e6babd9366">

   - Go to your `Storage Account`, under `Access Control (IAM)` click on `+ Add`, and then `Add role assigment`:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/59881d40-eb4c-4276-b3d3-d5e7dd877af0">

   - Search for `Storage Blob Data Reader`, click `Next`. Then, click on `select members` and search for your `Document intelligence identity`. Finally click on `Review + assign`:

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/e8bbe706-8ecc-41bd-a189-846e82ccef01">

- In the Form Recognizer Studio, select `Custom extraction model`.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/61c190d3-f795-4ac6-ab73-73e7e83b9dcc">

- Scroll down, and click on `Create a project` (e.g, `pdfinvoiceproject`, `Extract information from pdf invoices`):

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/4d8eb2f1-a05e-47ca-b7a0-0f850a093e5f">

- Configure the service resource for the project, choose `subscription`, `resource group`, `Document Intelligence or Cognitive Service Resource` and the `api version`.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/6a100714-844e-4a2a-a875-c50da88bc889">

- Connect training data source: Provide the information of the Azure Blob Storage account and the folder that contains your training data.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/f15a9908-8710-4a3e-a457-8d557c8f2f48">

- You can also `Auto label` if it's required:
      
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/8552060b-f241-4d06-9a51-98b3b2171c08">

- **Test the Model**:
   - Upload a new document to test the custom model.
   - Verify that the model correctly extracts the desired fields.

## Step 5: Set Up Azure Functions for Document Ingestion and Processing

> An `Azure Function App` is a `container for hosting individual Azure Functions`. It provides the execution context for your functions, allowing you to manage, deploy, and scale them together. `Each function app can host multiple functions, which are small pieces of code that run in response to various triggers or events, such as HTTP requests, timers, or messages from other Azure services`. <br/> <br/>
> Azure Functions are designed to be lightweight and event-driven, enabling you to build scalable and serverless applications. `You only pay for the resources your functions consume while they are running, making it a cost-effective solution for many scenarios`.

 ### Create a Function App
- In the Azure portal, go to your **Resource Group**.
- Click **+ Create**.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/7796ccf9-808d-487a-85cc-ec8bc382a7aa">

- Search for `Function App`, click on `Create`:

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/7c5ce746-06b7-4dd8-992f-edc597ea6c27">

- Choose a `hosting option`; for this example, we will use `Functions Premium`. Click [here for a quick overview of hosting options](https://github.com/brown9804/MicrosoftCloudEssentialsHub/tree/parsePDFDocIntellig/0_Azure/3_AzureAI/14_AIUseCases/0_PDFProcessingFAOF#function-app-hosting-options):
        
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/11fabed8-1219-4090-9ba8-a79a41f2830a">

- Enter a name for the Function App (e.g., `ContosoFAaiDocIntellig`).
- Choose your runtime stack (e.g., `.NET` or `Python`).
- Select the region and other settings.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/7e5dbc3c-6ee9-4272-95d4-243c7cca68d9">

- Select **Review + create** and then **Create**. Verify the resources created in your `Resource Group`.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/002620d0-4040-4289-ad56-3e5d4d6ff3c7">

 > [!IMPORTANT]
 > This example is using system-assigned managed identity to assign RBACs (Role-based Access Control).
 > <img width="550" alt="image" src="https://github.com/user-attachments/assets/46fe06d4-d978-4743-801d-59c197fa4717">

- Please assign the `Storage Blob Data Contributor` and `Storage File Data SMB Share Contributor` roles to the `Function App` within the `Storage Account` related to the runtime (the one created with the function app).

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/a08f77bf-71d4-4922-8001-cf402e9e81f2">

- Assign `Storage Blob Data Reader` to the `Function App` within the `Storage Account` that will contains the invoices, click `Next`. Then, click on `select members` and search for your `Function App` identity. Finally click on `Review + assign`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/dcfdd7f0-f7a6-4829-876a-87383887e0e2">

- Also add `Cosmos DB Operator`, `DocumentDB Account Contributor`, `Azure AI Administrator`, `Cosmos DB Account Reader Role`, `Contributor`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/7570747e-a5f1-4090-98ce-b44928ef1f57">

- To assign the `Microsoft.DocumentDB/databaseAccounts/readMetadata` permission, you need to create a custom role in Azure Cosmos DB. This permission is required for accessing metadata in Cosmos DB. Click [here to understand more about it](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/security/how-to-grant-data-plane-role-based-access?tabs=built-in-definition%2Ccsharp&pivots=azure-interface-cli#prepare-role-definition).

    | **Aspect**         | **Data Plane Access**                                                                 | **Control Plane Access**                                                                 |
    |--------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
    | **Scope**          | Focuses on `data operations` within databases and containers. This includes actions such as reading, writing, and querying data in your databases and containers. | Focuses on `management operations` at the account level. This includes actions such as creating, deleting, and configuring databases and containers. |
    | **Roles**          | - `Cosmos DB Built-in Data Reader`: Provides read-only access to data within the databases and containers. <br> - `Cosmos DB Built-in Data Contributor`: Allows read and write access to data within the databases and containers. <br> - `Cosmos DB Built-in Data Owner`: Grants full access to manage data within the databases and containers. | - `Contributor`: Grants full access to manage all Azure resources, including Cosmos DB. <br> - `Owner`: Grants full access to manage all resources, including the ability to assign roles in Azure RBAC. <br> - `Cosmos DB Account Contributor`: Allows management of Cosmos DB accounts, including creating and deleting databases and containers. <br> - `Cosmos DB Account Reader`: Provides read-only access to Cosmos DB account metadata. |
    | **Permissions**    | - `Reading documents` <br> - `Writing documents` <br> - Managing data within containers. | - `Creating or deleting databases and containers` <br> - Configuring settings <br> - Managing account-level configurations. |
    | **Authentication** | Uses `Azure Active Directory (AAD) tokens` or `resource tokens` for authentication.                      | Uses `Azure Active Directory (AAD)` for authentication.                                 |

> Steps to assing it:

1. **Open Azure CLI**: Go to the [Azure portal](portal.azure.com) and click on the icon for the Azure CLI.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/b2643d9a-7364-454a-bb24-f16270e99d92">

2. **List Role Definitions**: Run the following command to list all of the role definitions associated with your Azure Cosmos DB for NoSQL account. Review the output and locate the role definition named `Cosmos DB Built-in Data Contributor`.

     ```powershell
     az cosmosdb sql role definition list \
         --resource-group "<your-resource-group>" \
         --account-name "<your-account-name>"
     ```
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/4c19d70e-d525-4c15-bb0e-518f50f61b37">
    

3. **Get Cosmos DB Account ID**: Run this command to get the ID of your Cosmos DB account. Record the value of the `id` property as it is required for the next step.

     ```powershell
     az cosmosdb show --resource-group "<your-resource-group>" --name "<your-account-name>" --query "{id:id}"
     ```

     Example output:
    
     ```json
    {                                                               
      "id": "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DocumentDB/databaseAccounts/{cosmos-account-name}"
    }     
     ```
    
     <img width="750" alt="image" src="https://github.com/user-attachments/assets/f3426130-2de5-46a0-96f0-4c6e15e57975">

4. **Assign the Role**: Assign the new role using `az cosmosdb sql role assignment create`. Use the previously recorded role definition ID for the `--role-definition-id` argument, the unique identifier for your identity for the `--principal-id` argument, and your account's ID for the `--scope` argument.
  
     > You can extract the `principal-id`, from `Identity` of the `Function App`:
    
      <img width="550" alt="image" src="https://github.com/user-attachments/assets/b54f046f-ecc7-4434-80ce-e49a0abeca66">
    
     ```powershell
     az cosmosdb sql role assignment create \
         --resource-group "<your-resource-group>" \
         --account-name "<your-account-name>" \
         --role-definition-id "<role-definition-id>" \
         --principal-id "<principal-id>" \
         --scope "/subscriptions/{subscriptions-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DocumentDB/databaseAccounts/{cosmos-account-name}"
     ```

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/72e1e4f9-9228-4ec0-aade-20ad4aaa1f4f">
    
    > After a few minutes, you will see something like this:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/5caea3b9-3e4d-4791-8376-fda4547547bd">

5. **Verify Role Assignment**: Use `az cosmosdb sql role assignment list` to list all role assignments for your Azure Cosmos DB for NoSQL account. Review the output to ensure your role assignment was created.
    
     ```powershell
     az cosmosdb sql role assignment list \
         --resource-group "<your-resource-group>" \
         --account-name "<your-account-name>"
     ```

    <img width="750" alt="image" src="https://github.com/user-attachments/assets/8c7675cf-8183-433c-a21b-f9b7029642d9">

### Configure/Validate the Environment variables

- Under `Settings`, go to `Environment variables`. And `+ Add` the following variables:

  -  `COSMOS_DB_ENDPOINT`: Your Cosmos DB account endpoint.
  -  `COSMOS_DB_KEY`: Your Cosmos DB account key.
  -  `COSMOS_DB_CONNECTION_STRING`: Your Cosmos DB connection string.
  -  `invoicecontosostorage_STORAGE`: Your Storage Account connection string.
  -  `FORM_RECOGNIZER_ENDPOINT`: For example: `https://<your-form-recognizer-endpoint>.cognitiveservices.azure.com/`
  -  `FORM_RECOGNIZER_KEY`: Your Documment Intelligence Key (Form Recognizer).
  -  `FUNCTIONS_EXTENSION_VERSION`: ~4 (Review the existence of this, if not create it)
  -  `FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR`: true (This setting ensures that all entry point errors are visible in your application insights logs).

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/31d813e7-38ba-46ff-9e4b-d091ae02706a">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/45313857-b337-4231-9184-d2bb46e19267">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/074d2fa5-c64d-43bd-8ed7-af6da46d86a2">

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/ec5d60f3-5136-489d-8796-474b7250865d">

  - Click on `Apply` to save your configuration.
    
      <img width="550" alt="image" src="https://github.com/user-attachments/assets/437b44bb-7735-4d17-ae49-e211eca64887">

### Develop the Function

- You need to install [VSCode](https://code.visualstudio.com/download)
- Install python from Microsoft store:
    
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/30f00c27-da0d-400f-9b98-817fd3e03b1c">

- Open VSCode, and install some extensions: `python`, and `Azure Tools`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/715449d3-1a36-4764-9b07-99421fb1c834">

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/854aa665-dc2f-4cbf-bae2-2dc0a8ef6e46">

- Click on the `Azure` icon, and `sign in` into your account. Allow the extension `Azure Resources` to sign in using Microsoft, it will open a browser window. After doing so, you will be able to see your subscription and resources.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/4824ca1c-4959-4242-95af-ad7273c5530d">

- Under Workspace, click on `Create Function Project`, and choose a path in your local computer to develop your function.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/2c42d19e-be8b-48ef-a7e4-8a39989cea5a">

- Choose the language, in this case is `python`:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/2fb19a1e-bb2d-47e5-a56e-8dc8a708647a">

- Select the model version, for this example let's use `v2`:
  
   <img width="550" alt="image" src="https://github.com/user-attachments/assets/fd46ee93-d788-463d-8b28-dbf2487e9a7f">

- For the python interpreter, let's use the one installed via `Microsoft Store`:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/3605c959-fc59-461f-9e8d-01a6a92004a8">

- Choose a template (e.g., **Blob trigger**) and configure it to trigger on new PDF uploads in your Blob container.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/0a4ed541-a693-485c-b6ca-7d5fb55a61d2">

- Provide a function name, like `BlobTriggerContosoPDFInvoicesDocIntelligence`:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/263cef5c-4460-46cb-8899-fb609b191d81">

- Next, it will prompt you for the path of the blob container where you expect the function to be triggered after a file is uploaded. In this case is `pdfinvoices` as was previously created.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/7005dc44-ffe2-442b-8373-554b229b3042">

- Click on `Create new local app settings`, and then choose your subscription.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/07c211d6-eda0-442b-b428-cdaed2bf12ac">

- Choose `Azure Storage Account for remote storage`, and select one. I'll be using the `invoicecontosostorage`. 

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/3b5865fc-3e84-4582-8f06-cb5675d393f0">

- Then click on `Open in the current window`. You will see something like this:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/f30e8e10-0c37-4efc-8158-c83faf22a7d8">

- Now we need to update the function code to extract data from PDFs and store it in Cosmos DB, use this an example:

   > 1. **PDF Upload**: A PDF is uploaded to the Azure Blob Storage container named `pdfinvoices`.
   > 2. **Trigger Azure Function**: The upload triggers the Azure Function `BlobTriggerContosoPDFInvoicesDocIntelligence`.
   > 3. **Initialize Clients**: Sets up connections to Document Intelligence and Cosmos DB. <br/>
   >       - The function initializes the `DocumentAnalysisClient` to interact with Azure Document Intelligence. <br/>
   >       - It also initializes the `CosmosClient` to interact with Cosmos DB. <br/>
   > 4. **Read PDF from Blob Storage**: The function reads the PDF content from the Blob Storage into a byte stream.
   > 5. **Analyze PDF**: Uses Document Intelligence to extract data. <br/>
   >      - The function calls the `begin_analyze_document` method of the `DocumentAnalysisClient` using the prebuilt invoice model to analyze the PDF. <br/>
   >      - It waits for the analysis to complete and retrieves the results. <br/>
   > 6. **Extract Data**: Structures the extracted data. <br/>
   >       - The function extracts relevant fields from the analysis result, such as customer name, email, address, company name, phone, address, and rental details. <br/>
   >       - It structures this extracted data into a dictionary (`invoice_data`). <br/>
   > 7. **Save Data to Cosmos DB**: Inserts the data into Cosmos DB. <br/>
   >       - The function calls `save_invoice_data_to_cosmos` to save the structured data into Cosmos DB. <br/>
   >       - It ensures the database and container exist, then inserts the extracted data. <br/>
   > 8. **Logging (process and errors)**: Throughout the process, the function logs various steps and any errors encountered for debugging and monitoring purposes.

   - Update the function_app.py:

      | Template Blob Trigger | Function Code updated |
      | --- | --- |
      |   <img width="550" alt="image" src="https://github.com/user-attachments/assets/07a7b285-eed2-4b42-bb1f-e41e8eafd273"> |  <img width="550" alt="image" src="https://github.com/user-attachments/assets/d364591b-817e-4f36-8c50-7de187c32a1e">|
      
      <details>
      <summary><b>Function Code </b> (Click to expand)</summary>

     ```python
      import logging
      import azure.functions as func
      from azure.ai.formrecognizer import DocumentAnalysisClient
      from azure.core.credentials import AzureKeyCredential
      from azure.cosmos import CosmosClient, PartitionKey, exceptions
      from azure.identity import DefaultAzureCredential
      import os
      import uuid
      
      app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
      
      ## DEFINITIONS 
      def initialize_form_recognizer_client():
          endpoint = os.getenv("FORM_RECOGNIZER_ENDPOINT")
          key = os.getenv("FORM_RECOGNIZER_KEY")
          if not isinstance(key, str):
              raise ValueError("FORM_RECOGNIZER_KEY must be a string")
          logging.info(f"Form Recognizer endpoint: {endpoint}")
          return DocumentAnalysisClient(endpoint=endpoint, credential=AzureKeyCredential(key))
      
      def read_pdf_content(myblob):
          logging.info(f"Reading PDF content from blob: {myblob.name}")
          return myblob.read()
      
      def analyze_pdf(form_recognizer_client, pdf_bytes):
          logging.info("Starting PDF analysis.")
          poller = form_recognizer_client.begin_analyze_document(
              model_id="prebuilt-invoice",
              document=pdf_bytes
          )
          logging.info("PDF analysis in progress.")
          return poller.result()
      
      def extract_invoice_data(result):
          logging.info("Extracting invoice data from analysis result.")
          invoice_data = {
              "id": str(uuid.uuid4()),
              "customer_name": "",
              "customer_email": "",
              "customer_address": "",
              "company_name": "",
              "company_phone": "",
              "company_address": "",
              "rentals": []
          }
      
          def serialize_field(field):
              if field:
                  return str(field.value)  # Convert to string
              return ""
          
          for document in result.documents:
              fields = document.fields
              invoice_data["customer_name"] = serialize_field(fields.get("CustomerName"))
              invoice_data["customer_email"] = serialize_field(fields.get("CustomerEmail"))
              invoice_data["customer_address"] = serialize_field(fields.get("CustomerAddress"))
              invoice_data["company_name"] = serialize_field(fields.get("VendorName"))
              invoice_data["company_phone"] = serialize_field(fields.get("VendorPhoneNumber"))
              invoice_data["company_address"] = serialize_field(fields.get("VendorAddress"))
      
              items = fields.get("Items").value if fields.get("Items") else []
              for item in items:
                  item_value = item.value if item.value else {}
                  rental = {
                      "rental_date": serialize_field(item_value.get("Date")),
                      "title": serialize_field(item_value.get("Description")),
                      "description": serialize_field(item_value.get("Description")),
                      "quantity": serialize_field(item_value.get("Quantity")),
                      "total_price": serialize_field(item_value.get("TotalPrice"))
                  }
                  invoice_data["rentals"].append(rental)
      
          logging.info(f"Successfully extracted invoice data: {invoice_data}")
          return invoice_data
      
      def save_invoice_data_to_cosmos(invoice_data):
          try:
              endpoint = os.getenv("COSMOS_DB_ENDPOINT")
              key = os.getenv("COSMOS_DB_KEY")
              aad_credentials = DefaultAzureCredential()
              client = CosmosClient(endpoint, credential=aad_credentials, consistency_level='Session')
              logging.info("Successfully connected to Cosmos DB using AAD default credential")
          except Exception as e:
              logging.error(f"Error connecting to Cosmos DB: {e}")
              return
          
          database_name = "ContosoDBDocIntellig"
          container_name = "Invoices"
      
          
          try: # Check if the database exists
              # If the database does not exist, create it
              database = client.create_database_if_not_exists(database_name)
              logging.info(f"Database '{database_name}' does not exist. Creating it.")
          except exceptions.CosmosResourceExistsError: # If error get name, keep going 
              database = client.get_database_client(database_name)
              logging.info(f"Database '{database_name}' already exists.")
      
          database.read()
          logging.info(f"Reading into '{database_name}' DB")
      
          try: # Check if the container exists
              # If the container does not exist, create it
              container = database.create_container(
                  id=container_name,
                  partition_key=PartitionKey(path="/transactionId"),
                  offer_throughput=400
              )
              logging.info(f"Container '{container_name}' does not exist. Creating it.")
          except exceptions.CosmosResourceExistsError:
              container = database.get_container_client(container_name)
              logging.info(f"Container '{container_name}' already exists.")
          except exceptions.CosmosHttpResponseError:
              raise
      
          container.read()
          logging.info(f"Reading into '{container}' container")
      
          try:
              response = container.upsert_item(invoice_data)
              logging.info(f"Saved processed invoice data to Cosmos DB: {response}")
          except Exception as e:
              logging.error(f"Error inserting item into Cosmos DB: {e}")
      
      ## MAIN 
      @app.blob_trigger(arg_name="myblob", path="pdfinvoices/{name}",
                        connection="invoicecontosostorage_STORAGE")
      def BlobTriggerContosoPDFInvoicesDocIntelligence(myblob: func.InputStream):
          logging.info(f"Python blob trigger function processed blob\n"
                       f"Name: {myblob.name}\n"
                       f"Blob Size: {myblob.length} bytes")
      
          try:
              form_recognizer_client = initialize_form_recognizer_client()
              pdf_bytes = read_pdf_content(myblob)
              logging.info("Successfully read PDF content from blob.")
          except Exception as e:
              logging.error(f"Error reading PDF: {e}")
              return
      
          try:
              result = analyze_pdf(form_recognizer_client, pdf_bytes)
              logging.info("Successfully analyzed PDF using Document Intelligence.")
          except Exception as e:
              logging.error(f"Error analyzing PDF: {e}")
              return
      
          try:
              invoice_data = extract_invoice_data(result)
              logging.info(f"Extracted invoice data: {invoice_data}")
          except Exception as e:
              logging.error(f"Error extracting invoice data: {e}")
              return
      
          try:
              save_invoice_data_to_cosmos(invoice_data)
              logging.info("Successfully saved invoice data to Cosmos DB.")
          except Exception as e:
              logging.error(f"Error saving invoice data to Cosmos DB: {e}")
     ```

      </details>

   - Now, let's update the `requirements.txt`:

    | Template `requirements.txt` | Updated `requirements.txt` |
    | --- | --- |
    | <img width="550" alt="image" src="https://github.com/user-attachments/assets/239516e0-a4b7-4e38-8c2b-9be12ebb00de"> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/91bd6bd8-ec21-4e1a-ae86-df577d37bcbb">| 

     ```text
      azure-functions
      azure-ai-formrecognizer
      azure-core
      azure-cosmos==4.3.0
      azure-identity==1.7.0
     ```
   - Since this function has already been tested, you can deploy your code to the function app in your subscription. If you want to test, you can use run your function locally for testing.
      - Click on the `Azure` icon.
      - Under `workspace`, click on the `Function App` icon.
      - Click on `Deploy to Azure`.

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/12405c04-fa43-4f09-817d-f6879fbff035">

      - Select your `subscription`, your `function app`, and accept the prompt to overwrite:

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/1882e777-6ba0-4e18-9d7b-5937204c7217">

      - After completing, you see the status in your terminal:

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa090cfc-f5b3-4ef2-9c2d-6be4f00b83b8">

           <img width="550" alt="image" src="https://github.com/user-attachments/assets/369ecfc7-cc31-403c-a625-bb1f6caa271c">

> [!IMPORTANT]
If you need further assistance with the code, please click [here to view all the function code](./src/).

> [!NOTE]
> Please ensure that all specified roles are assigned to the Function App. The provided example used `System assigned` for the Function App to facilitate the role assignment.

## Step 6: Test the solution

> [!IMPORTANT]
> Please ensure that the user/system admin responsible for uploading the PDFs to the blob container has the necessary permissions. The error below illustrates what might occur if these roles are missing. <br/> 
> <img width="550" alt="image" src="https://github.com/user-attachments/assets/d827775a-d419-467e-9b2d-35cb05bc0f8a"> <br/>
> In that case, go to `Access Control (IAM)`, click on `+ Add`, and `Add role assignment`: <br/>
> <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa4deff1-b6e1-49ec-9395-831ce2f982f5"> <br/>
> Search for `Storage Blob Data Contributor`, click `Next`. <br/>
> <img width="550" alt="image" src="https://github.com/user-attachments/assets/1fd40ef8-53f7-42df-a263-5bc3c80e61ba"> <br/>
> Then, click on `select members` and search for your user/systen admin. Finally click on `Review + assign`.

> Upload sample PDF invoices to the Blob container and verify that data is correctly ingested and stored in Cosmos DB.

- Click on `Upload`, then select `Browse for files` and choose your PDF invoices to be stored in the blob container, which will trigger the function app to parse them.

   <img width="950" alt="image" src="https://github.com/user-attachments/assets/a8456461-400b-4c68-b3d3-ac0b1630374d">

- Check the logs, and traces from your function with `Application Insights`:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/d499580a-76cb-4b4f-bb36-fd60c563a91c">

- Under `Investigate`, click on `Performance`. Filter by time range, and `drill into the samples`. Sort the results by date (if you have many, like in my case) and click on the last one.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/e266131c-e46f-4848-96ed-db2c04c5c18f">

- Click on `View all`:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/19356900-00c8-43ca-b888-fe493b25f258">

- Check all the logs, and traces generated. Also review the information parsed:

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/8f4631cc-162e-4c3b-913d-d146ea4e36b3">

- Validate that the information was uploaded to the Cosmos DB. Under `Data Explorer`, check your `Database`.

   <img width="550" alt="image" src="https://github.com/user-attachments/assets/27309a6d-c654-4c76-bbc1-990a9338973c">

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
