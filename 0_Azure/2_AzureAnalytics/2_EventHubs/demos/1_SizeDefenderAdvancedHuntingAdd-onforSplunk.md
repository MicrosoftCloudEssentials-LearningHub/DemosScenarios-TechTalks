# Event Hub Sizing for Microsoft Defender Advanced Hunting Add-on for Splunk - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> The goal is to collect endpoint telemetry logs, such as registry changes, port activity, filesystem modifications, process information, and service details, into Splunk. This data will be used for incident response, threat hunting, and compliance. <br/>

> [Microsoft Defender Advanced Hunting Add-on for Splunk](https://splunkbase.splunk.com/app/5518) can pull the necessary data. This add-on provides field extractions and CIM (Common Information Model: it is a standard used in Splunk to normalize data from different sources into a common format) compatibility for the Endpoint datamodel for Microsoft Defender Advanced Hunting data. It maps Device Alert events to the Alerts datamodel and supports detection searches in Splunk Enterprise Security Content Update.

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Sysmon v15.15](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Compare Azure Event Hubs tiers](https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers)
- [Microsoft Defender Advanced Hunting Add-on for Splunk](https://splunkbase.splunk.com/app/5518)
- [Monitor Azure Event Hubs](https://learn.microsoft.com/en-us/azure/event-hubs/monitor-event-hubs?tabs=AzureDiagnostics%2CAzureDiagnosticsforRuntimeAudit%2CAzureDiagnosticsforAppMetrics)
- [Pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)
- [Quickstart: Create a Dedicated Azure Event Hubs cluster using Azure portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-dedicated-cluster-create-portal)
- [Capture events through Azure Event Hubs in Azure Blob Storage or Azure Data Lake Storage](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-capture-overview)

</details>

> [!TIP]
> Sysmon (System Monitor) is a Windows system service and device driver that monitors and logs system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time.

## Content 

- [Overview](#overview)
- [Event Hub Sizing](#event-hub-sizing)
    - [Step 1: Determine Ingress Data Rate](#step-1-determine-ingress-data-rate)
    - [Step 2: Calculate Throughput Units TUs](#step-2-calculate-throughput-units-tus)
    - [Step 3: Monitor and Adjust](#step-3-monitor-and-adjust)
- [Installation Steps](#installation-steps)
- [Example Calculation](#example-calculation)
- [How to achieve more TUs](#how-to-achieve-more-tus)

## Overview 

| **Feature**                          | **Description**                                                                                       |
|--------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Field Extractions and CIM Compatibility** | Ensures that the data is structured and can be easily queried within Splunk. CIM standardizes data fields across different sources for consistent searching and reporting. |
| **Sysmon-like Data**                 | Provides detailed telemetry similar to what Sysmon logs offer, including process creation, network connections, and file modifications. |
| **Future Support**                   | Plans to support additional Microsoft 365 products like Microsoft Defender for Office 365 and Microsoft Defender for Identity. This ensures broader coverage and integration of security data. |
| **Event Hub for Data Ingestion**     | Uses Azure Event Hub to avoid REST API rate limits, ensuring reliable and scalable data ingestion. Event Hub can handle large volumes of data efficiently. |

 ```mermaid
  graph TD
    A[Microsoft Defender for Endpoint] -->|Streams Advanced Hunting Events| B[Azure Event Hub]
    B -->|Ingests Data| C[Splunk]

    subgraph Splunk
        direction TB
        C1[Splunk Heavy Forwarders] -->|Forwards Data| C2[Splunk Indexers]
        C2 -->|Indexes Data| C3[Splunk Search Heads]
        C3 -->|Runs Searches and Reports| C4[Step 6: Verification+]
    end

    subgraph Explanation
        direction TB
        C1 -->|Handles initial data ingestion| E1[Heavy Forwarders]
        C2 -->|Processes and stores data| E2[Indexers]
        C3 -->|Allows querying + analysis| E3[Search Heads]
        C4 -->|Ensures DataIntegrity+alerts| E4[Step 6: Verification+]
    end 
```

1. **Microsoft Defender for Endpoint** streams Advanced Hunting events to `Azure Event Hub`.
2. **Azure Event Hub** ingests the data and forwards it to `Splunk Heavy Forwarders`.
3. **Splunk Heavy Forwarders** forward the data to `Splunk Indexers`.
4. **Splunk Indexers** index the data, making it searchable.
5. **Splunk Search Heads** run searches and reports on the indexed data.
6. **Verification and Scheduled Searches** are performed on the data within Splunk to ensure data integrity and generate necessary alerts and reports.

## Event Hub Sizing

> To right-size the Event Hub, estimate the average record collection volume to determine the appropriate number of Throughput Units (TUs).

<div align="center">
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/51707336-0e21-4369-ac39-a9817288b12d" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

> [!IMPORTANT]
> Please click here see a table shows the [list of features that are available (or not available)](https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers#features) in a specific tier of Azure Event Hubs. <br/>
> Here for [table shows limits that are different for Basic, Standard, Premium, and Dedicated tiers](https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers#quotas)

<table>
  <tr>
    <th>Tier</th>
    <th>Description</th>
    <th>Plans</th>
  </tr>
  <tr>
    <td><strong>Basic</strong></td>
    <td>Suitable for development and testing scenarios. It offers limited features and lower throughput capacity.</td>
    <td rowspan="4" style="text-align: center;">
      <img width="600" alt="image" src="https://github.com/user-attachments/assets/0c906563-e749-4d6b-abed-97eb48434c46" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
    </td>
  </tr>
  <tr>
    <td><strong>Standard</strong></td>
    <td>Provides higher throughput and additional features such as Capture, which allows you to automatically capture streaming data. Option available for Auto-Inflate: automatically scales the number of Throughput Units assigned to your Standard Tier Event Hubs Namespace when your traffic exceeds the capacity of the Throughput Units assigned to it. You can specify a limit to which the Namespace will automatically scale.</td>
  </tr>
  <tr>
    <td><strong>Premium</strong></td>
    <td>Offers enhanced performance, higher throughput, and additional features for mission-critical applications.</td>
  </tr>
  <tr>
    <td><strong>Dedicated</strong></td>
    <td>Provides dedicated resources for the highest throughput and performance, suitable for large-scale enterprise applications.</td>
  </tr>
</table>

https://github.com/user-attachments/assets/b8302c11-f668-4ea8-850a-980e4733523f

### Step 1: Determine Ingress Data Rate

| **Step**          | **Action**| **Example**| **Metric**        | **Value**             | **Formula** |
|------------|---------------------|-------------------------------------|-------|-----|-------------|
| **Data Sources**  | Identify all devices and systems that will provide telemetry data.| Endpoints, servers, network devices, applications.| **Number of Sources** | Endpoints: 200, Servers: 50 | N/A|
| **Data Volume**   | Calculate the average amount of data generated by each source per second.| Endpoint generates 0.25 MB/s, server generates 1 MB/s.| **Total Data Volume (MB/s)** | Endpoints: 50, Servers: 50 | Number of Sources * Data Volume per Source |
| **Event Rate**    | Determine the frequency of events generated by each source per second.| Endpoint generates 2 events/s, server generates 5 events/s.| **Total Event Rate (events/s)** | Endpoints: 400, Servers: 250 | Number of Sources * Event Rate per Source |

### Step 2: Calculate Throughput Units (TUs)

> Each TU provides: <br/>
> Up to 1 MB per second of ingress events. <br/>
> Up to 2 MB per second of egress events.

> [!NOTE]
> The required TUs will be the maximum of the two calculated values.

$$
\text{Required TUs} = \max \left( \frac{\text{Ingress MB/s}}{1}, \frac{\text{Events/second}}{1000} \right)
$$

### Step 3: Monitor and Adjust

1. **Deploy the Event Hub** with the calculated TUs.
2. **Monitor Metrics** to ensure the Event Hub performs as expected.
3. **Adjust TUs** as needed based on real-time data.
4. **Auto-Inflate Feature**: Start with a lower number of TUs and set an upper threshold for automatic scaling.

## Installation Steps

<details>
<summary><b>Step 1: Configure Microsoft Defender for Endpoint</b></summary>

**Action:** Stream Advanced Hunting events to an Azure Event Hub

**Details:**
- **Create an Azure Event Hub namespace and Event Hub:**
  - Navigate to the Azure Portal.
  - Select `Create a resource` and search for `Event Hubs`.
  - Create a new Event Hub namespace and within it, create an Event Hub.
  - Note down the connection string for the Event Hub.

- **Configure Microsoft Defender for Endpoint to stream events to the Event Hub:**
  - Access the Microsoft Defender Security Center.
  - Go to `Settings` > `Advanced features`.
  - Enable the `Streaming API` and configure it to stream events to the Azure Event Hub using the connection string.

- **Ensure necessary permissions are granted:**
  - Ensure that the Azure Event Hub has the necessary permissions to receive data from Microsoft Defender for Endpoint.
  - Assign the appropriate roles (e.g., `Event Hub Data Sender`) to the Defender for Endpoint service principal.

**Example/Command:**
- **Azure Portal:** Create Event Hub
- **Defender Security Center:** Enable Streaming API

</details>

<details>
<summary><b>Step 2: Install the Add-on</b></summary>

**Action:** Install the Add-on on your Search Heads, Indexers, and Heavy Forwarders

**Details:**
- **Download the Microsoft Defender Advanced Hunting Add-on for Splunk:**
  - Visit Splunkbase and search for `Microsoft Defender Advanced Hunting Add-on`.
  - Download the add-on package.

- **Install the add-on on all relevant Splunk components:**
  - Log in to your Splunk instance.
  - Navigate to `Apps` > `Manage Apps`.
  - Click `Install app from file` and upload the downloaded add-on package.
  - Repeat the installation process for Search Heads, Indexers, and Heavy Forwarders.

- **Configure the add-on as per your environment requirements:**
  - Access the add-on configuration page.
  - Set parameters such as the index, sourcetype, and any other environment-specific settings.

**Example/Command:**
- **Splunkbase:** Download Add-on
- **Splunk UI:** Apps > Manage Apps > Install app from file

</details>

<details>
<summary><b>Step 3: Set up the Input</b></summary>

**Action:** Set up the Input in the Splunk Add-on for Microsoft Cloud Services

**Details:**
- **Navigate to the Splunk Add-on for Microsoft Cloud Services configuration page:**
  - Open Splunk and go to `Settings` > `Data Inputs`.

- **Add a new input for Azure Event Hub:**
  - Select `Azure Event Hub` as the input type.
  - Provide the connection string for the Azure Event Hub.

- **Set the Sourcetype to `mscs:azure:eventhub:defender:advancedhunting`:**
  - In the input configuration, set the sourcetype to `mscs:azure:eventhub:defender:advancedhunting`.

- **Configure other parameters such as index, interval, and format:**
  - Specify the index where the data should be stored.
  - Set the interval for data collection.
  - Configure the format and any other relevant parameters.

**Example/Command:**
- **Splunk UI:** Settings > Data Inputs > Azure Event Hub
- **Sourcetype:** `mscs:azure:eventhub:defender:advancedhunting`

</details>

<details>
<summary><b>Step 4: Verify Data Arrival</b></summary>

**Action:** Run a search to verify data arrival

**Details:**
- **Open the Splunk Search & Reporting app:**
  - Navigate to the `Search & Reporting` app in Splunk.

- **Run the search query to verify that data is being ingested correctly:**
  - Use the following search query to check for incoming data:
  ```spl
  index=* eventtype="ms_defender_advanced_hunting_sourcetypes"
  ```

**Example/Command:**
```spl
index=* eventtype="ms_defender_advanced_hunting_sourcetypes"
```

</details>

<details>
<summary><b>Step 5: Enable Scheduled Saved Searches</b></summary>

**Action:** Enable Scheduled Saved Searches for Malware and Email data models

**Details:**
- **Navigate to Saved Searches in Splunk:**
  - Go to `Settings` > `Searches, Reports, and Alerts`.

- **Create new saved searches for malware and email data models:**
  - Click `New Search` and define search queries for malware and email data models.
  - Example search queries:
  ```spl
  index=* sourcetype="defender:advancedhunting:malware"
  index=* sourcetype="defender:advancedhunting:email"
  ```

- **Schedule the searches to run at regular intervals (e.g., every hour):**
  - Set the schedule for the saved searches to run at desired intervals.

- **Configure alert actions if needed:**
  - Define alert actions such as email notifications or script execution.

- **Verify data generation by running the saved searches manually:**
  - Execute the saved searches manually to ensure they generate the expected results.

**Example/Command:**
- **Splunk UI:** Settings > Searches, Reports, and Alerts
- **Example search queries:**
```spl
index=* sourcetype="defender:advancedhunting:malware"
index=* sourcetype="defender:advancedhunting:email"
```

</details>

## Example Calculation

> Assume we have 200 endpoints and 50 servers. <br/>
> - Each endpoint sends 0.25 MB of data per second and generates 2 events per second.
> - Each server sends 1 MB of data per second and generates 5 events per second.

1. **Total Ingress Data Rate**:

$$
\text{Total Ingress MB/s} = (\text{Number of Endpoints} \times \text{Data Volume per Endpoint (MB/s)}) + (\text{Number of Servers} \times \text{Data Volume per Server (MB/s)})
$$

$$
\text{Total Ingress MB/s} = (200 \text{ endpoints} \times 0.25 \text{ MB/s per endpoint}) + (50 \text{ servers} \times 1 \text{ MB/s per server}) = 50 \text{ MB/s} + 50 \text{ MB/s} = 100 \text{ MB/s}
$$

2. **Total Event Rate**:

$$
\text{Total Events/second} = (\text{Number of Endpoints} \times \text{Event Rate per Endpoint (events/second)}) + (\text{Number of Servers} \times \text{Event Rate per Server (events/second)})
$$

$$
\text{Total Events/second} = (200 \text{ endpoints} \times 2 \text{ events/second per endpoint}) + (50 \text{ servers} \times 5 \text{ events/second per server}) = 400 \text{ events/second} + 250 \text{ events/second} = 650 \text{ events/second}
$$

3. **Calculate Required TUs**:

> Required TUs for MB/s (Ingress Data):

$$
\text{Required TUs for MB/s} = \frac{\text{Total Ingress MB/s}}{1 \text{ MB/s per TU}}
$$

$$
\text{Required TUs for MB/s} = \frac{100 \text{ MB/s}}{1 \text{ MB/s per TU}} = 100 \text{ TUs}
$$

> Required TUs for Events/second:

$$
\text{Required TUs for Events/second} = \frac{\text{Total Events/second}}{1000 \text{ events/second per TU}}
$$

$$
\text{Required TUs for Events/second} = \frac{650 \text{ events/second}}{1000 \text{ events/second per TU}} = 0.65 \text{ TUs}
$$

4. **Determine the Maximum Value**:

$$
\text{Required TUs} = \max \left( \frac{\text{Total Ingress MB/s}}{1}, \frac{\text{Total Events/second}}{1000} \right)
$$

$$
\text{Required TUs} = \max(100, 0.65) = 100 \text{ TUs}
$$

| **Step**          | **Action**                                                                                     | **Example**                                                                 | **Metric**        | **Value**             | **Formula** |
|-------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|-------------------|-----------------------|-------------|
| **Data Sources**  | Identify all devices and systems that will provide telemetry data.                            | Endpoints, servers, network devices, applications.                          | **Number of Sources** | Endpoints: 200, Servers: 50 | N/A         |
| **Data Volume**   | Calculate the average amount of data generated by each source per second.                     | Endpoint generates 0.25 MB/s, server generates 1 MB/s.                      | **Total Data Volume (MB/s)** | Endpoints: 50, Servers: 50 | Number of Sources * Data Volume per Source |
| **Event Rate**    | Determine the frequency of events generated by each source per second.                        | Endpoint generates 2 events/s, server generates 5 events/s.                 | **Total Event Rate (events/s)** | Endpoints: 400, Servers: 250 | Number of Sources * Event Rate per Source |
| **Required TUs**  | Calculate the required Throughput Units based on data volume and event rate.                  | Total Ingress MB/s = 100, Total Events/second = 650                          | **Required TUs** | 100 | Max value between the two: 100/1 = (100) or 650/1000 = (0.65) |

## How to achieve more TUs

> Azure Event Hubs has specific limits on the number of Throughput Units (TUs) that can be assigned to a single Event Hub. As of my last update, the maximum number of TUs for a single Event Hub in the Standard tier is 40. If you need more than 40 TUs, you would need to use multiple Event Hubs or consider other strategies.

| **Method**| **Description**| **Steps** |
|-----------------------------------------|--------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Using Multiple Event Hubs with Load Balancer** | Distribute the data load across multiple Event Hubs using a load balancer.| Create four Event Hubs with 25 TUs each, set up load balancer, configure data sources.|
| **Partitioning Data Streams**           | Divide data streams into smaller chunks and send to different Event Hubs.| Create multiple Event Hubs, partition data streams, configure data sources.|
| **Using Event Hub Namespaces**          | Manage multiple Event Hubs under a single namespace.| Create an Event Hub namespace, create multiple Event Hubs, configure data sources.            |
| **Using Azure Stream Analytics**        | Process and route data streams to multiple Event Hubs.| Create Stream Analytics job, configure inputs and outputs, define query.                      |
| **Using Azure Data Factory**            | Orchestrate and manage data flows between multiple Event Hubs.| Create Data Factory, create pipelines, configure data sources, configure Event Hubs.          |
| **Using Event Hubs Dedicated Clusters** | Provision a single-tenant cluster with high capacity and low latency.| Create a dedicated cluster, create namespaces and event hubs, distribute data.                |

> Configuration Steps:

<details>
<summary>1. Using Multiple Event Hubs with Load Balancer</summary>

> Distribute the data load across multiple Event Hubs using a load balancer.

- **Load Balancer Configuration**:
  - Use the Azure portal or Azure CLI to create and configure the load balancer.
  - Define backend pools consisting of the four Event Hubs.
  - Set up rules to distribute traffic based on round-robin or other algorithms.
- **Health Probes**:
  - Configure HTTP or TCP health probes to periodically check the status of each Event Hub.
  - Define thresholds for probe responses to determine when an Event Hub is considered unhealthy.

**Steps**:
1. **Create Four Event Hubs**: 
   - Navigate to the Azure portal.
   - Create four Event Hubs, each configured with 25 TUs.
   - Ensure each Event Hub is set up within the same region for optimal performance.

2. **Set Up Load Balancer**: 
   - Create an Azure Load Balancer.
   - Configure the load balancer to distribute incoming data evenly across the four Event Hubs.
   - Set up health probes to monitor the status of each Event Hub and ensure data is routed to healthy instances.

3. **Configure Data Sources**: 
   - Update your data sources to send data to the load balancer's IP address or DNS name.
   - Ensure data sources are configured to handle failover scenarios, redirecting data to other Event Hubs if one becomes unavailable.

</details>

<details>
<summary>2. Partitioning Data Streams</summary>

> Divide the data streams into smaller, manageable chunks and send them to different Event Hubs.

- **Partitioning Strategy**:
  - Use hashing algorithms to partition data based on device ID or other criteria.
  - Implement partitioning logic within Azure Functions or custom applications.
- **Data Source Configuration**:
  - Use SDKs or APIs to configure data sources to send data to specific Event Hubs.
  - Implement retry logic to handle failover scenarios.

**Steps**:
1. **Create Multiple Event Hubs**: 
   - Navigate to the Azure portal.
   - Create multiple Event Hubs, each with a portion of the required TUs.
   - Ensure each Event Hub is set up within the same region for optimal performance.

2. **Partition Data Streams**: 
   - Implement a partitioning strategy based on specific criteria such as device ID, region, or data type.
   - Use Azure Functions or custom code to partition data streams dynamically.

3. **Configure Data Sources**: 
   - Update your data sources to send data to the appropriate Event Hub based on the partitioning strategy.
   - Ensure data sources are configured to handle failover scenarios, redirecting data to other Event Hubs if one becomes unavailable.

</details>

<details>
<summary>3. Using Event Hub Namespaces</summary>

> Manage multiple Event Hubs under a single namespace, providing a unified management experience.

- **Namespace Configuration**:
  - Use the Azure portal or Azure CLI to create and configure the namespace.
  - Define Event Hubs within the namespace with specific throughput and retention settings.
- **Data Source Configuration**:
  - Use SDKs or APIs to configure data sources to send data to specific Event Hubs within the namespace.
  - Implement retry logic to handle failover scenarios.

**Steps**:
1. **Create an Event Hub Namespace**: 
   - Navigate to the Azure portal.
   - Create an Event Hub namespace in Azure.
   - Ensure the namespace is set up within the same region for optimal performance.

2. **Create Multiple Event Hubs**: 
   - Within the namespace, create multiple Event Hubs, each with a portion of the required TUs.
   - Configure each Event Hub with appropriate settings for throughput and retention.

3. **Configure Data Sources**: 
   - Update your data sources to send data to the appropriate Event Hub within the namespace.
   - Ensure data sources are configured to handle failover scenarios, redirecting data to other Event Hubs if one becomes unavailable.

</details>

<details>
<summary>4. Using Azure Stream Analytics</summary>

> Process and route data streams to multiple Event Hubs using Azure Stream Analytics.

- **Stream Analytics Job Configuration**:
  - Use the Azure portal or Azure CLI to create and configure the Stream Analytics job.
  - Define inputs and outputs with specific settings for data ingestion and routing.
- **Query Definition**:
  - Use SQL-like syntax to write queries for data routing.
  - Implement logic to route data based on device ID, region, or other criteria.

**Steps**:
1. **Create Stream Analytics Job**: 
   - Navigate to the Azure portal.
   - Create a Stream Analytics job in Azure.
   - Configure the job with appropriate settings for input and output.

2. **Configure Inputs**: 
   - Define inputs to receive data from your data sources.
   - Configure input settings to handle data ingestion and processing.

3. **Configure Outputs**: 
   - Define outputs to send data to multiple Event Hubs.
   - Configure output settings to handle data routing and distribution.

4. **Define Query**: 
   - Write a query to route data to the appropriate Event Hub based on specific criteria.
   - Test and validate the query to ensure accurate data routing.

</details>

<details>
<summary>5. Using Azure Data Factory</summary>

> Orchestrate and manage data flows between multiple Event Hubs using Azure Data Factory.

- **Data Factory Configuration**:
  - Use the Azure portal or Azure CLI to create and configure the Data Factory instance.
  - Define pipelines with specific settings for data orchestration.
- **Pipeline Definition**:
  - Use visual tools or code to define pipelines for data ingestion, transformation, and routing.
  - Implement logic to route data to specific Event Hubs based on criteria.

**Steps**:
1. **Create Data Factory**: 
   - Navigate to the Azure portal.
   - Create an Azure Data Factory instance.
   - Configure the instance with appropriate settings for data orchestration.

2. **Create Pipelines**: 
   - Define pipelines to manage data flows between data sources and Event Hubs.
   - Configure pipeline settings to handle data ingestion, transformation, and routing.

3. **Configure Data Sources**: 
   - Update your data sources to send data to the Data Factory.
   - Configure data source settings to handle data ingestion and processing.

4. **Configure Event Hubs**: 
   - Define Event Hubs as destinations within the Data Factory pipelines.
   - Configure Event Hub settings to handle data routing and distribution.

</details>

<details>
<summary>6. Using Event Hubs Dedicated Clusters</summary>

> Provision a single-tenant cluster with high capacity and low latency.

- **Dedicated Cluster Configuration**:
  - Use the Azure portal or Azure CLI to create and configure the dedicated cluster.
  - Define namespaces and Event Hubs within the cluster with specific settings for throughput and retention.
- **Data Distribution**:
  - Use partitioning or load balancing algorithms to distribute data evenly across Event Hubs.
  - Implement retry logic to handle failover scenarios and ensure data availability.

**Steps**:
1. **Create an Event Hubs Dedicated Cluster**: 
   - Navigate to the Azure portal.
   - Create a dedicated cluster with the required capacity units (CUs).
   - Configure the cluster with appropriate settings for throughput and latency.

2. **Create Namespaces and Event Hubs**: 
   - Within the dedicated cluster, create namespaces and Event Hubs.
   - Configure each Event Hub with appropriate settings for throughput and retention.

3. **Distribute Data**: 
   - Use partitioning or load balancing to distribute the data evenly across the Event Hubs within the cluster.
   - Implement logic to handle failover scenarios and ensure data availability.

</details>

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->

