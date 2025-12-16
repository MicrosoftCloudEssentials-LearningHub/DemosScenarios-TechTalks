# Scaling Beyond Azure AI Search Index Limits - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!TIP]
> Imagine a huge library filled with millions of books (your raw data in storage).
> - Without a catalog, a human would have to `walk through every hall and open every book to find what they need, it's slow and exhausting.`
> - The catalog card is the index: `it summarizes the book’s title, author, subject, and keywords.`
> - With that index, `you can jump straight to the right shelf and book in seconds.`
> - Azure AI Search works like that catalog system: `it builds indexes for your files, so queries don’t have to scan every document.`

<details>
<summary><b> List of References </b> (Click to expand)</summary>

- [Azure AI Search pricing](https://azure.microsoft.com/en-us/pricing/details/search/?msockid=38ec3806873362243e122ce086486339#pricing)
- [Service limits in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-limits-quotas-capacity)
- [Design patterns for multitenant SaaS applications and Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-modeling-multitenant-saas-applications)
- [Create a hybrid query in Azure AI Search](https://docs.azure.cn/en-us/search/hybrid-search-how-to-query?tabs=portal)
- [Hybrid search using vectors and full text in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/hybrid-search-overview)
- [AI enrichment in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/cognitive-search-concept-intro)

    <img width="1314" height="470" alt="image" src="https://github.com/user-attachments/assets/c5191f11-af7b-42ab-a641-ec18c9e5dea4" />

- [Azure AI Search: Outperforming vector search with hybrid retrieval and reranking](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/azure-ai-search-outperforming-vector-search-with-hybrid-retrieval-and-reranking/3929167)
- [Index projections in Azure AI Search](https://docs.azure.cn/en-us/search/index-projections-concept-intro?tabs=kstore-rest)
- [Monitor Azure AI Search](https://learn.microsoft.com/en-us/azure/search/monitor-azure-cognitive-search)
- [Foundry IQ: boost response relevance by 36% with agentic retrieval](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-iq-boost-response-relevance-by-36-with-agentic-retrieval/4470720)
- [Foundry IQ: Unlocking ubiquitous knowledge for agents](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-iq-unlocking-ubiquitous-knowledge-for-agents/4470812)
- [Azure Updates - MSFT Foundry](https://azure.microsoft.com/en-us/updates/?searchterms=foundry)
- [Chunk large documents for agentic retrieval and vector search in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents#common-chunking-techniques)
- [Chunk and vectorize by document layout or structure](https://learn.microsoft.com/en-us/azure/search/search-how-to-semantic-chunking)
- [Configure BM25 relevance scoring](https://learn.microsoft.com/en-us/azure/search/index-ranking-similarity)
- [Configure semantic ranker and return captions in search results](https://learn.microsoft.com/en-us/azure/search/semantic-how-to-configure?tabs=portal)
- [Auquan helps financial institutions save 50,000+ hours with Microsoft Azure OpenAI](https://www.microsoft.com/en/customers/story/23303-auquan-azure) - CX story
- [Montgomery County revolutionizes constituent experiences with an AI chatbot powered by Microsoft Azure OpenAI Service](https://www.microsoft.com/en/customers/story/23066-montgomery-county-azure-open-ai-service) - CX story
- [Zenya embraces Azure OpenAI Service to revolutionize healthcare with smart quality management software](https://www.microsoft.com/en/customers/story/23419-zenya-azure-open-ai-service) - CX story
- [Agentic retrieval in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts)

</details>


<details>
<summary><b> Table of Content </b> (Click to expand)</summary>

- [How LLMs fit in?](#how-llms-fit-in)
- [Why quotas differ?](#why-quotas-differ)
- [Scaling approaches](#scaling-approaches)
- [Examples](#examples)
- [How to integrate vector embedding](#how-to-integrate-vector-embedding)
- [Chunking Techniques](#chunking-techniques)

</details>

<img width="1400" height="539" alt="image" src="https://github.com/user-attachments/assets/5a15fdea-7057-468b-bf08-602b84afa9c9" />


> [!NOTE]
> - [BM25](https://learn.microsoft.com/en-us/azure/search/index-similarity-and-scoring) = the baseline keyword relevance algorithm. It scores documents based on term frequency and inverse document frequency. `BM25 is the foundation of traditional search in Azure AI Search.`

<img width="740" height="278" alt="image" src="https://github.com/user-attachments/assets/457fb7d2-9d9c-478c-b1cf-20bdfe25c76e" />

> - [Semantic ranker](https://learn.microsoft.com/en-us/azure/search/semantic-search-overview) = a component that improves relevance by applying transformer-based semantic understanding on top of BM25 results. `Semantic ranker is a tool for better search, enhancing keyword matches with contextual meaning.`

<img width="710" height="399" alt="image" src="https://github.com/user-attachments/assets/7231be89-5aa0-4c63-9532-c232073a4b95" />

> - [Agentic retrieval](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts) = a pipeline that integrates BM25, semantic ranker, and LLM reasoning to handle complex, multi-part queries and produce grounded answers. `Agentic retrieval is a system that uses those tools, orchestrated by LLMs, to make search conversational and intelligent.`

<img width="800" alt="image" src="https://github.com/user-attachments/assets/d1225f14-bc34-4f5c-b0f2-b8702bd77aca" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/8d9f4d6f-e067-440d-97b9-d4a529fbbdcb" />

> Azure AI Search is a cloud search service that `lets you add powerful search capabilities to applications. Instead of just storing data`, it provides:
> - Indexing: You define indexes `(like a database schema) that organize documents for fast retrieval.`
> - Search queries: `Full‑text search, filters, facets, and ranking` across structured and unstructured data.
> - AI enrichment: You can `attach skills (like OCR, entity recognition, or language detection) to enrich raw content during indexing.`
> - Scalability by tiers: Different pricing tiers (Free, Basic, Standard S1–S3, S3 HD) `set hard limits on how many indexes, documents, and storage you can use.` For example: 

## How LLMs fit in?

> Large Language Models (LLMs) e.g GPT‑4 are like expert librarians:
> - They can answer complex questions, summarize, or reason about content.
> - But `even the best librarian is slow if they have to open every book one by one.`
> - With AI Search indexes, the librarian `gets a catalog shortcut`, they know exactly which books to pull before answering.

## Why quotas differ? 

- AI Search indexes are like the physical catalog cards: `you can only fit so many in a system before it breaks. That’s why Microsoft enforces hard caps (e.g., 1,000 in S3 HD).`
- LLM quotas are like the number of questions you can ask the librarian per minute: `Microsoft can increase that by assigning more staff (GPU compute). It’s flexible throughput, not a structural limit.`
    
    | **Service** | **Limit Type** | **Why It’s Fixed or Flexible** |
    |-------------|----------------|--------------------------------|
    | **Azure AI Search** | **Index limits (e.g., 1,000 in S3 HD)** | Each index is a heavy structural object tied to partitions and replicas. Allowing more would destabilize the cluster. Microsoft enforces hard caps to guarantee performance and reliability. |
    | **Azure OpenAI (LLMs)** | **Quota limits (tokens per minute, requests per minute)** | These are throughput controls. Microsoft can allocate more GPU capacity to your tenant if approved. Quotas are “soft” limits that can be raised without changing the architecture. |

    > E.g: 
    
    <img width="1903" height="468" alt="image" src="https://github.com/user-attachments/assets/39908577-2f8d-4b14-a2f5-68c5e29af527" />

## Scaling approaches

> [!NOTE]
> When to use it?
> - Multi‑Tenant Indexes (Most Used) → Use when you have many small tenants and want scalability with logical isolation.
> - Domain‑Based Indexing (Common) → Use when documents share structure (contracts, invoices, catalogs).
> - Metadata Enrichment (Widely Complementary) → Always use when retrieval accuracy matters. 
> - Partitions / Replicas Tuning (Standard Practice) → Use when queries are slow or incomplete due to load.
> - Multi‑Agent Orchestration (Emerging) → Use when queries span multiple domains or need reasoning.
> - Hybrid Model (Growing) → Use when some tenants require strict isolation and others don’t. 
> - Multiple S3 HD Services (Less Common) → Use only when compliance mandates hard isolation or you exceed index limits. 

| Approach | Typical Service / Index Count | Agent Strategy | Isolation Level | Technical Notes |
|----------|-------------------------------|----------------|-----------------|-----------------|
| **Multi‑Tenant Indexes** | 1–4 shared indexes by domain (e.g., invoices, contracts, catalogs) in a single S2/S3 service | Router agent + 3–4 SME agents (per domain) | Logical isolation via `tenantId` filters | Most common SaaS design. Schema must include `tenantId`, `docType`, metadata. Requires strict RBAC and query filter enforcement. Scales easily without hitting index limits. |
| **Domain‑Based Indexing** | 3–6 indexes across domains in one S3 service | 1 agent per domain; optional router agent | Logical isolation via filters | Organizes data by type, simplifies schema. Often combined with multi‑tenant design. Supports federated queries across domains. |
| **Metadata Enrichment** | Same service/index count; focus on enrichment pipeline | Enrichment agent + SMEs | Logical isolation via metadata filters | Adds OCR, entity extraction, embeddings, canonical IDs. Fixes “missing info” issues. Enables hybrid keyword + vector search. Almost always paired with other approaches. |
| **Partitions / Replicas Tuning** | Same service; scale partitions (storage) and replicas (QPS). Typical: 2–4 replicas, 2 partitions | No change | Same as base design | Improves performance and query completeness. Doesn’t increase index count. Used routinely once query load grows. |
| **Multi‑Agent Orchestration** | Depends on index design; typically 1 router agent + 3–6 SME agents | Router agent + SMEs (invoices, contracts, compliance, catalogs) | Logical isolation enforced at agent layer | Router inspects query, selects SME agent, applies tenant filters. Useful for complex B2B SaaS with diverse domains. Adoption is early but promising. |
| **Hybrid Model** | Example: 1 S3 HD service for ~50 large tenants (dedicated indexes) + 1 S3 service with 3 shared indexes for ~1,450 smaller tenants | Router agent + SME agents | Mixed: strong isolation for top tenants, logical for long tail | Balances compliance with scalability. Requires routing logic to decide “dedicated vs shared.” Increasingly popular in B2B SaaS. |
| **Multiple S3 HD Services** | For 1,500 tenants each needing dedicated indexes: 2 services (1,000 + 500). If tenants grow, plan 3 services | 1 router agent | Strong isolation per service | Needed only for strict compliance or >1,000 indexes. Higher operational overhead. Requires tenant→service→index registry. |

## Examples 

| Scenario | Root Cause | Fix |
|----------|------------|-----|
| **Multiple Plans in One Document** | Chunking ignores plan boundaries | Split by plan boundaries + tag `planType` |
| **Different Documents with Shared Language** | Semantic similarity across reused text | Tag `planId` + emphasize numeric fields |


<details>
<summary><b> Multiple Plans Within a Single Document </b> (Click to expand)</summary>

> **Result**: Retrieval only returns chunks from the correct plan variation, even if language overlaps.

> Problem:
> - One document contains multiple plan variations (PPO, HDHP, POS).
> - AI Search chunks the document into passages.
> - Embeddings see semantic similarity across all plan sections.
> - Queries for one plan may return chunks from other plan sections.

> Root Cause:
> - Chunking ignores plan boundaries.
> - Retrieval doesn’t know which plan the member is enrolled in.  

> **Solution Strategy**: 
> 1. **Chunking by Plan Boundaries**  
>    - Split documents at the plan level, not just fixed length.  
>    - Each chunk = one plan variation.  
> 2. **Metadata Enrichment**  
>    - Tag each chunk with `planType` (PPO, HDHP, POS).  
>    - Add `planId` or enrollment ID if available.  
> 3. **Hybrid Retrieval (BM25 + Semantic)**  
>    - BM25 filters on `planType` or enrollment ID.  
>    - Semantic search reranks within the correct plan subset.  
> 4. **Agent Enforcement (Optional)**: SME agent for “plan retrieval” ensures queries only hit the enrolled plan.  

</details>


```mermaid
flowchart LR
    A[Chunk by plan boundaries] --> B[Add planType / planId metadata] --> C[BM25 filter on planType] --> D[Semantic rerank within correct plan] --> E[Optional SME agent enforcement]
```

<details>
<summary><b> Different Documents for Different Plans That Share Standardized Language </b> (Click to expand)</summary>

> **Result**: Retrieval returns the correct plan document, even if text is semantically similar across plans.
  
> **Problem**:
> - Each plan has its own document.  
> - Carriers reuse standardized language across all plan versions.  
> - Embeddings retrieve the wrong plan’s document because text is semantically similar, even though numeric values differ.

> **Root Cause**:
> - Semantic similarity dominates; numeric differences (deductibles, copays) aren’t emphasized.  
> - Retrieval doesn’t anchor on plan identifiers or numeric values.  

> **Solution Strategy**:
> 1. **Metadata Enrichment**  
>    - Add `planId`, `effectiveDate`, `coverageLevel` to each document.  
>    - Index numeric values (deductibles, copays) as structured fields.  
> 2. **Hybrid Retrieval (BM25 + Semantic)**  
>    - BM25 anchors retrieval on exact numeric values and planId.  
>    - Semantic search reranks for contextual similarity.  
> 3. **Agent Enforcement (Optional)**: SME agent for “plan comparison” ensures queries include numeric filters.  

</details>

```mermaid
flowchart LR
    A[Add planId + numeric metadata] --> B[Index numeric values as structured fields] --> C[BM25 filter on planId/numeric values] --> D[Semantic rerank for context] --> E[Optional SME agent enforcement]
```

## How to integrate vector embedding 

<img width="1084" height="651" alt="image" src="https://github.com/user-attachments/assets/9d3f4479-3bc3-4f02-a7c2-1aba628d475c" />

From [Integrated vector embedding in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/vector-search-integrated-vectorization#component-diagram)


## Chunking Techniques
>  Document chunking should balance token limits, semantic coherence, and retrieval accuracy. `The goal is to split large documents into manageable pieces that are small enough for embeddings and LLMs, but still meaningful enough to preserve context.`

> [!TIP]
> - **Chunk size**: Recommended ~512 tokens (~2,000 characters).
> - **Overlap**: ~25% (~128 tokens) to preserve context.
> - **Choice depends on document type**: Narrative vs structured vs conversational.  

>  Why It Matters? 
- Prevents exceeding embedding/LLM limits.  
- Improves **retrieval precision** (finding the right chunk).  
- Enhances **answer grounding** with citations.  
- Enables **agentic retrieval** pipelines to work effectively with multi-query decomposition.  

| **Technique** | **How it Works** | **Pros** | **Cons** | **Best Use Cases** |
|---------------|------------------|----------|----------|--------------------|
| **Fixed-size chunks** | Splits text into blocks of a set length (e.g., 512 tokens or 2,000 characters). Often includes overlap (10–25%). | Simple, predictable, easy to implement. | May break sentences or context mid-way. | Large narrative documents, technical manuals. |
| **Variable-sized chunks** | Breaks text based on natural boundaries like sentences, paragraphs, or headings. | Preserves readability and logical flow. | Chunk sizes can vary widely, affecting retrieval consistency. | Articles, structured documents, Markdown/HTML files. |
| **Semantic chunks** | Uses NLP or AI to split text into meaningful units that preserve semantic relationships. | High-quality context preservation, better search relevance. | More complex, requires AI processing. | Conversational text, FAQs, knowledge bases. |
| **Custom combinations** | Mixes fixed and variable approaches, e.g., adding titles or metadata to chunks. | Flexible, balances context and efficiency. | Requires tuning and experimentation. | Enterprise apps needing both precision and recall. |
| **Document parsing** | Indexers parse large files (Markdown, JSON, PDFs) into smaller search documents. | Automated, efficient for structured files. | Less control over chunk boundaries. | Technical documents, structured datasets. |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
