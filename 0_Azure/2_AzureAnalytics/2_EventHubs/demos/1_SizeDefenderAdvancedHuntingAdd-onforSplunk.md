# Event Hub Sizing for Microsoft Defender Advanced Hunting Add-on for Splunk - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-25

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
  
</details>

> [!TIP]
> Sysmon (System Monitor) is a Windows system service and device driver that monitors and logs system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time.

## Content 

- [Overview](#overview)
- [Event Hub Sizing](#event-hub-sizing)
    - [Step 1: Determine Ingress Data Rate](#step-1-determine-ingress-data-rate)
    - [Step 2: Calculate Throughput Units TUs](#step-2-calculate-throughput-units-tus)
    - [Step 3: Monitor and Adjust](#step-3-monitor-and-adjust)
    - [Example Calculation](#example-calculation)
- [Installation Steps](#installation-steps)

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
    <td>Provides higher throughput and additional features such as Capture, which allows you to automatically capture streaming data. Option available for `Auto-Inflate: automatically scales the number of Throughput Units assigned to your Standard Tier Event Hubs Namespace when your traffic exceeds the capacity of the Throughput Units assigned to it. You can specify a limit to which the Namespace will automatically scale.`</td>
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

### Example Calculation

> Assume we have 200 endpoints, each sending 0.25 MB of data per second and generating 2 events per second.

1. **Total Ingress Data Rate**:

$$
\text{Total Ingress MB/s} = \text{Number of Endpoints} * \text{Data Volume per Endpoint (MB/s)}
$$
      
$$
\text{Total Ingress MB/s} = 200 \text{ endpoints} * 0.25 \text{ MB/s per endpoint} = 50 \text{ MB/s}
$$

2. **Total Event Rate**:

$$
\text{Total Events/second} = \text{Number of Endpoints} \times \text{Event Rate per Endpoint (events/second)}
$$

$$
\text{Total Events/second} = 200 \text{ endpoints} \times 2 \text{ events/second per endpoint} = 400 \text{ events/second}
$$

3. **Calculate Required TUs**:

   - Required TUs for MB/s:

$$
\text{Required TUs for MB/s} = \frac{\text{Total Ingress MB/s}}{1 \text{ MB/s per TU}}
$$

$$
\text{Required TUs for MB/s} = \frac{50 \text{ MB/s}}{1 \text{ MB/s per TU}} = 50 \text{ TUs}
$$

   - Required TUs for Events/second:

$$
\text{Required TUs for Events/second} = \frac{\text{Total Events/second}}{1000 \text{ events/second per TU}}
$$

$$
\text{Required TUs for Events/second} = \frac{400 \text{ events/second}}{1000 \text{ events/second per TU}} = 0.4 \text{ TUs}
$$

4. **Determine the Maximum Value**:

$$
\text{Required TUs} = \max \left( \frac{\text{Total Ingress MB/s}}{1}, \frac{\text{Total Events/second}}{1000} \right)
$$

$$
\text{Required TUs} = \max(50, 0.4) = 50 \text{ TUs}
$$

| **Step**          | **Action**                                                                                     | **Example**                                                                 | **Metric**        | **Value**             | **Formula** |
|-------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|-------------------|-----------------------|-------------|
| **Data Sources**  | Identify all devices and systems that will provide telemetry data.                            | Endpoints, servers, network devices, applications.                          | **Number of Sources** | Endpoints: 200, Servers: 50 | N/A         |
| **Data Volume**   | Calculate the average amount of data generated by each source per second.                     | Endpoint generates 0.25 MB/s, server generates 1 MB/s.                      | **Total Data Volume (MB/s)** | Endpoints: 50, Servers: 50 | Number of Sources * Data Volume per Source |
| **Event Rate**    | Determine the frequency of events generated by each source per second.                        | Endpoint generates 2 events/s, server generates 5 events/s.                 | **Total Event Rate (events/s)** | Endpoints: 400, Servers: 250 | Number of Sources * Event Rate per Source |
| **Required TUs**  | Calculate the required Throughput Units based on data volume and event rate.                  | Total Ingress MB/s = 50, Total Events/second = 400                          | **Required TUs** | 50 | Max value between the two: 50/1 = (50) or 400/1000 = (0.4) |

## Installation Steps

| **Step** | **Action** | **Details** | **Example/Command** |
|----------|-------------|-------------|---------------------|
| **1. Configure Microsoft Defender for Endpoint** | Stream Advanced Hunting events to an Azure Event Hub | - Create an Azure Event Hub namespace and Event Hub. <br> - Configure Microsoft Defender for Endpoint to stream events to the Event Hub. <br> - Ensure necessary permissions are granted. | - Azure Portal: Create Event Hub <br> - Defender Security Center: Enable Streaming API |
| **2. Install the Add-on** | Install the Add-on on your Search Heads, Indexers, and Heavy Forwarders | - Download the Microsoft Defender Advanced Hunting Add-on for Splunk from Splunkbase. <br> - Install the add-on on all relevant Splunk components (Search Heads, Indexers, Heavy Forwarders). <br> - Configure the add-on as per your environment requirements. | - Splunkbase: Download Add-on <br> - Splunk UI: Apps > Manage Apps > Install app from file |
| **3. Set up the Input** | Set up the Input in the Splunk Add-on for Microsoft Cloud Services | - Navigate to the Splunk Add-on for Microsoft Cloud Services configuration page. <br> - Add a new input for Azure Event Hub. <br> - Set the Sourcetype to `mscs:azure:eventhub:defender:advancedhunting`. <br> - Provide the connection string for the Azure Event Hub. <br> - Configure other parameters such as index, interval, and format. | - Splunk UI: Settings > Data Inputs > Azure Event Hub <br> - Sourcetype: `mscs:azure:eventhub:defender:advancedhunting` |
| **4. Verify Data Arrival** | Run a search to verify data arrival | - Open the Splunk Search & Reporting app. <br> - Run the search query to verify that data is being ingested correctly. | `index=* eventtype="ms_defender_advanced_hunting_sourcetypes"` |
| **5. Enable Scheduled Saved Searches** | Enable Scheduled Saved Searches for Malware and Email data models | - Navigate to Saved Searches in Splunk. <br> - Create new saved searches for malware and email data models. <br> - Schedule the searches to run at regular intervals (e.g., every hour). <br> - Configure alert actions if needed. <br> - Verify data generation by running the saved searches manually. | - Splunk UI: Settings > Searches, Reports, and Alerts <br> - Example search queries: <br> `index=* sourcetype="defender:advancedhunting:malware"` <br> `index=* sourcetype="defender:advancedhunting:email"` |

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

