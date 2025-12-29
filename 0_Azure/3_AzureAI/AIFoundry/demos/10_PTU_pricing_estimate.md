# PTUs Pricing Estimate - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-12-29

----------

`Provisioned Throughput Units (PTUs)` <br/>
`Tokens Per Minute (TPM)`

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Azure OpenAI pricing](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/?msockid=38ec3806873362243e122ce086486339) - table
- [Pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/) - more precise
- [Input TPM per PTU](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding?view=foundry-classic#latest-azure-openai-models) - table
- [Deployment types for Microsoft Foundry Models](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-models/concepts/deployment-types?view=foundry-classic#global-provisioned)
- [Understanding costs associated with provisioned throughput units (PTU)](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding?view=foundry-classic)

</details>

<img width="1125" height="511" alt="image" src="https://github.com/user-attachments/assets/d418bd70-073b-4d26-906b-3c135d51a8ac" />

From [Understanding costs associated with provisioned throughput units (PTU)](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/provisioned-throughput-onboarding?view=foundry-classic)

## How to estimate?

> [!IMPORTANT]
> The most straightforward approach is to use the [Azure Provisioned Capacity Calculator](#provisioned-capacity-calculator) and the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) to generate a more relevant estimate. If the specific model (LLM) is not yet available in the dropdown, we can leverage rough estimate.

For example: [Azure Provisioned Capacity Calculator](#provisioned-capacity-calculator)

| Model | PTUs | 
| ----- | ----- | 
| `gpt-4.1-nano` | <img width="1858" height="640" alt="image" src="https://github.com/user-attachments/assets/404b83be-228a-4058-9918-a1066e654d34" /> | 
| `gpt-4.1-mini` | <img width="1897" height="685" alt="image" src="https://github.com/user-attachments/assets/16443832-5f5c-4e68-9337-45607b765b71" /> | 
| `gpt-5-mini` | <img width="1886" height="621" alt="image" src="https://github.com/user-attachments/assets/a3a35179-89e7-497b-a982-6896922d428b" /> | 
| `gpt-4.1`| <img width="1881" height="645" alt="image" src="https://github.com/user-attachments/assets/07aba116-bd89-413d-a00f-beec21c4d06d" /> |
| `gpt-5` | <img width="1889" height="644" alt="image" src="https://github.com/user-attachments/assets/b0463b28-c87d-4fd1-a206-759dba6b2bde" /> |

For example: [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

> [!TIP]
> Reservations: `Reduce costs on select Azure services by forecasting your resource needs and paying for them in advance.`

| Model | Price estimate | 1 month reserved | 1 year reserved |
| ----- | ----- | ----- | ----- | 
| `gpt-4.1-nano` | <img width="1087" height="886" alt="image" src="https://github.com/user-attachments/assets/5e31d568-a13b-4e01-9e9f-fcdd2bbccc5f" /> | <img width="1090" height="878" alt="image" src="https://github.com/user-attachments/assets/b5cbf1b6-27ce-48e8-9922-ce1fadce7e39" /> | <img width="1068" height="866" alt="image" src="https://github.com/user-attachments/assets/274b25fb-9283-48f3-a11f-4f0f8e69379d" /> | 
| `gpt-4.1-mini` | <img width="1050" height="887" alt="image" src="https://github.com/user-attachments/assets/3e1b3258-56ee-4ebf-a79a-b0f41dc9a251" /> | <img width="1073" height="896" alt="image" src="https://github.com/user-attachments/assets/aca889b0-ca50-4162-a7af-6543a09e8ca7" /> | <img width="1063" height="902" alt="image" src="https://github.com/user-attachments/assets/ccadb3e8-0684-4958-ac63-7d427ec1fb9e" /> | 
| `gpt-4.1`| <img width="1062" height="887" alt="image" src="https://github.com/user-attachments/assets/0429879c-39cf-412e-856b-6431718fd3fa" /> | <img width="1072" height="892" alt="image" src="https://github.com/user-attachments/assets/ecd9e938-f300-4c78-af1f-80a1d1dd292b" /> | <img width="1068" height="908" alt="image" src="https://github.com/user-attachments/assets/6e41f763-9c59-4a62-b77c-63b4c52b5c51" /> | 

## Rough estimate?

> If the specific model (LLM) is not available yet in the dropdown [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/), we can leverage rough estimate.

`gpt-5-mini` \& `gpt-5` 

## Provisioned Capacity Calculator

> Improve accuracy of your estimate by adding multiple workloads to your PTU calculation. Each workload will be calculated and displayed as well as the aggregate total if both are running at the same time to your deployment.

https://github.com/user-attachments/assets/31b5e2db-79dd-432f-a250-46227d551fcc


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
