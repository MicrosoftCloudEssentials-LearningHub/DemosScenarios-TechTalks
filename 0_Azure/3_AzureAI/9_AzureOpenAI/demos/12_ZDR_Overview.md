# Zero Data Retention on Azure Open AI - Overview 

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-12-03

------------------------------------------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Data, privacy, and security for Azure Direct Models in Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-portal#how-can-a-customer-verify-if-data-storage-for-abuse-monitoring-is-off)

</details>

> ZDR - Microsoft is committed to not retaining any customer requests or response data beyond what is strictly necessary for real-time processing. Once the data has fulfilled its intended purpose, it is promptly deleted, ensuring that prompts and completions are not stored for training, debugging, or analytics purposes.

<img width="943" height="1052" alt="flow-3" src="https://github.com/user-attachments/assets/efe3ce83-75f5-4567-8ab3-384bb61fff36" />

From [How does Foundry process data to provide Azure Direct Models?](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-portal#how-does-foundry-process-data-to-provide-azure-direct-models)

## How can a customer verify if data storage for abuse monitoring is off?

> Once approval is granted, data storage for abuse monitoring will be disabled. You can confirm this status using the Azure portal or Azure CLI. For further details, please consult the documentation here: [How can a customer verify if data storage for abuse monitoring is off?](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-portal#how-can-a-customer-verify-if-data-storage-for-abuse-monitoring-is-off)

> Using [Azure CLI](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-cli#prerequisites):

```azurecli
az cognitiveservices account show -n resource\_name -g resource \_group
```

> [!NOTE]
> The system will return a JSON response. If abuse monitoring logging is disabled, you will find a value labeled `ContentLogging`, which will be set to `FALSE`.


> Using [Azure Portal](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-portal#prerequisites):

For example: In my Azure OpenAI instance, I'm not able to find the `ContentLogging` attribute. `This attribute is only visible when set to false, indicating that abuse monitoring has been disabled.` In this case, for me is on.

<img width="1911" height="830" alt="image" src="https://github.com/user-attachments/assets/35f43b1b-35cb-49f0-bf57-048575cbd6d5" />

<img width="1883" height="827" alt="image" src="https://github.com/user-attachments/assets/4814d8e9-84fd-485a-8f8f-03126d09bf2a" />

> When it is set to `off`, you should be able to view the following:

```
{
    "name":"ContentLogging",
    "value":"false"
}
```

> [!TIP]
> In essence, `data storage for abuse monitoring is off` means the same thing as `Zero Data Retention (ZDR) with abuse monitoring disabled`, but the terminology depends on the platform:
> - On the OpenAI platform, ZDR guarantees that prompts and completions are not saved or used for training purposes. But, abuse monitoring may require temporary data storage to identify harmful activity. If you have ZDR approval and have opted out of abuse monitoring, then your data will not be stored for this purpose.
>     - [Enterprise privacy at OpenAI](https://openai.com/enterprise-privacy/)
>     - [Business data privacy, security, and compliance](https://openai.com/business-data/)
>  - From the Azure OpenAI standpoint, `Azure does not use the term ZDR, and by default, prompts and completions are not stored for training purposes.` Regarding `abuse monitoring`, it is `enabled by default and may require temporary data storage`. But, we can request to disable this storage, which also turns off abuse monitoring data storage.
>      - [Abuse Monitoring](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/abuse-monitoring?view=foundry-classic)
>      - [How can a customer verify if data storage for abuse monitoring is off?](https://learn.microsoft.com/en-us/azure/ai-foundry/responsible-ai/openai/data-privacy?view=foundry-classic&tabs=azure-portal#how-can-a-customer-verify-if-data-storage-for-abuse-monitoring-is-off)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
