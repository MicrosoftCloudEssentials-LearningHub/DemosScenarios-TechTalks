# Truncation Handling for Complex Documents - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

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

> Why It Matters?

- You may hit token limits even with seemingly short documents.
- Truncation may occur mid-sentence or mid-logic, leading to incomplete or incoherent outputs.
- Azure OpenAI’s tokenizer (`tiktoken`) breaks text into subword units, so structurally dense content can consume more tokens than expected.
- Complex documents often lack named entities (e.g., people, places, dates), which are helpful for grounding and compressing meaning efficiently.

> How to Address?

- Use **semantic chunking** to isolate logical units (e.g., one condition per chunk). In Azure, this can be implemented using:
  - **Azure AI Search’s Document Layout skill** to chunk by paragraphs, headings, or sections.
  - **Text Split skill** to define chunk size and overlap, preserving context across boundaries.
  - Example configuration:
    ```json
    {
      "@odata.type": "#Microsoft.Skills.Text.SplitSkill",
      "textSplitMode": "pages",
      "maximumPageLength": 800,
      "overlappingLength": 100
    }
    ```

- Preprocess documents to simplify or flatten nested logic where possible:
  - Use Azure Functions or Logic Apps to transform complex conditionals into simpler declarative statements or bullet points.
  - Example transformation:
    - Original:  
      `If A and B, unless C, then D.`
    - Flattened:  
      - Condition 1: A is true  
      - Condition 2: B is true  
      - Exception: C is false  
      - Action: Perform D

- Use **token-aware chunking** before sending content to Azure OpenAI:
  - Deploy a preprocessing step using `tiktoken` in an Azure Function to:
    - Count tokens per clause or paragraph
    - Split content into ≤3000-token chunks
    - Return token-safe chunks to Azure OpenAI for inference
  - This ensures that each chunk respects token limits and avoids mid-logic truncation.

- Monitor token usage and truncation patterns using **Azure Monitor** and **Log Analytics**:
  - Track metrics like `tokens_used`, `completion_tokens`, and `prompt_tokens`.
  - Set alerts for high token usage or frequent truncation errors.

</details>

<details>
<summary><b> Tokenizer Behavior </b> (Click to expand)</summary>

> Azure OpenAI uses the same tokenizer as OpenAI, typically `tiktoken`. This tokenizer breaks text into **subword tokens**, not full words. For example:  
> - “Initialization” → `["Initial", "ization"]`  
> - “FallbackProtocol” → `["Fallback", "Protocol"]`

> Complex syntax, rare words, or compound identifiers (like in code, legal, or scientific text) often result in more tokens per word than expected. This is especially common in enterprise documents with domain-specific terminology, acronyms, or camelCase identifiers.

> **Why It Matters**

- Token count can balloon unexpectedly, even in short or medium-length documents.
- This can lead to:
  - Premature truncation of outputs.
  - Rejection of prompts that exceed model limits (e.g., 128k for GPT-4-128k).
  - Increased latency and cost due to inefficient token usage.
- Token inflation is especially problematic in Azure OpenAI when using models in high-throughput or stateless scenarios, where every token counts toward performance and billing.

> **How to Address**

- Use the `tiktoken` library to **pre-calculate token usage** before sending prompts to Azure OpenAI:
  - Deploy this as part of a preprocessing pipeline in an **Azure Function** or **Logic App**.
  - Example:
    ```python
    import tiktoken
    enc = tiktoken.encoding_for_model("gpt-4")
    tokens = enc.encode("Your input text here")
    print(len(tokens))
    ```

- Normalize or simplify text during preprocessing:
  - Replace compound identifiers like `FallbackProtocol` with `fallback protocol`.
  - Convert camelCase or snake_case to plain language equivalents.
  - Remove unnecessary jargon or abbreviations unless essential.

- Avoid overly technical phrasing unless required:
  - Instead of:  
    `The system's failoverInitFlag must be set to true unless the watchdogOverride is active.`  
  - Use:  
    `The system must fail over unless the watchdog override is active.`

