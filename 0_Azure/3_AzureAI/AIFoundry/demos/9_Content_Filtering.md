# Content Filtering \& Guardrails - Overview

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-12-26

------------------------------------------

> Microsoft Foundry enforces Responsible AI principles by applying content filters to all Large Language Models (LLMs) and image generation models.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Content filtering overview](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/content-filter?view=foundry-classic)
- [Configure content filters](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/content-filters?view=foundry-classic#understand-content-filter-configurability)
- [Azure OpenAI in Microsoft Foundry model deprecations and retirements](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/model-retirements?view=foundry-classic&tabs=text#current-models)
- [Emissions Impact Dashboard for Azure](https://marketplace.microsoft.com/en-us/product/power-bi/coi-sustainability.emissions_impact_dashboard)
- [GPT‑5.1 in Foundry: A Workhorse for Reasoning, Coding, and Chat](https://techcommunity.microsoft.com/blog/partnernews/gpt%E2%80%915-1-in-foundry-a-workhorse-for-reasoning-coding-and-chat/4469803)
- [Getting started with Azure OpenAI Assistants (Preview)](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/assistant?view=foundry-classic)
- [Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement)
- [Content filtering in Microsoft Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/content-filtering?view=foundry-classic)
- [Protected material detection](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/protected-material?view=foundry&tabs=text)
- [Default Guardrails and controls policies for Microsoft Foundry Models](https://learn.microsoft.com/en-us/azure/ai-foundry/foundry-models/concepts/default-safety-policies?view=foundry-classic)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [What Default guardrails means?](#what-default-guardrails-means)
- [Custom Filters](#custom-filters)

</details>

> [!NOTE]
> These filters are powered by Azure AI Content Safety and operate at two stages:
> - Input filtering: Checks user prompts before sending them to the model.
> - Output filtering: Checks model responses before returning them to the user.

> Default Filters:
> - Every deployment has a `default filter applied automatically.`
> - These filters `detect harmful content in four categories:`
>   - Violence
>   - Hate
>   - Sexual
>   - Self-harm
> - Each category has severity levels: safe, low, medium, high.
> - By default, medium and high severity content is blocked, while safe and low are allowed.


## What Default guardrails means?

> New UI:

https://github.com/user-attachments/assets/16015025-aea8-4ffe-8b66-85c945a98b75

| Default | Default v2 | 
| --- | --- | 
| <img width="1903" height="970" alt="image" src="https://github.com/user-attachments/assets/cde07660-349b-45ff-9051-f7208dcfb436" /> | <img width="1908" height="988" alt="image" src="https://github.com/user-attachments/assets/b7288176-aa8c-4bb3-99d6-2362890e17b0" /> |

> Old view:

https://github.com/user-attachments/assets/94e7e745-4123-4d63-909b-c126b6a2462f

| Default | Default v2 | 
| --- | --- | 
| <img width="648" height="452" alt="image" src="https://github.com/user-attachments/assets/291628e7-1c4d-4fc4-acb4-2ea79516856e" /> | <img width="751" height="700" alt="image" src="https://github.com/user-attachments/assets/5b6c66b6-a72c-4310-ac7d-8ff133172a5a" /> | 

## Custom Filters

> You can create custom content filters to override defaults:
> - Configure severity thresholds per category.
> - Enable or disable binary classifiers (e.g., jailbreak detection).
> - Custom filters can be applied at resource level or deployment level using:
>   - Foundry portal
>   - Azure CLI
>   - Bicep templates

> [!IMPORTANT]
> By default, data that flows through those agents is not shared publicly and is not used to train other models. Clikc here to read more about [Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
