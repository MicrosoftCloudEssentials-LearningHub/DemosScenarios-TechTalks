# How ACA + Artemis Work Together - Overview 

> Big picture summary so you can see how Azure Container Apps (ACA) fits with ActiveMQ Artemis for a broker + quorum voter setup.

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-10-23

----------

> Big picture: `ActiveMQ Artemis provides the messaging and HA logic; Azure Container Apps provides the resilient execution platform`
> - `Artemis` is the brain: `It knows how to broker messages, enforce HA, and use voters to stay consistent.`
> - `ACA` is the body: `It runs those brokers and voters in a resilient, elastic, cloud‑native environment.`
> - Together: `You get a geo‑redundant, fault‑tolerant messaging backbone where failover is decided by quorum voters, and ACA ensures the containers are always healthy, distributed, and secure.`

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Use a split-brain DNS configuration to host a web app in Azure](https://learn.microsoft.com/en-us/azure/architecture/example-scenario/networking/split-brain-dns)
- [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)
- [What is infrastructure as code (IaC)?](https://learn.microsoft.com/en-us/devops/deliver/what-is-infrastructure-as-code)
- [CI/CD baseline architecture with Azure Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/architectures/devops-pipelines-baseline-architecture?view=azure-devops)

    <img width="1155" height="414" alt="image" src="https://github.com/user-attachments/assets/67cc7bd5-4cee-45b3-aaa3-64fad2de90cf" />

</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>


</details>

`Artemis is infrastructure, not a coding framework. You code against its APIs, but the broker itself runs as a service.`

- You **run Artemis brokers** in Azure Container Apps, and if neeeded you can add other data centers.  
- Your **application code** connects to these brokers using JMS/AMQP/etc.  
- **Quorum voters** (also running in Azure or other sites) decide which broker should be live during failures.  
- Your app doesn’t need to know which broker is live, the client libraries handle failover automatically if configured correctly.


## Overview

1. ActiveMQ Artemis role: 
    - Broker = messaging server: `Receives, stores, and forwards messages between producers and consumers.`
    - HA model: `Brokers run in live/backup pairs, with quorum voters deciding who is live to prevent split‑brain.`
    - Cluster option: `Multiple brokers can form a cluster for load balancing and redundancy.`
2. Quorum voters:
    - Purpose: `Independent processes that arbitrate failover decisions.`
    - Placement: Spread across multiple data centers and Azure regions to `ensure no single site controls majority.`
    - Outcome: `Only one broker is promoted to live at a time, preserving consistency.`
3. Azure Container Apps role:
    - Execution environment: Runs brokers and voters as `containers without needing to manage VMs or Kubernetes.`
    - Resiliency: `Provides zone and region fault tolerance, automatic restarts, and scaling.`
    - Networking: `VNET integration and private endpoints secure broker‑to‑broker and voter communication.`
    - Operations: Readiness/liveness probes, autoscaling, and revision rollouts align with Artemis HA needs.

> How ACA + Artemis Work Together?

| Layer | What Artemis Provides | What ACA Provides |
|-------|-----------------------|-------------------|
| **Messaging logic** | Brokers handle queues, topics, persistence, clustering | Container runtime for brokers, scaling, probes |
| **HA control** | Quorum voters prevent split‑brain, elect live broker | Geographic distribution, independent failure domains |
| **Durability** | Journals, replication/shared store | Restart/recovery orchestration, resource isolation |
| **Security** | TLS, auth, role‑based access | VNET, private DNS, NSGs, managed identity |
| **Operations** | Failover, fencing, client reconnect | Autoscaling, observability, revision rollouts |

## How Artemis work?

`It’s open source, part of the Apache ActiveMQ project.`

> - **ActiveMQ Artemis is a *message broker server***, a runtime process that applications connect to. `You don’t “embed” it into your code (unless you choose the embedded mode); instead, you run Artemis as a service** (like a database or Kafka), and your application talks to it using APIs or protocols.`
> - Your application code uses a **client library** (for example, JMS in Java, AMQP in many languages, or MQTT for IoT). `In code, you configure a connection** to the broker (hostname, port, protocol).`Then you **send messages** (producer) or **receive messages** (consumer).  

Example in Java (simplified): Broker is the server that receives and routes the message `"Order #123"`.

```java
ConnectionFactory cf = new ActiveMQConnectionFactory("tcp://broker-host:61616");
Connection connection = cf.createConnection();
Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
Queue queue = session.createQueue("orders");
MessageProducer producer = session.createProducer(queue);
producer.send(session.createTextMessage("Order #123"));
```

- In Artemis HA setups, you have **instances** (brokers).  
- One broker is **live** (active, serving clients).  
- Another broker is **backup** (standby, waiting).  
- If the live broker fails, the backup can become live, but only if **quorum voters** agree.  
- This ensures only one broker is live at a time `(avoiding split‑brain).`

> [!NOTE]
> `Split-brain`:
> - In computing, it describes a `situation where two separate data sets are maintained with overlapping scope, leading to inconsistencies due to network partitions or failure conditions.`
> - In distributed systems, it `indicates a scenario where nodes in a cluster lose communication, leading to conflicting data handling and potential data inconsistencies`

## Best Practices for ActiveMQ Artemis on Azure Container Apps



<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
