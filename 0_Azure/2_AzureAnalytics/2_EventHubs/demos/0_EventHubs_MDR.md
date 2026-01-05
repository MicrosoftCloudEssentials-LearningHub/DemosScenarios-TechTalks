# Event Hubs & Managed Detection and Response (MDR)

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [What Is MDR? Managed Detection and Response](https://www.microsoft.com/en-us/security/business/security-101/what-is-mdr-managed-detection-response)
- [What is Event Hubs](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-about)
- [Event Hubs pricing](https://azure.microsoft.com/en-us/pricing/details/event-hubs/)
- [Event Hubs price calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)
- [Event Hubs tiers - Features](https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers#features)
- [Events Hubs tiers - Quota](https://learn.microsoft.com/en-us/azure/event-hubs/compare-tiers#quotas)
- [Monitor Azure resources with Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/monitor-azure-resource)
- [Collect and analyze resource logs from an Azure resource](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/tutorial-resource-logs)
- [Step-by-Step: Finding and Analyzing Microsoft Azure Cloud Usage Costs](https://techcommunity.microsoft.com/t5/finops-blog/step-by-step-finding-and-analyzing-microsoft-azure-cloud-usage/ba-p/718890)

</details>

## MDR 

> `Managed Detection and Response (MDR)` is a cybersecurity service that combines advanced technology with human expertise to `detect, monitor, and respond to cyber threats in real-time`.

Some key aspects of MDR:

| **Service**                    | **Description**                                                                                       |
|--------------------------------|-------------------------------------------------------------------------------------------------------|
| Threat Detection and Monitoring| MDR services continuously monitor your organization's network for suspicious activities and potential threats |
| Threat Hunting                 | Security experts proactively search for hidden threats that automated systems might miss              |
| Incident Response              | When a threat is detected, MDR providers quickly respond to contain and mitigate the impact           |
| Expert Analysis                | Human analysts review and prioritize alerts to ensure that significant threats are addressed promptly |
| Reporting and Recommendations  | Regular reports and security health checks help organizations understand their security posture and improve their defenses |

## Overview

| **Aspect**          | **Event Hubs**                                                                 | **Log Analytics**                                                                                   |
|---------------------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Service Focus**   | Event streaming and real-time data processing                                 | Log collection, analysis, and security monitoring                                                   |
| **Setup Complexity**| Involves more steps related to event ingestion and processing                 | Focuses on log collection and integration with security solutions                                   |
| **End Goals**       | Handles large-scale event data streams                                        | Provides insights and security monitoring through log data                                          |

Key benefits:

| **Benefit**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| Rapid Threat Detection and Response | Significantly reduces the time to detect and respond to threats.               |
| 24/7 Monitoring                 | Ensures continuous monitoring for suspicious activities.                        |
| Expertise and Advanced Technology | Combines cutting-edge technology with human expertise for advanced threat handling. |
| Cost-Effective                  | Avoids the high costs of building and maintaining an in-house SOC (Security Operations Center).              |
| Improved Security Posture       | Regular health checks and reports to enhance defenses.                         |
| Focus on Core Business          | Allows internal teams to focus on strategic projects.                          |
| Compliance and Reporting        | Provides detailed reporting and compliance support.                            |

## Licensing Options 

| **Service**                | **Option**            | **Description**                                                                 |
|----------------------------|-----------------------|---------------------------------------------------------------------------------|
| Log Analytics Workspace    | Pay-As-You-Go         | Charges based on data volume ingested and retained. Default retention is 90 days, extendable up to 730 days. |
|                            | Commitment Tiers      | Discount on data ingestion costs by committing to a specific amount of data per day. |
| Azure Event Hubs           | Basic, Standard, Premium, Dedicated Tiers | Costs depend on the number of throughput units (TUs), processing units (PUs), or capacity units (CUs) provisioned. Additional costs for data capture and transfer. |
| Azure Storage              | Standard Storage Costs | Charges based on the amount of data stored and the duration of storage.          |

> Azure Event Hubs Options:

| Resource Type     | Billing Basis          | Description                                                                 |
|-------------------|------------------------|-----------------------------------------------------------------------------|
| Throughput Units  | Hourly per TU          | Billed based on the number of TUs provisioned                               |
| Processing Units  | Hourly per PU          | Billed based on the number of PUs provisioned (Premium tier)                |
| Capacity Units    | Hourly per CU          | Billed based on the number of CUs provisioned (Dedicated tier)              |
| Capture           | Additional storage cost| Costs for storing data in Azure Blob Storage or Azure Data Lake             |
| Data Transfer     | Standard rates apply   | Costs for data moving in and out of Event Hubs                              |

## Costs 

| **Category**     | **Description**                                                                 | **Example Cost**                       |
|------------------|---------------------------------------------------------------------------------|----------------------------------------|
| Log Analytics    | Data ingestion is typically charged per GB.                                     | Around $2.76 per GB ingested.     |
| Storage          | Standard storage costs apply.                                                   | Around $0.0184 per GB per month.  |
| Activity Logs    | Sending activity logs to a Log Analytics workspace is free for the default retention period. | Free.                             |

> Event Hubs: Costs vary based on the number of throughput units and the amount of data processed. Around $0.028 per million events.

| Tier      | Cost per Hour          | Features                                                                 |
|-----------|------------------------|--------------------------------------------------------------------------|
| Basic     | $0.015 per TU          | Suitable for small-scale applications with basic event streaming needs   |
| Standard  | $0.03 per TU           | Includes Capture feature for saving data to Azure Blob Storage or Data Lake |
| Premium   | $1.233 per PU          | Enhanced performance, resource isolation, extended retention periods     |
| Dedicated | $6.849 per CU          | Exclusive single-tenant deployment for large-scale, mission-critical applications |

## Estimating the amount of data and events generated by Azure resources

1. **Create a Log Analytics Workspace**:
   - Go to the Azure portal.
   - In the left-hand menu, select `Log Analytics workspaces`.
   - Click on `Add` to create a new workspace.
   - Fill in the required details:
     - **Subscription**: Select your Azure subscription.
     - **Resource Group**: Choose an existing resource group or create a new one.
     - **Name**: Enter a unique name for your workspace.
     - **Region**: Select the region where you want to create the workspace.
   - Click `Review + create`, then `Create` to finalize the creation of the workspace.
2. **Configure Diagnostic Settings**:
   - Navigate to the Azure resource you want to monitor (e.g., Virtual Machine, Storage Account).
   - In the resource's menu, select `Diagnostic settings` under the **Monitoring** section.
   - Click on `Add diagnostic setting`.
   - Provide a name for the diagnostic setting.
   - Choose the logs and metrics you want to collect. You can select from options like **AuditLogs**, **PerformanceCounters**, **Metrics**, etc.
   - Select the destination for the collected data:
     - **Log Analytics workspace**: Choose the workspace you created earlier.
     - **Event Hubs**: If you want to stream the data to Event Hubs.
     - **Storage Account**: For long-term storage in Azure Storage.
   - Click `Save` to apply the diagnostic settings.
3. **Analyze Historical Data**:
   - Go to your **Log Analytics workspace** in the Azure portal.
   - Use **Log Analytics** to run queries on the collected data. You can use the **Kusto Query Language (KQL)** to filter and analyze the data.
   - Review the data to understand usage patterns, peak loads, and other relevant metrics. This will help you estimate future data and event volumes.
4. **Use Azure Cost Management**:
   - Navigate to **Azure Cost Management + Billing** in the Azure portal.
   - Use the **Cost analysis** tool to review your resource usage and costs.
   - Set up **budgets** and **alerts** to monitor and control your spending.
   - Analyze the cost data to identify which resources and activities contribute most to your monthly Azure bill. This can help you optimize your resource usage and reduce costs.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/49f6bddf-3ac1-44fc-88c0-5e847ca05531">

## Setting up Azure Event Hubs 

> Is a big data streaming platform and event ingestion service. It can receive and process millions of events per second.
> - Real-time data ingestion and processing. <br/>
> - Streaming analytics.  <br/>
> - Telemetry data collection from IoT devices.

> Involves creating an Event Hubs namespace and an event hub within that namespace. 

- Step 1: Create an Event Hubs Namespace
    1. **Sign in to Azure Portal**: Go to the Azure portal.
    2. **Create a Resource Group**:
        - In the left-hand menu, select `Resource groups`.
        - Click `Create` and fill in the required details like Subscription, Resource Group Name, and Region.
        - Click `Review + Create` and then `Create`.
    3. **Create Namespace**:
        - In the left-hand menu, select `All services` and then `Event Hubs`.
        - Click `Create` on the Event Hubs page.
        - Fill in the required details:
            - **Subscription**: Select your subscription.
            - **Resource Group**: Select the resource group you created.
            - **Namespace Name**: Enter a unique name for your namespace.
            - **Location**: Choose a region.
            - **Pricing Tier**: Choose between Basic, Standard, or Dedicated based on your needs.
        - Click `Review + Create` and then `Create`.
- Step 2: Create an Event Hub
    1. **Navigate to Event Hubs Namespace**:
        - In the Azure portal, go to your Event Hubs namespace.
        - Under `Entities`, select `Event Hubs`.
        - Click `Create` to create a new event hub.
    2. **Configure Event Hub**:
        - **Name**: Enter a name for your event hub.
        - **Partition Count**: Choose the number of partitions (default is 4).
        - **Message Retention**: Set the message retention period (default is 1 day).
        - **Capture**: Optionally, enable capture to store event data in Azure Blob Storage or Azure Data Lake.
        - Click `Create`.
- Step 3: Configure Security and Access
    1. **Shared Access Policies**:
        - In your Event Hubs namespace, go to `Shared access policies`.
        - Click `Add` to create a new policy.
        - Enter a name for the policy and select the appropriate permissions (e.g., Send, Listen, Manage).
        - Click `Create`.
    2. **Connection Strings**:
        - After creating the shared access policy, click on it to view the connection strings.
        - Copy the connection string for use in your applications.
- Step 4: Verify and Test
    1. **Send Events**:
        - Use the connection string to configure your application to send events to the event hub.
        - You can use SDKs like Azure SDK for .NET, Java, Python, etc., to send events.
    2. **Monitor and Analyze**:
        - In the Azure portal, go to your event hub and click on `Metrics` to monitor incoming events and throughput.
        - Use Azure Stream Analytics, Azure Functions, or other services to process and analyze the event data.

## Setting Up Azure Activity Logs to an MDR Solution

> Collect and analyze logs, and then forwarding these logs to a Managed Detection and Response (MDR) solution for security monitoring and incident response.
> - Security monitoring and incident response.  <br/>
> - Compliance and auditing.  <br/>
> - Operational monitoring and troubleshooting.

- Step 1: Create a Log Analytics Workspace
    1. **Navigate to Azure Portal**: Go to the Azure portal and search for `Log Analytics workspaces`.
    2. **Create Workspace**: Click on `Create` and fill in the required details like Subscription, Resource Group, and Workspace Name.
    3. **Review and Create**: Review the details and click `Create`.
- Step 2: Configure Diagnostic Settings
    1. **Navigate to Azure Monitor**: In the Azure portal, search for `Azure Monitor`.
    2. **Diagnostic Settings**: Under `Settings`, click on `Diagnostic settings`.
    3. **Add Diagnostic Setting**: Click on `Add diagnostic setting`.
    4. **Select Logs**: Choose the logs you want to send (e.g., Activity Logs).
    5. **Select Destination**: Choose `Send to Log Analytics workspace` and select the workspace you created.
    6. **Save**: Click `Save` to apply the settings.
- Step 3: Verify Data Ingestion
    1. **Navigate to Log Analytics Workspace**: Go to the Log Analytics workspace you created.
    2. **Logs**: Click on `Logs` under `General`.
    3. **Run Query**: Use Kusto Query Language (KQL) to query the logs and verify that data is being ingested.
- Step 4: Forward Logs to MDR Solution
    1. **Set Up Integration**: Follow the specific instructions provided by your MDR solution to integrate with Azure Log Analytics. This often involves setting up API connections or using built-in connectors.
    2. **Configure Alerts and Actions**: Set up alerts and automated actions within your MDR solution to respond to specific log events.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1497-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-05</p>
</div>
<!-- END BADGE -->