- Use **Azure AI Search** to preprocess and chunk documents before embedding:
  - The **Text Split skill** can help break down dense content into manageable, semantically meaningful units.
  - Combine this with token-aware chunking to ensure each chunk stays within safe token limits.

- Monitor token usage in production:
  - Use **Azure Monitor** and **Log Analytics** to track `prompt_tokens`, `completion_tokens`, and `total_tokens`.
  - Set alerts for unusually high token usage or truncation errors.

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
- In Azure OpenAI, token usage directly impacts:
  - **Latency**: More tokens = longer processing time.
  - **Cost**: You are billed per token used.
  - **Reliability**: Long outputs are more likely to hit model limits or timeout in high-load environments.

> **How to Address**

- For structured tasks (e.g., summarization, extraction), set:
  ```json
  {
    "temperature": 0.2,
    "top_p": 0.9
  }
  ```
  - This configuration ensures the model stays focused and avoids unnecessary elaboration.
  - `top_p` (nucleus sampling) helps limit the range of token choices, further reducing verbosity.

- Use `max_tokens` to cap output length:
  ```json
  {
    "max_tokens": 1500
  }
  ```
  - This prevents the model from generating excessively long responses.
  - In Azure OpenAI Studio, you can set this in the deployment playground or via API.

- Define `stop` sequences to cut off output at logical boundaries:
  ```json
  {
    "stop": ["\n\n", "###", "END"]
  }
  ```
  - This is especially useful when generating structured outputs like JSON, YAML, or bullet lists.
  - It ensures the model stops cleanly instead of trailing off or repeating.

- In Azure OpenAI deployments:
  - Use **deployment-level defaults** for temperature and `max_tokens` to enforce consistency across applications.
  - For example, in Azure OpenAI Studio, under your deployment settings, configure:
    - `temperature = 0.3`
    - `max_tokens = 1024`
    - `frequency_penalty = 0.2` (optional, to reduce repetition)

- Monitor and tune:
  - Use **Azure Monitor** and **Application Insights** to track:
    - Average token usage per request
    - Frequency of truncation errors
    - Latency spikes due to verbose completions
  - Adjust temperature and `max_tokens` dynamically based on usage patterns.

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

> Azure OpenAI models like GPT-4-128k enforce strict token limits. Complex documents with nested logic or rare terms can tokenize inefficiently, leading to unexpected truncation. Use an `Azure Function` or `Logic App` with the `tiktoken` library to analyze and split documents into token-aware chunks before sending them to Azure OpenAI.

> E.g: A 5-page technical document with nested conditions and domain-specific terms may tokenize into 40,000+ tokens, well beyond expectations, because of how `tiktoken` breaks down compound words and logic-heavy phrasing.

> **Why It Matters**

- Token limits are hard constraints in Azure OpenAI. If your prompt + completion exceeds the model’s token ceiling (e.g., 128k for GPT-4-128k), the request will fail or be truncated.
- Token inflation from complex syntax can cause:
  - Incomplete outputs
  - Higher latency
  - Increased cost per request
- Without token budgeting, you risk unpredictable behavior in production, especially in stateless or high-throughput applications.

> **How to Address**

- Use `tiktoken` in an Azure-native preprocessing pipeline to **count and manage tokens**:
  - Deploy an **Azure Function** that:
    - Accepts raw document input (from Blob Storage, SharePoint, etc.)
    - Uses `tiktoken` to calculate token count
    - Splits content into ≤3000-token chunks (or your preferred threshold)
    - Returns token-safe chunks to Azure OpenAI or Power Automate

  Example Python snippet:
  ```python
  import tiktoken
  enc = tiktoken.encoding_for_model("gpt-4")
  tokens = enc.encode(your_text)
  print(len(tokens))  # Use this to enforce chunking logic
  ```

- Integrate with **Power Automate**:
  - Trigger the Azure Function from a flow
  - Loop through returned chunks and call Azure OpenAI for each
  - Aggregate responses if needed (e.g., for summarization or document Q&A)

