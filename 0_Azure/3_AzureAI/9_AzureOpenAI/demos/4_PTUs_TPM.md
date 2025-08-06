# PTUs and TPM relationship

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

`Provisioned Throughput Units (PTUs)` <br/>
`Tokens Per Minute (TPM)`

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [How much throughput per PTU you get for each model](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding)
- [Understanding costs associated with provisioned throughput units (PTU)](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding#azure-reservations-for-azure-ai-foundry-provisioned-throughput)
- [Deployment types for Azure AI Foundry Models](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/deployment-types#global-provisioned)
- [Region availability for provisioned throughput capability](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/provisioned-throughput?tabs=global-ptum#region-availability-for-provisioned-throughput-capability)
- [Model summary table and region availability](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/models?tabs=global-ptum%2Cstandard-chat-completions#model-summary-table-and-region-availability)
- [Fine-tuning models](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/models?tabs=global-ptum%2Cstandard-chat-completions#fine-tuning-models) - input/output Max
- [Azure OpenAI in Azure AI Foundry Models quotas and limits](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/quotas-limits?context=%2Fazure%2Fai-foundry%2Fcontext%2Fcontext&tabs=REST)

</details>

<div align="center">
  <img width="700" alt="image" src="https://github.com/user-attachments/assets/0741d4b2-d70e-4b5e-a6cf-9c399483e598" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

From [Microsoft official documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding#model-independent-quota)

> Explanation:

- **PTUs**: Provisioned Throughput Units represent the capacity of tokens that can be processed per minute.
- **Calls per Minute**: The number of API calls that can be made per minute.
- **Tokens in Prompt**: The number of tokens in the input prompt for each call.
- **Tokens in Response**: The number of tokens in the model's response for each call.
- **Tokens per Minute (TPM)**: The total number of tokens processed per minute, calculated as:

1. **Tokens per Minute**: Calculate the total tokens per minute:

$$
\text{TPM} = \text{Calls per Minute} \times (\text{Tokens in Prompt} + \text{Tokens in Response})
$$

2. **Provisioned Throughput Units**: 

$$
\text{PTUs} = \frac{\text{TPM}}{\text{Tokens per PTU per Minute}}
$$

Where:
- **TPM** = Total tokens you want to process per minute
- **Tokens per PTU per Minute** = Depends on the model (e.g., 3,000 tokens/min for GPT-4.1 or GPT-4.1 Mini)

> E.g
> If you want to process **150,000 tokens per minute** using GPT-4.1:

$$
\text{PTUs} = \frac{150{,}000}{3{,}000} = 50
$$

## Provisioned Capacity Calculator

> Improve accuracy of your estimate by adding multiple workloads to your PTU calculation. Each workload will be calculated and displayed as well as the aggregate total if both are running at the same time to your deployment.

<img width="750" alt="image" src="https://github.com/user-attachments/assets/d7599273-b4e3-478a-b2b0-b72f8647bb0e" />

<img width="750" alt="image" src="https://github.com/user-attachments/assets/540a1fd2-cae1-445c-8ca8-a0123cc63d7e" />

https://github.com/user-attachments/assets/27beba15-57d6-4a2b-943e-496829644dbe

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1559-limegreen" alt="Total views">
  <p>Refresh Date: 2025-08-04</p>
</div>
<!-- END BADGE -->
