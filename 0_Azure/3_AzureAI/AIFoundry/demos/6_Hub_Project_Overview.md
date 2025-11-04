# Understanding project vs Hub in Azure AI platform - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

------------------------------------------


<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Upgrade from Azure OpenAI to Azure AI Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/upgrade-azure-openai?tabs=portal)
- [Cost Tracking with API calls - Overview](https://github.com/MicrosoftCloudEssentials-LearningHub/DemosScenarios-TechTalks/blob/main/0_Azure/3_AzureAI/9_AzureOpenAI/demos/7_TokenizationCostAnalysis.md#cost-tracking-with-api-calls)
- [Manage and increase quotas for resources with Azure AI Foundry (Foundry projects)](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/quota)
- [Manage and increase quotas for hub resources](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/hub-quota)

  <img width="1542" height="950" alt="image" src="https://github.com/user-attachments/assets/20f0e813-a69f-4f62-843c-e83873f82efb" />
 
</details>


<img width="1404" height="663" alt="image" src="https://github.com/user-attachments/assets/de201ffc-60c6-4ba7-a884-b8274fe3d3cd" />

From [Hub vs project](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/migrate-project?tabs=azure-ai-foundry)

E.g:

<img width="1718" height="588" alt="image" src="https://github.com/user-attachments/assets/7f27a307-be6b-4848-aa12-6a5bca5cb321" />

> Example of how it works:

<img width="1434" height="605" alt="image" src="https://github.com/user-attachments/assets/4244dc71-638a-4d76-bc43-0d1be1991a33" />

- When I create a project under the project as parent resource, I can only view the model and endpoints tied to that specific project (e.g red marked) 

     <img width="1115" height="506" alt="image" src="https://github.com/user-attachments/assets/7ce89e2a-498e-4395-875b-1f9a34490acc" />

 - Depending on who the parent is, you’ll see the deployments show up differently. For example, when the project has the hub or AI Foundry as the parent, it’s group by the AI service. (e.g yellow marked)

 
     <img width="1115" height="506" alt="image" src="https://github.com/user-attachments/assets/1689b1b9-a930-445a-8d8b-6c1eb445f73b" />

- Inherited permissions associated with the resources linked to the project:
 
    <img width="1223" height="556" alt="image" src="https://github.com/user-attachments/assets/40dd4a2b-5a92-46f4-8855-e32773333d0d" />

    <img width="1450" height="639" alt="image" src="https://github.com/user-attachments/assets/87595fc8-f4cb-4200-a012-96ec3148d24a" />

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
