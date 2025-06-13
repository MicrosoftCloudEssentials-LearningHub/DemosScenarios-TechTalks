#  Microsoft Build (Seattle, Washington 2025) - Analytics Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-04-08

----------

>  `Seattle from May 19 to May 21.`. Showcased significant advancements and innovations across different domains of Microsoft products. 

 
<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [ Microsoft Build 2025 BOOK OF NEWS](https://news.microsoft.com/build-2025-book-of-news/?msockid=38ec3806873362243e122ce086486339)

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Create powerful AI agents in Azure AI Foundry with data in Azure Databricks](#create-powerful-ai-agents-in-azure-ai-foundry-with-data-in-azure-databricks)
- [Expanding Chat with User Data Capabilities to Power BI and Copilot Studio](#expanding-chat-with-user-data-capabilities-to-power-bi-and-copilot-studio)
- [Digital Twin Builder in Microsoft Fabric Now in Preview](#digital-twin-builder-in-microsoft-fabric-now-in-preview)
- [Shortcut Transformations Help Create AI-Ready Data Faster in OneLake](#shortcut-transformations-help-create-ai-ready-data-faster-in-onelake)
- [Translytical Task Flows in Microsoft Fabric in Preview](#translytical-task-flows-in-microsoft-fabric-in-preview)

</details>

## Create powerful AI agents in Azure AI Foundry with data in Azure Databricks

> Azure AI Foundry now integrates with **Azure Databricks**, enabling **multi-agent orchestration** with **real-time data processing**.
> `With our new integration between Azure AI Foundry and Azure Databricks, we’re empowering developers to build intelligent AI agents that can access and process enterprise data in real time. These agents can run Spark jobs, interact with data using natural language, and operate securely under Unity Catalog governance.` This integration brings AI closer to your data, enabling smarter and faster decision-making across the organization.

> [!IMPORTANT]  
> **Agents can now leverage Databricks Delta Lake** for **low-latency data access**, improving AI-driven decision-making.

> [!TIP]  
> Use **Databricks AutoML** to automate feature selection and hyperparameter tuning for AI models.

| **Concept**                   | **Description**                                                         | **Key Benefits**                                      |
|--------------------------------|------------------------------------------------------------------------|------------------------------------------------------|
| **Event-driven AI workflows**  | Agents can **subscribe to Databricks event streams** for real-time inference. | - Enables **low-latency decision-making** <br> - Automates responses such as fraud detection <br> - Improves **scalability** for high-volume data processing |
| **Federated learning**         | AI models can **train across distributed datasets** without centralizing sensitive data. | - Preserves **data privacy** <br> - Supports **edge computing** for AI training on local devices <br> - Enables **collaborative AI development** without raw data sharing |
| **Vector search optimization** | **Databricks MLflow** supports **embedding-based retrieval**, enhancing **semantic search**. | - Improves **search accuracy** by finding semantically relevant results <br> - Optimizes **fast query execution** <br> - Enhances AI applications like **chatbots & recommendation systems** |

<details>
<summary><b>Event-Driven AI Workflows</b></summary>

> Event-driven architectures are crucial for AI applications that need real-time responsiveness. By **subscribing to Databricks event streams**, AI agents can perform **real-time inference** based on incoming data. This means AI models can react instantly to new information, such as financial transactions, sensor data, or user interactions.

**Key Benefits**:
- **Low-latency decision-making**: AI models process and analyze data as soon as an event occurs.
- **Automated responses**: Systems trigger actions automatically (such as fraud detection alerts or dynamic pricing updates).
- **Scalability**: Distributed event processing enables AI models to handle massive data flows efficiently.
</details>

<details>
<summary><b>Federated Learning</b></summary>

> Federated learning allows AI models to **train across distributed datasets** without centralizing sensitive data, ensuring privacy and security.

**Use Cases**:
- **Data privacy compliance**: Healthcare and finance industries can train models while keeping sensitive information secure.
- **Edge computing applications**: AI models train directly on edge devices, like smartphones or IoT sensors, reducing reliance on cloud computing.
- **Collaborative AI training**: Organizations can improve AI models collectively without sharing their raw data.
</details>

<details>
<summary><b>Vector Search Optimization</b></summary>

> With the rise of unstructured data (text, images, audio) **embedding-based retrieval** enhances **semantic search** accuracy. **Databricks MLflow** integrates optimized vector search, allowing AI systems to find relevant information efficiently.

**Advantages**:

- **Improved accuracy**: Searches return more meaningful results by considering semantic similarity rather than exact keyword matches.
- **Fast query execution**: Optimized indexing methods speed up retrieval, making it scalable.
- **Enhanced AI applications**: Useful for chatbots, recommendation systems, and large-scale document search.
</details>

## **Expanding Chat with User Data Capabilities to Power BI and Copilot Studio**  

> Microsoft extends **chat-based AI interactions** with **user data** across **Power BI** and **Copilot Studio**, enabling **context-aware AI responses**.  
> `We’re making it easier than ever to explore data using natural language. With the new “Chat with your data” experience in Power BI and Copilot Studio, users can simply ask questions and get insights without needing to dig through reports or write complex queries. Business users in Power BI can now chat with data agents without switching context`. Whether you're a business analyst or a data scientist, our AI-powered agents help you find answers quickly using the tools you already know and trust.

> [!IMPORTANT]  
> **Copilot Studio now supports fine-tuned LLMs**, allowing **custom AI agents** to interact with **Power BI datasets**.  

> [!TIP]  
> Use **Power BI’s DirectQuery mode** for **low-latency AI-driven insights**.  

| **Concept**                      | **Description**                                                          | **Key Benefits**                                      |
|-----------------------------------|--------------------------------------------------------------------------|------------------------------------------------------|
| **Dynamic query generation**      | AI agents can **convert natural language prompts into optimized DAX queries**. | - Enables **real-time AI-driven insights** <br> - Reduces need for manual query building <br> - Enhances usability for non-technical users |
| **Adaptive reasoning**            | Agents can **adjust responses based on real-time data updates** in Power BI. | - Improves AI decision-making based on latest data <br> - Enables **dynamic and evolving responses** <br> - Supports **predictive analytics** |
| **Multi-modal AI**                | **Copilot Studio now integrates with Azure Speech Services**, enabling **voice-driven analytics**. | - Expands AI accessibility with **speech-based interaction** <br> - Supports **multi-modal user engagement** <br> - Enhances **hands-free data exploration** |

<details>
<summary><b>Dynamic Query Generation</b></summary>

> AI agents can **convert natural language prompts into optimized DAX queries**, making data exploration more intuitive.  

**Key Benefits**:
- **Real-time insights**: Enables AI-driven, **on-the-fly** query generation for instant data retrieval.  
- **Reduced complexity**: Users no longer need manual query expertise to analyze Power BI data.  
- **Enhanced usability**: Improves accessibility for **business users** and non-technical stakeholders.  
</details>

<details>
<summary><b>Adaptive Reasoning</b></summary>

> Agents can **adjust responses based on real-time data updates** in Power BI, ensuring decisions are informed by the latest trends.  

**Use Cases**:
- **Context-aware analytics**: AI-driven recommendations evolve **as new data streams in**.  
- **Predictive insights**: AI models refine predictions dynamically to enhance forecasting accuracy.  
- **Business intelligence**: Organizations benefit from **self-learning AI systems** that adapt over time.  
</details>

<details>
<summary><b>Multi-Modal AI</b></summary>

> **Copilot Studio now integrates with Azure Speech Services**, enabling **voice-driven analytics** for hands-free data exploration.  

**Advantages**:
- **Speech-based interactions**: Users can ask AI for insights **without typing queries**.  
- **Multi-modal experiences**: Combines text, voice, and visual AI components for richer engagement.  
- **Accessible analytics**: Improves usability for mobile and remote AI interactions.  
</details>

## **Digital Twin Builder in Microsoft Fabric Now in Preview**  

> Microsoft Fabric introduces a **Digital Twin Builder**, enabling **graph-based modeling** for **predictive analytics**.
> `With the new Digital Twin Builder in Microsoft Fabric, we’re simplifying how organizations model and simulate real-world systems. Using a no-code or low-code interface, even non-technical users can create digital twins by connecting live data from physical assets and processes. You can visualize and analize digital twin data with Power Bi and Copilot in MS Fabric`. These models can then power deep analytics, support what-if scenarios, and enable AI-driven automation, unlocking new levels of operational insight and efficiency.

> [!IMPORTANT]  
> **Fabric’s Digital Twin API** now supports **real-time IoT telemetry ingestion**, improving **asset monitoring**.  

> [!TIP]  
> Use **Azure Stream Analytics** to **preprocess IoT telemetry** before feeding it into digital twin models.  

| **Concept**                     | **Description**                                                          | **Key Benefits**                                      |
|----------------------------------|--------------------------------------------------------------------------|------------------------------------------------------|
| **Edge AI processing**           | Digital twins can **run inference on Azure IoT Edge**, reducing cloud dependency. | - Enables **real-time localized AI processing** <br> - Minimizes **latency** by keeping computations at the edge <br> - Reduces **cloud bandwidth usage** |
| **Graph-based anomaly detection** | **Fabric’s Graph Engine** enables **relationship-aware AI models**. | - Improves detection of **complex dependencies in systems** <br> - Enhances **predictive maintenance** for industrial assets <br> - Supports **dynamic pattern recognition** |
| **Synthetic data generation**     | AI can **simulate operational scenarios** for **risk assessment**. | - Enables **robust AI training** without real-world exposure <br> - Enhances **risk analysis** for predictive modeling <br> - Supports **virtual testing environments** |

<details>
<summary><b>Edge AI Processing</b></summary>

> Digital twins can **run inference on Azure IoT Edge**, reducing cloud dependency while maintaining real-time analytics.  

**Key Benefits**:
- **Localized AI execution**: Keeps processing close to IoT devices, minimizing network delays.  
- **Cloud efficiency**: Reduces the need for continuous cloud synchronization.  
- **Scalability**: Allows AI to operate seamlessly across **distributed edge environments**.  
</details>

<details>
<summary><b>Graph-Based Anomaly Detection</b></summary>

> **Fabric’s Graph Engine** enables **relationship-aware AI models**, improving anomaly detection and system intelligence.  

**Use Cases**:
- **Predictive maintenance**: Detects irregularities in **industrial machinery** before failures occur.  
- **Complex system analysis**: Identifies patterns in **multi-node IoT networks**.  
- **Fraud detection**: Enhances AI’s ability to recognize suspicious behavioral patterns in **financial transactions**.  
</details>

<details>
<summary><b>Synthetic Data Generation</b></summary>

> AI can **simulate operational scenarios** for **risk assessment**, allowing businesses to model hypothetical conditions effectively.  

**Advantages**:
- **Training AI models**: Provides **scalable data augmentation** for AI learning.  
- **Reducing real-world risks**: Enables testing of edge cases **without real-world consequences**.  
- **Scenario simulation**: Supports predictive insights for **supply chain management, cybersecurity, and disaster recovery**.  
</details>

## **Shortcut Transformations Help Create AI-Ready Data Faster in OneLake**  

> OneLake now supports **shortcut transformations**, enabling **automated data preprocessing** for **AI model training**.
> `We’re evolving OneLake into a true hub for enterprise data. With shortcut transformations, users can bring in data from multiple sources and automatically convert it into analytics-ready formats like Delta Lake. Even better, they can apply AI-powered transformations such as summarization, translation, and classification in real time, without duplicating or moving the data.` It’s a seamless and efficient way to prepare data for analysis and AI.

> [!IMPORTANT]  
> **OneLake’s new transformation engine** supports **schema evolution**, allowing **adaptive data pipelines**.  

> [!TIP]  
> Use **Azure Synapse Link** to **streamline data movement** between OneLake and Azure ML.  

| **Concept**                         | **Description**                                                            | **Key Benefits**                                       |
|--------------------------------------|---------------------------------------------------------------------------|------------------------------------------------------|
| **Automated feature engineering**    | AI models can **dynamically adjust feature sets** based on **data drift**. | - Enhances **AI model accuracy** by refining features on-the-fly <br> - Reduces **manual intervention** for data preprocessing <br> - Enables **self-optimizing AI workflows** |
| **Hybrid cloud processing**          | **OneLake now supports Azure Arc**, enabling **cross-cloud AI workflows**. | - Allows seamless **data integration across cloud environments** <br> - Supports **distributed computing** for AI tasks <br> - Improves flexibility for **multi-cloud AI models** |
| **GPU-accelerated transformations**  | **Azure ML Compute** can now **parallelize OneLake transformations**. | - Speeds up **data preprocessing** for AI model training <br> - Leverages **high-performance GPU clusters** for intensive workloads <br> - Enhances **scalability for enterprise AI applications** |

<details>
<summary><b>Automated Feature Engineering</b></summary>

> AI models can **dynamically adjust feature sets** based on **data drift**, ensuring data remains relevant for predictions.  

**Key Benefits**:
- **Continuous adaptation**: AI automatically refines features as data patterns evolve.  
- **Improved AI model performance**: Reduces bias and enhances **predictive accuracy**.  
- **Less manual tuning**: Enables efficient **self-optimizing AI workflows**.  
</details>

<details>
<summary><b>Hybrid Cloud Processing</b></summary>

> **OneLake now supports Azure Arc**, enabling **cross-cloud AI workflows** for greater flexibility in model deployment.  

**Use Cases**:
- **Multi-cloud AI models**: Seamlessly integrates data across Azure, AWS, and other platforms.  
- **Distributed AI training**: Supports **scalable AI computation** across various cloud environments.  
- **Flexible infrastructure**: Allows **on-premises and cloud collaboration** for AI-driven applications.  
</details>

<details>
<summary><b>GPU-Accelerated Transformations</b></summary>

> **Azure ML Compute** can now **parallelize OneLake transformations**, significantly reducing AI training time.  

**Advantages**:
- **High-speed data processing**: Reduces bottlenecks in data preparation for AI models.  
- **Scalable AI computation**: Supports **large-scale AI deployments** using GPU acceleration.  
- **Optimized machine learning workflows**: Enhances **deep learning and complex AI model training**.  
</details>

## **Translytical Task Flows in Microsoft Fabric in Preview**  

> Microsoft Fabric introduces **Translytical Task Flows**, merging **transactional and analytical processing**.
> `We’re taking Power BI beyond visualization by enabling users to take action directly from their reports. With translytical task flows, users can update records, trigger workflows, or call external APIs based on the context of the data they’re viewing. This bridges the gap between analytics and operations, helping teams move from insight to action without ever leaving the report.`

> [!IMPORTANT]  
> **Fabric’s Translytical Engine** now supports **HTAP (Hybrid Transactional/Analytical Processing)**, reducing **ETL overhead**.  

> [!TIP]  
> Use **Azure Cosmos DB’s HTAP capabilities** to **accelerate AI-driven analytics**.  

| **Concept**                     | **Description**                                                          | **Key Benefits**                                      |
|----------------------------------|--------------------------------------------------------------------------|------------------------------------------------------|
| **Real-time AI inference**       | AI models can **run predictions directly on operational data**, eliminating batch delays. | - Enables **instant decision-making** <br> - Reduces latency for AI-driven applications <br> - Supports **real-time business intelligence** |
| **Adaptive indexing**            | **Fabric’s HTAP engine** dynamically **adjusts query execution plans**, optimizing performance. | - Improves **query efficiency** with automated adjustments <br> - Enhances **transactional workloads** for AI-driven analytics <br> - Reduces **manual indexing efforts** |
| **AI-driven anomaly detection**  | **Translytical workflows** enable **instant fraud detection** by merging transactional and analytical data. | - Detects **irregular patterns in financial transactions** <br> - Enhances **risk analysis in operational systems** <br> - Supports **proactive security measures** |

<details>
<summary><b>Real-Time AI Inference</b></summary>

> AI models can **run predictions directly on operational data**, removing batch processing delays for faster decision-making.  

**Key Benefits**:
- **Instant insights**: AI-driven predictions adjust dynamically to new data streams.  
- **Optimized workflows**: Reduces the need for staged batch inference.  
- **Business intelligence enhancement**: Supports real-time forecasting and predictive analytics.  
</details>

<details>
<summary><b>Adaptive Indexing</b></summary>

> **Fabric’s HTAP engine** dynamically **adjusts query execution plans**, reducing overhead and improving performance.  

**Use Cases**:
- **Optimized query execution**: AI refines indexing based on **workload patterns**.  
- **Enhanced AI-driven applications**: Supports **hybrid query processing** in real-time environments.  
- **Efficient data operations**: Reduces manual indexing adjustments while improving speed.  
</details>

<details>
<summary><b>AI-Driven Anomaly Detection</b></summary>

> **Translytical workflows** merge transactional and analytical processing to **detect fraud and system anomalies instantly**.  

**Advantages**:
- **Proactive fraud detection**: Identifies irregularities **before transactions are completed**.  
- **Risk mitigation**: AI enhances cybersecurity and financial protection.  
- **Real-time security updates**: Supports dynamic monitoring for AI-powered risk analysis.  
</details>

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
