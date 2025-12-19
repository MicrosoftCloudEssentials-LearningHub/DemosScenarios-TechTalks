# API Key Authentication in Azure AI Foundry Projects - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------


> [!IMPORTANT]
> If you’ve tried the update with the correct resource ID and API version, and the property still reads "disableLocalAuth": true, that means the setting is enforced by default in your subscription or tenant.
> `This behavior is a platform level security enhancement by Microsoft. Local authentication (API keys) is disabled by default in many tenants, and you cannot override it with CLI or REST API. Even subscription owners and tenant admins will continue to see "disableLocalAuth": true unless the organization explicitly opts out, which is rare.`
>  The only `supported path forward is to use Microsoft Entra ID authentication for your Foundry projects.` [Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/identity-professional/security-for-ai#microsoft-entra-agent-id)

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Security for AI agents with Microsoft Entra Agent ID](https://learn.microsoft.com/en-us/entra/agent-id/identity-professional/security-for-ai#microsoft-entra-agent-id)
- [Security for Foundry Tools](https://learn.microsoft.com/en-us/azure/ai-services/security-features)
- [Disable local authentication in Foundry Tools](https://learn.microsoft.com/en-us/azure/ai-services/disable-local-auth?utm_source=copilot.com)
- [Authentication and authorization in Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/authentication-authorization-foundry?view=foundry-classic&utm_source=copilot.com)
- [Microsoft Ignite - BOOK OF NEWS November 18 - 21, 2025](https://news.microsoft.com/ignite-2025-book-of-news/?msockid=1d5e87de30816a213ee0911931bf6b3b)
- [Foundry Control Plane: Where Developers Build, Operate, and Govern Every Agent](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-control-plane-where-developers-build-operate-and-govern-every-agent/4467885)
- [Control user access to agents](https://learn.microsoft.com/en-us/entra/agent-id/identity-professional/control-user-access-agents)
- [What is Microsoft Entra Agent ID?](https://learn.microsoft.com/en-us/entra/agent-id/identity-professional/microsoft-entra-agent-identities-for-ai-agents)

    <img width="916" height="558" alt="image" src="https://github.com/user-attachments/assets/de44264b-2b81-4a05-af1d-cc6ffab56a8b" />

 - [What's new at Microsoft Ignite 2025 - Microsoft Entra](https://learn.microsoft.com/en-us/entra/fundamentals/whats-new-ignite-2025?utm_source=copilot.com)

</details>

> In new Azure AI Foundry projects, API key authentication is disabled by default because the resource property `disableLocalAuth` is set to **true**. This prevents listing or generating keys and forces authentication through Microsoft Entra ID (Azure AD).  

<img width="1906" height="830" alt="image" src="https://github.com/user-attachments/assets/1cb23e16-930d-4984-ba61-15578438142d" />

<img width="1900" height="821" alt="image" src="https://github.com/user-attachments/assets/7f96a526-8d04-495a-85b0-bf3642516120" />

> [!NOTE]
> If re‑enable API keys is allowed, you must update the backing **Cognitive Services account** configuration at the Azure resource level (via Azure CLI, ARM template, or REST API) by setting `disableLocalAuth=false`. Once updated, API keys can be managed under **Keys and Endpoints** in the Azure portal.  

<img width="1906" height="828" alt="image" src="https://github.com/user-attachments/assets/3852b6c7-f843-414f-8c9d-98f5d466008d" />

1. Run this command in the CLI to see the properties first:
  
      ```cli
      az resource show \
        --ids "/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.CognitiveServices/accounts/<ACCOUNT_NAME>" \
        --query properties \
        --output json
      ```

  > E.g
  
  <img width="1899" height="820" alt="image" src="https://github.com/user-attachments/assets/779d0d85-c8a1-42b1-a599-a2f65468683d" />

2. If your tenant allows you to change it, you can re‑enable API key authentication by setting the property to `false`:
      
      ```cli
      az resource update  \
       --ids "/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.CognitiveServices/accounts/<ACCOUNT_NAME>"  \
       --set properties.disableLocalAuth=false   \
       --api-version 2023-05-01 \
       --debug
      ```

  > E.g 
  <img width="1914" height="325" alt="image" src="https://github.com/user-attachments/assets/e3628b8f-d5dc-45ee-813a-9f248cf533f8" />


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
