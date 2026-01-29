# AI Foundry LLM Evaluations <br/> How it works - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Observability in generative AI](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/observability?view=foundry-classic)
- [What’s New in Azure AI Foundry Finetuning: July 2025](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/what%E2%80%99s-new-in-azure-ai-foundry-finetuning-july-2025/4438850)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Overview](#overview)
- [How it works?](#how-it-works)

</details>

## Overview 

> Evaluation features,  enhance how developers assess and monitor fine-tuned models. 

1. **RFT Observability ("Auto-Evals")**: Offers real-time visibility into Reinforcement Fine-Tuning (RFT) jobs.
    *   **How it works**: Automatically launches a linked evaluation job when an RFT job starts. This job tracks intermediate results (prompts, responses, and grader scores) at each checkpoint.
    *   **Benefits**:  [What’s New in Azure AI Foundry Finetuning: July 2025](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/what%E2%80%99s-new-in-azure-ai-foundry-finetuning-july-2025/4438850)
        *   Enables live monitoring and debugging.
        *   Reduces wasted compute and budget due to misconfigured graders or reward hacking.
        *   Accessible via the “Evaluation” section on the Fine-tuning page when using RFT.
2. **Quick Evaluations (Quick Evals)**: Rapidly assess model outputs from Stored Completions.
      *   One-click evaluation without setting up a full evaluation job.
      *   Compare outputs across multiple models instantly.
      *   Ideal for fast iteration and spotting issues quickly. 
3. **Python Grader**: Custom evaluation logic using Python code.
      *   Users write Python functions to score model outputs based on structure, content, or tool usage.
      *   Returns a numeric score (typically 0–1).
      *   Can be combined with other graders for holistic evaluation.


> [!NOTE]
> You can create evaluation runs using:
> - **Built-in metrics**: Includes AI-assisted quality, NLP-based metrics (e.g., ROUGE, BLEU), and safety checks (e.g., self-harm, hate speech).
> - **Custom flows**: Upload datasets (CSV or JSONL), configure evaluation targets (fine-tuned model or dataset), and map data columns to metric inputs. Read more about it here: [Evaluate generative AI models and applications by using Microsoft Foundry](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/evaluate-generative-ai-app?view=foundry-classic)

> Evaluation Targets:

| Target | Description |
|--------|-------------|
| Fine-tuned model | Evaluates outputs generated during testing |
| Dataset | Evaluates pre-generated outputs stored in a dataset |

> Metric Categories:

| Category | Description | Key Details |
|----------|-------------|-------------|
| AI Quality (AI-assisted) | Evaluates output quality using AI models | Requires a model deployment |
| AI Quality (NLP) | Evaluates using mathematical metrics | Uses F1, ROUGE, BLEU scores |
| Risk & Safety | Detects harmful or inappropriate content | Content safety evaluation |

<img width="909" height="484" alt="image" src="https://github.com/user-attachments/assets/4c432506-dc16-4baa-966c-c8de17f57852" />

From [Observability in generative AI](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/observability?view=foundry-classic)

## How it works?

> Here’s a handy reference with all the details about the parameters for textual similarity: [Textual similarity evaluators](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/evaluation-evaluators/textual-similarit…). The approach is to experiment with different scenarios to identify the one with best results for the intended use case.

E.g: 

<img width="1581" height="828" alt="image" src="https://github.com/user-attachments/assets/2fa49964-fe97-40ed-ad2e-31ad4b7ba275" />

> System Prompt used: 

~~~text
You are a search-query string checker. For each user query, output exactly one label from this list: misspelling, brand name, heritage month, holiday, industry, customer service information, product use, event.
misspelling: common word or brand spelled incorrectly.
brand name: references to specific companies, product brands, or branded product phrases.
heritage month: terms tied to cultural observances (e.g., Pride Month).
holiday: religious or cultural holidays.
industry: sectors of business or commerce (e.g., plumbing, technology).
customer service information: phrases seeking store policies, coupons, hours, contacts, or similar help.
product use: phrases describing what an item is for (e.g., “guitar pick”).
event: occasions or gatherings such as weddings or concerts.
If none apply, choose the closest match. Do not provide explanations, return only the label.
~~~

> Please make any adjustments as you see fit:

<img width="1570" height="835" alt="image" src="https://github.com/user-attachments/assets/60bb1e75-370d-4bef-849e-ec42642b28b2" />

> Add the test criteria, for example:

<img width="1587" height="837" alt="image" src="https://github.com/user-attachments/assets/ba86935a-b4a8-459f-bd91-c7170b39ebb4" />

> Example of values used:
> - F1 = 0.8 
> - Precision = 0.85 
> - Recall = 0.85

<img width="1583" height="826" alt="image" src="https://github.com/user-attachments/assets/d649259c-23d9-4452-a719-5431724f757c" />

> We can add more test criteria:

<img width="1562" height="837" alt="image" src="https://github.com/user-attachments/assets/db34639f-702c-44e7-a15f-9d9aa793fa3e" />

> Overall:

<img width="1561" height="831" alt="image" src="https://github.com/user-attachments/assets/b4bae8d7-9010-4b3b-8326-f8b81746111b" />

> E.g Achieved a pass rate of 11/12 responses. Similar to ML, LLMs overall performance depends on both the model architecture and the configuration parameters selected: 

<img width="1030" height="827" alt="image" src="https://github.com/user-attachments/assets/6d4060f8-d330-41da-b66f-5474432febbb" />

<img width="1907" height="1002" alt="image" src="https://github.com/user-attachments/assets/97ad9a41-2321-4872-bf75-7575bcd6c251" />

> [!TIP]
> The key is to review the prompt you are using and experiment with few values to determine which settings best meet your requirements.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