- Use **Azure AI Search** for chunking + embedding:
  - Apply the **Text Split skill** with `maximumPageLength` and `overlappingLength` to control chunk size and preserve context.
  - Combine with the **Document Layout skill** to chunk by paragraphs or sections.

  Example skill configuration:
  ```json
  {
    "@odata.type": "#Microsoft.Skills.Text.SplitSkill",
    "textSplitMode": "pages",
    "maximumPageLength": 800,
    "overlappingLength": 100
  }
  ```

> **Monitoring**

- Use **Azure Monitor** and **Log Analytics** to track:
  - `tokens_used` per request
  - `flowRunId` and `request_uri` for traceability
  - `completion_tokens` vs `prompt_tokens` to optimize prompt design

- Visualize token trends in **Power BI**:
  - Identify documents or use cases with high token consumption
  - Detect anomalies like sudden spikes or frequent truncation errors

- Set alerts for:
  - Token usage thresholds
  - Truncation-related errors
  - Latency spikes due to oversized prompts

</details>

<details>
<summary><b> Semantic Chunking with Azure AI Search </b> (Click to expand)</summary>

> Azure `AI Search` supports semantic chunking via built-in skills like `Document Layout` and `Text Split`. These tools preserve logical structure and improve retrieval quality for RAG pipelines. `Chunking is not just about staying under token limits, it also improves embedding quality and relevance scoring.`  
> Click here to read more about [Chunk large documents for vector search solutions in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents)

> E.g: A 10-page policy document with multiple sections and subheadings can be chunked by paragraph or heading using the Document Layout skill. This ensures each chunk contains a coherent idea, improving both retrieval accuracy and LLM comprehension.

> **Why It Matters**

- Fixed-size chunking (e.g., every 1,024 tokens) can split content mid-sentence or mid-thought, leading to:
  - Poor embedding quality
  - Irrelevant or incoherent retrieval results
  - Increased token usage due to repeated context
- Semantic chunking ensures each chunk is logically complete, which:
  - Improves the quality of vector embeddings
  - Increases the relevance of search results in RAG pipelines
  - Reduces the likelihood of truncation or hallucination in LLM responses

> **How to Apply in Azure**

- Use the **Document Layout skill** to chunk by:
  - Paragraphs
  - Headings (e.g., Markdown, HTML, or PDF structure)
  - Tables or sections
  - This skill extracts structural elements from documents and enables chunking based on layout rather than raw text length.

- Use the **Text Split skill** to:
  - Split by sentence, character count, or page length
  - Add 10–15% overlap between chunks to preserve context across boundaries
  - This is especially useful when layout metadata is unavailable or inconsistent

> **Example Configuration**

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

- Combine both skills in a skillset pipeline:
  - First, apply the Document Layout skill to extract structured content
  - Then, apply the Text Split skill to chunk the structured content into token-efficient, semantically meaningful segments

> **Additional Tips**

- Store both the chunk content and its source metadata (e.g., heading, section title) in your Azure AI Search index. This improves filtering and reranking.
- Use chunk-level embeddings for vector search and rerank results using Azure AI Search’s semantic scoring.
- Evaluate chunking effectiveness by measuring:
  - Retrieval precision (e.g., top-k relevance)
  - LLM response quality
  - Token efficiency per query

</details>


<details>
<summary><b> Temperature & Output Control in Azure OpenAI </b> (Click to expand)</summary>

> High temperature values (e.g., 0.8–1.0) increase creativity but also verbosity, which can lead to token overflow. Lower values (e.g., 0.2–0.4) yield more concise, deterministic outputs. Combine temperature control with `top_p`, `stop` sequences, and `max_tokens` in your Azure OpenAI deployment or API call. Click here to read more about [What is Azure OpenAI in Azure AI Foundry Models?](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/overview)

> E.g: A prompt like “Summarize the following policy document” with a high temperature (0.9) might result in a long, overly creative response that includes speculative or unnecessary elaboration. The same prompt with a temperature of 0.2 will yield a more focused and concise summary.

> **Why It Matters**

- Verbose completions may exceed token budgets, especially in stateless or high-throughput scenarios.
- Truncation may occur mid-sentence or mid-thought, degrading output quality and user trust.
- In Azure OpenAI, token usage directly affects:
  - **Latency**: More tokens = longer processing time.
  - **Cost**: You are billed per token used.
  - **Reliability**: Long outputs are more likely to hit model limits or timeout in high-load environments.
