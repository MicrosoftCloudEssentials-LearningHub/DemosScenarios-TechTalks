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
- [Content filtering in Microsoft Foundry portal](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/content-filtering?view=foundry-classic)
- [Azure OpenAI in Microsoft Foundry model deprecations and retirements](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/concepts/model-retirements?view=foundry-classic&tabs=text#current-models)
- [Emissions Impact Dashboard for Azure](https://marketplace.microsoft.com/en-us/product/power-bi/coi-sustainability.emissions_impact_dashboard)
- [GPT‑5.1 in Foundry: A Workhorse for Reasoning, Coding, and Chat](https://techcommunity.microsoft.com/blog/partnernews/gpt%E2%80%915-1-in-foundry-a-workhorse-for-reasoning-coding-and-chat/4469803)
- [Getting started with Azure OpenAI Assistants (Preview)](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/assistant?view=foundry-classic)
  
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

## Custom Filters

> You can create custom content filters to override defaults:
> - Configure severity thresholds per category.
> - Enable or disable binary classifiers (e.g., jailbreak detection).
> - Custom filters can be applied at resource level or deployment level using:
>   - Foundry portal
>   - Azure CLI
>   - Bicep templates

> [!IMPORTANT]
> By default, user's, any organizational data that flows through those agents is not shared publicly and is not used to train other models.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
