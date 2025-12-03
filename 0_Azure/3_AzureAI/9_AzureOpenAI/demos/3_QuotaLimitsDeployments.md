# Azure Open AI: Deployments Quota, Limits, Features 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

 ## Wiki 

 - [Azure OpenAI Service quotas and limits](https://learn.microsoft.com/en-us/azure/ai-services/openai/quotas-limits)
 - [Azure OpenAI Service pricing table](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/)
 - [What is provisioned throughput?](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/provisioned-throughput)
 - [How to assign quota](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/quota?tabs=rest#assign-quota)
 - [Provisioned throughput units onboarding](https://learn.microsoft.com/en-us/azure/ai-services/openai/how-to/provisioned-throughput-onboarding)
 - [Data, privacy, and security for Azure OpenAI Service](https://learn.microsoft.com/en-us/legal/cognitive-services/openai/data-privacy?context=%2Fazure%2Fai-services%2Fopenai%2Fcontext%2Fcontext&tabs=azure-portal)

 
## Quota limits by deployment method

| **Deployment Method**       | **Quota Limits**                                                                 |
|-----------------------------|----------------------------------------------------------------------------------|
| **Serverless API**          | - Maximum prompt tokens per request: Varies per model.<br> - Max concurrent requests: 2 for DALL-E 2.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |
| **Models as a Service (MaaS)** | - Maximum prompt tokens per request: Varies per model.<br> - Max fine-tuned model deployments: 5.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |
| **Models as a Platform (MaaP)** | - Maximum prompt tokens per request: Varies per model.<br> - Max fine-tuned model deployments: 5.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |
| **Flows and Web Applications** | - Maximum prompt tokens per request: Varies per model.<br> - Max concurrent requests: 2 for DALL-E 2.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |
| **Managed Compute**         | - Maximum prompt tokens per request: Varies per model.<br> - Max fine-tuned model deployments: 5.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |
| **Provisioned-Managed**     | - Maximum number of PTUs per deployment: 100,000.<br> - Maximum prompt tokens per request: Varies per model.<br> - Max training jobs queued: 20.<br> - Max size of all files per upload: 16 MB.<br> - Max number of inputs in array with /embeddings: 2048. |

> Additional Quota Information

These limits are based on the default quotas and restrictions set by Azure OpenAI Service to ensure efficient and fair usage of resources.


| **Quota**                                      | **Limit**                                                                 | **Context**                                                                 | **What to Do if You Need More**                                            |
|------------------------------------------------|--------------------------------------------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **OpenAI resources per region per Azure subscription** | 30                                                                       | Limits the number of resources you can deploy in a single region to ensure regional availability. | 1. Go to the Azure portal.<br>2. Navigate to your subscription.<br>3. Select `Usage + quotas`.<br>4. Click `Request increase`.<br>5. Fill out the form with your requirements. |
| **Max training jobs queued**                   | 20                                                                       | Controls the number of training jobs that can be queued to manage compute resources effectively. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your training needs. |
| **Max size of all files per upload (Azure OpenAI on your data)** | 16 MB                                                                    | Ensures that uploads are manageable and do not overwhelm the system.        | 1. Optimize file sizes if possible.<br>2. If larger uploads are necessary, go to the Azure portal.<br>3. Navigate to your OpenAI resource.<br>4. Select `Quotas`.<br>5. Click `Request increase`. |
| **Max number of inputs in array with /embeddings** | 2048                                                                     | Limits the number of inputs to ensure efficient processing of embedding tasks. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your embedding needs. |
| **Max number of /chat/completions messages**   | 2048                                                                     | Ensures that chat completions are processed efficiently without overloading the system. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your chat completion needs. |
| **Max number of /chat/completions functions**  | 128                                                                      | Limits the number of functions to maintain performance and manage resources. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your function needs. |
| **Max number of /chat completions tools**      | 128                                                                      | Ensures that the number of tools used in chat completions is manageable.    | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your tool needs. |
| **Max files per Assistant/thread**             | 10,000 (API/AI Studio)<br>20 (Azure OpenAI Studio)                       | Limits the number of files to ensure efficient management and processing.   | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your file needs. |
| **Max file size for Assistants & fine-tuning** | 512 MB                                                                   | Ensures that individual file sizes are manageable for processing.           | 1. Optimize file sizes if possible.<br>2. If larger files are necessary, go to the Azure portal.<br>3. Navigate to your OpenAI resource.<br>4. Select `Quotas`.<br>5. Click `Request increase`. |
| **Max size for all uploaded files for Assistants** | 100 GB                                                                  | Limits the total size of uploaded files to manage storage and processing resources. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your storage needs. |
| **Assistants token limit**                     | 2,000,000 tokens                                                         | Ensures that the assistant can handle a substantial amount of data while maintaining performance. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token needs. |
| **GPT-4o max images per request**              | 10                                                                       | Limits the number of images to ensure efficient processing and resource management. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your image needs. |
| **GPT-4 vision-preview & GPT-4 turbo-2024-04-09 default max tokens** | 16,000                                                                  | Ensures that the model can handle large requests while maintaining performance. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token needs. |
| **GPT-4o max tokens defaults**                 | 4096                                                                     | Sets a default limit for tokens to manage processing resources effectively. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token needs. |
| **Max number of custom headers in API requests** | 10                                                                      | Limits the number of custom headers to ensure efficient processing of API requests. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your header needs. |

> Model-Specific Quota Limits

| **Model Type**              | **Description**                                                                 | **Limitations**                                                                 | **Context**                                                                 | **What to Do if You Need More**                                            |
|-----------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **GPT-4o & GPT-4 Turbo**    | Latest models with multimodal capabilities, handling both text and images.       | - Max tokens per request: 16,000.<br> - Max images per request: 10.             | Designed to handle complex tasks with large token and image limits.         | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token or image needs. |
| **GPT-4**                   | Improved models over GPT-3.5 for natural language and code generation.           | - Max tokens per request: 16,000.                                               | Enhanced capabilities for handling large text inputs.                       | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token needs. |
| **GPT-3.5**                 | Enhanced models over GPT-3 for natural language and code generation.             | - Max tokens per request: 4096.                                                 | Suitable for standard natural language processing tasks.                    | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your token needs. |
| **Embeddings**              | Converts text into numerical vectors for text similarity tasks.                  | - Max inputs in array: 2048.                                                    | Optimized for text similarity and search tasks with a high input limit.     | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your input needs. |
| **DALL-E**                  | Generates original images from natural language descriptions.                   | - Max concurrent requests: 2.                                                   | Resource-intensive image generation managed by limiting concurrent requests. | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your concurrent request needs. |
| **Whisper**                 | Transcribes and translates speech to text.                                       | - Max requests per minute: 3.                                                   | Manages the processing load of speech-to-text conversion.                   | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your request needs. |
| **Text to Speech (Preview)**| Synthesizes text to speech.                                                      | - Currently in preview, specific limitations may apply.                         | In preview, so limitations may vary as the service is refined.              | 1. Go to the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your text-to-speech needs. |
| **o1-preview & o1-mini**    | Designed for reasoning and problem-solving tasks with increased focus.          | - Limited access, available in East US2 region.<br> - Registration required.    | Specialized models with limited access to ensure focused usage and testing. | 1. Register for access through the Azure portal.<br>2. Navigate to your OpenAI resource.<br>3. Select `Quotas`.<br>4. Click `Request increase`.<br>5. Provide details about your needs. |

## PTUs and TPM relationship

> Provisioned Throughput Units (PTUs) <br/>
> Tokens Per Minute (TPM)

| **PTUs** | **Calls per Minute** | **Tokens in Prompt** | **Tokens in Response** | **Tokens per Minute (TPM)** |
|----------|----------------------|----------------------|------------------------|-----------------------------|
| 1        | 10                   | 50                   | 100                    | 1,500                       |
| 2        | 20                   | 50                   | 100                    | 3,000                       |
| 5        | 50                   | 50                   | 100                    | 7,500                       |
| 10       | 100                  | 50                   | 100                    | 15,000                      |
| 20       | 200                  | 50                   | 100                    | 30,000                      |
| 50       | 500                  | 50                   | 100                    | 75,000                      |

> Explanation:

- **PTUs**: Provisioned Throughput Units represent the capacity of tokens that can be processed per minute.
- **Calls per Minute**: The number of API calls that can be made per minute.
- **Tokens in Prompt**: The number of tokens in the input prompt for each call.
- **Tokens in Response**: The number of tokens in the model's response for each call.
- **Tokens per Minute (TPM)**: The total number of tokens processed per minute, calculated as:

$$
\text{TPM} = \text{Calls per Minute} \times (\text{Tokens in Prompt} + \text{Tokens in Response})
$$

> Example Calculation:
For 50 PTUs:

1. **Calls per Minute**: Calculate the number of calls per minute:

$$
\text{Calls per Minute} = \text{PTUs} \times \text{Calls per PTU per Minute}
$$

$$
\text{Calls per Minute} = 50 \times 10 = 500
$$

2. **Tokens per Minute**: Calculate the total tokens per minute:

$$
\text{TPM} = \text{Calls per Minute} \times (\text{Tokens in Prompt} + \text{Tokens in Response})
$$

$$
\text{TPM} = 500 \times (50 + 100) = 500 \times 150 = 75,000
$$

This means with 50 PTUs, you can process 75,000 tokens per minute.

## Provisioned Capacity Calculator

> Improve accuracy of your estimate by adding multiple workloads to your PTU calculation. Each workload will be calculated and displayed as well as the aggregate total if both are running at the same time to your deployment.

<img width="705" alt="image" src="https://github.com/user-attachments/assets/e59c7e24-6d9b-4ea3-855c-d4f284b53e59">

## How to increase your quota in Azure OpenAI:

1. **Sign in to the Azure Portal**:
   - Open your web browser and go to [portal.azure.com](https://portal.azure.com/)
   - Enter your Azure account credentials to log in.
2. **Navigate to Quotas**:
   - In the search bar at the top of the Azure Portal, type `Quotas`.
   - Select `My quotas` from the search results.
3. **Select the Resource**:
   - In the Quotas page, you will see a list of resources.
   - Find and click on the specific resource for which you want to increase the quota (e.g., Azure OpenAI).
4. **Request Quota Increase**:
   - Once you are on the resource page, look for an option that says `Request quota increase` or similar.
   - Click on this option to proceed.
5. **Enter New Limit**:
   - A form will appear where you can specify the new quota limit you need.
   - Enter the desired limit and provide any necessary details or justification for the increase.
6. **Submit the Request**: After filling out the form, click on the `Submit` button to send your request to Microsoft.
7. **Wait for Approval**:
   - Microsoft will review your request. This process may take some time.
   - You will receive a notification once your request has been approved or if additional information is needed.
8. **Check Status**: You can check the status of your quota increase request in the Azure Portal under the `Notifications` or `Support requests` section.

## Key considerations to ensure optimal performance, security, and cost-efficiency

| Key Consideration     | Description                                                                |
|-----------------------------|---------------------------------------------------------------------------------|
| **Model Selection**         | - Choose a model that fits your use case. <br/> - Consider performance metrics such as accuracy, latency, and throughput. |
| **Scalability**             | - Configure auto-scaling to handle varying loads. <br/> - Allocate sufficient compute resources to meet expected demand. |
| **Security**                | - Implement data encryption both in transit and at rest to protect sensitive information. <br/> - Use role-based access control (RBAC) to restrict access to the deployed models. |
| **Cost Management**         | - Select the appropriate billing model (e.g., pay-as-you-go, per token/request) based on your usage patterns. <br/> - Regularly monitor usage and costs to avoid unexpected expenses. |
| **Integration**             | - Ensure the deployed model's API endpoints are easily accessible and well-documented for integration with other applications. <br/> - Consider how the model will fit into existing workflows and systems. |
| **Compliance**              | - Ensure your deployment complies with relevant regulations and industry standards. Maintain logs and audit trails for all interactions with the deployed models. |
| **Maintenance and Updates** | - Plan for regular updates and retraining of models to maintain accuracy and relevance. <br/> - Continuously monitor model performance and make adjustments as needed. |
| **User Experience**         | - Optimize for low latency to ensure a smooth user experience. <br/> - Implement mechanisms for users to provide feedback on model performance. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->