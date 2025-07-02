# Truncation Handling for Complex Documents - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-03

------------------------------------------

> Truncation often results from exceeding token limits or poor chunking strategies. Complex documents (those with conditional logic, sparse entities, or nested structures) can tokenize inefficiently.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Chunk large documents for vector search solutions in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents)
- [What is Azure OpenAI in Azure AI Foundry Models?](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/overview)
- [Troubleshooting and best practices for Azure OpenAI On Your Data](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/on-your-data-best-practices)
 
</details>


<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Overview](#overview)
- [How to resolve truncation issues](#how-to-resolve-truncation-issues)

</details>


## Overview 

> Why Truncation Happens (Even in Shorter, Complex Documents)? <br/>
> `Truncation happens when the total token count for your prompt and its output goes over the model’s limit. But here’s the catch: it’s not just about how long your prompt is, how complex it is can also bump up the token usage.`

| Cause                        | Description                                                                                   | Why It Matters                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Structural Complexity        | Conditional logic, nested clauses, or sparse named entities lead to inefficient tokenization | Increases token count unexpectedly, risking mid-sentence truncation             |
| Tokenizer Behavior           | Azure OpenAI uses subword tokenization (e.g., `tiktoken`)                                     | Complex or rare words may consume more tokens than expected                     |
| Verbose or Tangential Output| High temperature settings cause longer, less focused completions                             | May exceed token limits and truncate output mid-thought                         |

<details>
<summary><b> Structural Complexity </b> (Click to expand)</summary>
  
> Documents with **conditional logic**, **nested clauses**, or **sparse named entities** are structurally complex. These patterns confuse tokenizers because they lack clear semantic anchors (like names or dates) and often involve long, interdependent clauses.

> E.g: `If the system fails to initialize, and the fallback protocol is not triggered unless the override is active, then the watchdog timer must be reset manually.`
> This sentence, while not long, contains multiple conditions and dependencies. Tokenizers break it into many subword units, inflating the token count.

> Why It Matter?

- You may hit token limits even with seemingly short documents.
- Truncation may occur mid-sentence or mid-logic, leading to incomplete or incoherent outputs.

> How to Address?

- Use **semantic chunking** to isolate logical units (e.g., one condition per chunk).
- Preprocess documents to simplify or flatten nested logic where possible.

</details>

<details>
<summary><b> Tokenizer Behavior </b> (Click to expand)</summary>

> Azure OpenAI uses the same tokenizer as OpenAI, typically `tiktoken`. This tokenizer breaks text into **subword tokens**, not full words. For example:
> - “Initialization” → `["Initial", "ization"]`  
> - “FallbackProtocol” → `["Fallback", "Protocol"]`

> Complex syntax, rare words, or compound identifiers (like in code or legal text) often result in more tokens per word than expected.

> **Why It Matters**

- Token count can balloon unexpectedly, even in short or medium-length documents.  
- This can lead to premature truncation or rejection of prompts that exceed model limits.

> **How to Address**

- Use the `tiktoken` library to **pre-calculate token usage** before sending prompts.  
- Normalize or simplify text during preprocessing (e.g., split compound words).  
- Avoid overly technical phrasing unless necessary.

</details>

<details>
<summary><b> Verbose or Tangential Output </b> (Click to expand)</summary>

> The `temperature` parameter controls randomness in model output:
> - **High temperature (0.8–1.0)** → creative, verbose, tangential  
> - **Low temperature (0.2–0.4)** → focused, deterministic, concise

> High temperature can cause the model to “ramble”, using more tokens than necessary and increasing the risk of hitting token limits.

> **Why It Matters**

- Verbose completions may exceed token budgets, especially in stateless or high-throughput scenarios.  
- Truncation may occur mid-sentence or mid-thought, degrading output quality.

> **How to Address**

- For structured tasks (e.g., summarization, extraction), set:
  ```json
  {
    "temperature": 0.2,
    "top_p": 0.9
  }
  ```
- Use `max_tokens` to cap output length.  
- Define `stop` sequences to cut off output at logical boundaries (e.g., `["\n\n", "###"]`).

</details>

## How to resolve truncation issues 

| **Solution Area**         | **Action**                                                                 | **Why It Helps**                                                                 |
|--------------------------|--------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| Token Budgeting          | Use Azure Functions with `tiktoken` to pre-calculate token usage before inference          | Prevents exceeding token limits and enables chunk-aware document processing     |
| Semantic Chunking        | Use Azure AI Search’s Document Layout or Text Split skillset for structure-aware chunking  | Preserves logical boundaries and improves embedding and retrieval quality       |
| Temperature Control      | Configure temperature and `top_p` in Azure OpenAI deployment settings                      | Reduces verbosity and keeps completions within token budget                     |
| Output Constraints       | Use `max_tokens`, `stop` sequences, and `top_p` in Azure OpenAI API calls                  | Ensures clean, bounded outputs and avoids mid-sentence truncation               |
| Monitoring & Scaling     | Use Azure Monitor, Log Analytics, and PTUs for throughput and cost control                 | Enables observability and resilience at enterprise scale                        |

<details>
<summary><b> Token Budgeting in Azure </b> (Click to expand)</summary>

> Azure OpenAI models like GPT-4-128k enforce strict token limits. Complex documents with nested logic or rare terms can tokenize inefficiently, leading to unexpected truncation. Use an `Azure Function or Logic App` with the `tiktoken` library to analyze and split documents into token-aware chunks before sending them to Azure OpenAI.

**How to Apply in Azure:**

- Deploy a lightweight Azure Function that:
  - Accepts document input
  - Uses `tiktoken` to count tokens
  - Splits content into ≤3000-token chunks
  - Returns chunks to Power Automate or Azure OpenAI for inference 

**Monitoring:**
- Use Azure Monitor and Log Analytics to track:
  - `tokens_used`
  - `flowRunId`
  - `request_uri`
- Visualize trends in Power BI to detect spikes or anomalies

</details>

<details>
<summary><b> Semantic Chunking with Azure AI Search </b> (Click to expand)</summary>

> Azure `AI Search` supports semantic chunking via built-in skills like `Document Layout and Text Split`. These tools preserve logical structure and improve retrieval quality for RAG pipelines. `Chunking is not just about staying under token limits—it also improves embedding quality and relevance scoring.` Click here to read more about [Chunk large documents for vector search solutions in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents) 

**How to Apply in Azure:**
- Use the **Document Layout skill** to chunk by:
  - Paragraphs
  - Headings (e.g., Markdown or HTML)
  - Tables or sections
- Use the **Text Split skill** to:
  - Split by sentence or character count
  - Add 10–15% overlap between chunks

**Example Configuration:**

```json
{
  "skills": [
    {
      "@odata.type": "#Microsoft.Skills.Text.SplitSkill",
      "textSplitMode": "pages",
      "maximumPageLength": 800,
      "overlappingLength": 100
    }
  ]
}
```

</details>

<details>
<summary><b> Temperature & Output Control in Azure OpenAI </b> (Click to expand)</summary>

> High temperature values (e.g., 0.8–1.0) increase creativity but also verbosity, which can lead to token overflow. Lower values (e.g., 0.2–0.4) yield more concise, deterministic outputs. Combine temperature control with `top_p`, `stop` sequences, and `max_tokens` in your Azure OpenAI deployment or API call. Click here to read more about [What is Azure OpenAI in Azure AI Foundry Models?](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/overview)

**How to Apply in Azure:**
- In Azure OpenAI Studio or API:
  ```json
  {
    "temperature": 0.3,
    "top_p": 0.9,
    "max_tokens": 1500,
    "stop": ["\n\n", "###", "END"]
  }
  ```

- For stateless, high-throughput scenarios:
  - Use Provisioned Throughput Units (PTUs) for predictable performance
  - Monitor latency and token usage with Azure Monitor.

</details>



<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