- Inconsistent output behavior can also affect downstream systems that rely on structured or predictable responses (e.g., JSON, YAML, or tabular formats).

> **How to Address**

- In Azure OpenAI Studio or API, configure your deployment or request with:
  ```json
  {
    "temperature": 0.3,
    "top_p": 0.9,
    "max_tokens": 1500,
    "stop": ["\n\n", "###", "END"]
  }
  ```
  - `temperature`: Controls randomness. Lower = more deterministic.
  - `top_p`: Limits token sampling to the top probability mass. Helps reduce tangents.
  - `max_tokens`: Caps output length to avoid overflow.
  - `stop`: Ensures clean termination of output at logical boundaries.

- For stateless, high-throughput scenarios:
  - Use **Provisioned Throughput Units (PTUs)** in Azure OpenAI to guarantee consistent performance under load.
  - PTUs allow you to reserve capacity and avoid throttling during peak usage.
  - Ideal for APIs that serve thousands of requests per minute without chat history.

- Monitor and tune:
  - Use **Azure Monitor** and **Application Insights** to track:
    - `prompt_tokens`, `completion_tokens`, and `total_tokens`
    - Latency and response time
    - Truncation errors or incomplete outputs
  - Adjust `temperature`, `max_tokens`, and `stop` sequences based on observed behavior.

- For structured tasks (e.g., summarization, classification, extraction):
  - Keep `temperature` between 0.2–0.4
  - Use `frequency_penalty` and `presence_penalty` to reduce repetition or encourage novelty when needed:
    ```json
    {
      "frequency_penalty": 0.2,
      "presence_penalty": 0.0
    }
    ```

</details>

<details>
<summary><b> Monitoring & Scaling </b> (Click to expand)</summary>

> Azure OpenAI workloads, especially those involving high-throughput or production-grade LLM applications—require robust monitoring and scaling strategies. Azure provides native tools like `Azure Monitor`, `Log Analytics`, and `Provisioned Throughput Units (PTUs)` to help you track performance, control costs, and ensure reliability at scale.

> E.g: A stateless summarization API that receives thousands of requests per minute may experience latency spikes or throttling if not backed by PTUs and monitored for token usage and response time. Without observability, it’s difficult to detect when truncation or cost overruns occur.

> **Why It Matters**

- Azure OpenAI usage is billed per token. Without monitoring, you may:
  - Exceed budget thresholds
  - Miss early signs of inefficient prompts or verbose completions
- High-traffic applications can experience:
  - Throttling or rate-limiting
  - Latency spikes
  - Inconsistent performance without PTUs
- Lack of observability can delay detection of:
  - Truncation errors
  - Prompt design flaws
  - Token inflation due to structural complexity

> **How to Address**

- Use **Azure Monitor** to track key metrics:
  - `tokens_used`, `prompt_tokens`, `completion_tokens`
  - `latency`, `success_rate`, `throttled_requests`
  - Set up alerts for anomalies (e.g., token spikes, high latency)

- Use **Log Analytics** to:
  - Query historical usage patterns
  - Correlate token usage with specific endpoints or flows
  - Analyze prompt efficiency and model behavior over time

- Visualize trends in **Power BI**:
  - Connect to Log Analytics workspace
  - Build dashboards for:
    - Token consumption by endpoint
    - Cost per request
    - Truncation frequency

- Use **Provisioned Throughput Units (PTUs)** for predictable performance:
  - PTUs reserve dedicated capacity for Azure OpenAI deployments
  - Ideal for:
    - Stateless APIs
    - Batch processing
    - Real-time inference at scale
  - PTUs help avoid throttling and ensure consistent latency

> PTUs are especially useful when using Azure OpenAI in conjunction with Azure AI Search or Power Automate, where downstream systems depend on consistent response times.

- Monitor PTU usage:
  - Use Azure Metrics Explorer to track:
    - PTU consumption
    - Cache hit ratio
    - Request volume
  - Adjust PTU allocation based on observed demand

</details>




<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
