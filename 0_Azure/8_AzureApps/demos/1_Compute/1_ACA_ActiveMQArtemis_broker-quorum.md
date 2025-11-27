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
    
- [Overview](#overview)
- [How Artemis work?](#how-artemis-work)
- [Best Practices for ActiveMQ Artemis on Azure Container Apps](#best-practices-for-activemq-artemis-on-azure-container-apps)
- [Q&A sample](#qa-sample)

</details>

`Artemis is infrastructure, not a coding framework. You code against its APIs, but the broker itself runs as a service.`

- You **run Artemis brokers** in Azure Container Apps, and if neeeded you can add other data centers.  
- Your **application code** connects to these brokers using JMS/AMQP/etc.  
- **Quorum voters** (also running in Azure or other sites) decide which broker should be live during failures.  
- Your app doesn’t need to know which broker is live, the client libraries handle failover automatically if configured correctly.

<img width="1600" height="917" alt="image" src="https://github.com/user-attachments/assets/d8fb6d24-429c-4199-a18a-2c737f330d9c" />

From [Azure Container Apps overview](https://learn.microsoft.com/en-us/azure/container-apps/overview)

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

1. **Failure-domain design**
      - **Odd number of voters:** Always deploy 3, 5, or 7 voters. This ensures a clear majority and avoids ties.  
      - **Geographic distribution:** Place voters in different Azure regions and on-prem data centers. No single site should hold majority control.  
      - **Zone awareness:** Brokers should be spread across availability zones to survive zone-level outages.  
      - **Partition testing:** Simulate network partitions to confirm only one broker becomes live.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Odd-number quorum:**  Use 3 or 5 quorum voters, never 2 or 4. Place at least one voter outside each broker’s region so no single site can form a majority alone. Test loss of any single site and confirm quorum still forms. `A majority requires a clear winner. With an odd count, you never get ties, so elections can complete deterministically under partial failures.`
      - **Prevents:** Stalled elections, split-brain caused by ambiguous quorum.  
      - **Evidence:** In a 3-voter setup, any single voter loss still yields a majority. In chaos tests, promotions still occur within expected time.
- **Independent failure domains:** Map each broker and voter to distinct availability zones or regions. Avoid co‑locating a broker with a majority of voters. Document the “who can fail” matrix so one outage cannot elect two lives. `Co-locating voters and brokers in the same zone couples their fate; one outage eliminates both capacity and control. Spreading voters/brokers keeps control available when capacity isn’t.`
      - **Prevents:** A single-zone outage taking down both messaging and the control plane that decides promotions.  
      - **Evidence:** Zone failure leaves at least one live broker candidate and a majority of reachable voters.
- **Network partition planning:**  Assume partial partitions. Define which segments can still communicate (brokers↔voters). Prefer cross-region voter placement with dedicated, monitored links. `Real failures are often partial: one site can reach voters, another can’t. Planning for asymmetric reachability ensures only the segment with majority acts.`
      - **Prevents:** Two live brokers accepting writes on divergent partitions.  
      - **Evidence:** Inject partial packet loss; only the segment with voter majority promotes.
- **Power and maintenance windows:** Stagger maintenance windows across sites. Ensure quorum persists during planned downtime and autoscaling events. `Planned downtime can accidentally erode quorum. Staggering keeps the decision-making plane intact while you service capacity.`
      - **Prevents:** Self-inflicted quorum loss during routine operations.  
      - **Evidence:** During patch windows, voters remain ≥ majority; brokers continue serving or cleanly fail over.

</details>

2. **HA and split-brain prevention**
      - **Clear live/backup roles:** Explicitly configure brokers as live or backup in `broker.xml`.  
      - **Timeout tuning:** Set election timeouts based on measured cross-region latency (2–3× p95).  
      - **Fencing:** Ensure failed brokers disable acceptors and stop writing journals to prevent dual writers.  
      - **Chaos drills:** Test asymmetric failures (e.g., one broker loses voters) to validate quorum logic.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Explicit roles:** Configure clear live/backup roles (replication or shared-store) and validate the backup never becomes live without quorum. Keep role state in configuration management to prevent drift. `Ambiguous role state is fertile ground for dual-writes. Declaring live/backup roles and enforcing them via voters creates a single-writer guarantee.`
      - **Prevents:** Two brokers acting as live due to config drift or race conditions.  
      - **Evidence:** Startup logs show one live, one backup; backup refuses promotion without quorum.
- **Timeout tuning:** Set election and failure-detection timeouts above your 95th percentile cross-region latency. Add jitter to retries to avoid synchronized flaps. Start conservative, then reduce based on measurements. `Latency spikes can look like failures. Timeouts aligned to cross-region latency ensure you don’t promote during transient slowness. Jitter avoids herd effects.`
      - **Prevents:** Flapping promotions and rapid role oscillations under short-lived network jitter.  
      - **Evidence:** Promotions occur only after sustained unreachability; no oscillations in election logs.
- **Fencing actions:** Define and test fencing: disable acceptors, pause journal writes, or cordon the isolated node. The failed or partitioned broker must not accept client connections until quorum restores. `When a node is suspected failed, you must guarantee it cannot continue accepting traffic or writing storage. Fencing makes failure “safe.”`
      - **Prevents:** Data corruption from “zombie” brokers writing after a backup is promoted.  
      - **Evidence:** Isolated broker disables acceptors and journal writes until quorum restores.
- **Single source of truth:**  Ensure only one broker is allowed to write the journal at any time. If using shared storage, enable lock/fencing mechanisms; if replication, verify backup promotion cancels the old live. `Storage consistency depends on exactly one writer. Replication or shared-store must enforce a hard lock or promotion cancelation.`
      - **Prevents:** Divergent journals, irreconcilable message state.  
      - **Evidence:** After failover, old live cannot rejoin as live without explicit demotion; storage lock is exclusive.
- **Chaos tests:**  Induce packet loss and asymmetric partitions to verify the backup stays passive without quorum and the live recovers cleanly. `Assumptions fail in production. Chaos reveals hidden coupling and timing bugs before users do.`
      - **Prevents:** Unknown failure modes surfacing under real incidents.  
      - **Evidence:** Documented test runs for packet loss, asymmetric partitions, and broker crashes with predictable outcomes.

</details>

3. **Persistence and durability**
      - **Journal configuration:** Size journal files for peak throughput; choose sync vs async writes based on RPO.  
      - **Paging thresholds:** Configure queue limits and paging to prevent memory exhaustion during consumer lag.  
      - **Replication vs shared-store:** Document your choice. Replication is simpler but heavier on bandwidth; shared-store requires strict fencing.  
      - **Recovery validation:** Measure broker startup and journal recovery time; align readiness probes accordingly.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Journal configuration:** Choose sync writes for strict durability guarantees; async for higher throughput with small risk windows during crashes. Use AIO/NIO tuned to disk characteristics; allocate direct I/O if supported. Size journal files and compaction thresholds for 2–3× peak throughput to handle bursts. `Sync writes guarantee every message hits disk before acknowledgment, eliminating RPO at the cost of latency. Async trades small loss windows for speed. Right-sizing prevents I/O saturation during spikes.`
   - **Prevents:** Message loss during crashes (sync) or I/O bottlenecks during peak load.  
   - **Evidence:** Zero unacknowledged message loss with sync; consistent sub-millisecond fsync latencies; no I/O wait spikes in metrics.

- **Paging thresholds:** Set address/queue size limits and paging thresholds to prevent memory exhaustion. Monitor page-in/out rates and back-pressure producers when consumers lag. Configure max-size-bytes and page-size-bytes based on available heap and expected message volume. `Unbounded queues exhaust memory when consumers slow down. Paging spills to disk gracefully; flow control stops producers before OOM kills the broker.`
   - **Prevents:** Out-of-memory crashes during consumer lag or traffic surges.  
   - **Evidence:** Stable heap usage under load; paging triggered predictably; producers receive flow-control signals before memory exhaustion.

- **Replication vs shared-store:** Replication offers lower RPO, simpler fencing, and more network bandwidth usage. Shared-store requires robust storage locks and fencing to prevent dual writers. Document your choice, expected RPO/RTO, and validate with failover drills. `Replication keeps journals independent and promotes faster; shared-store centralizes state but needs perfect lock discipline. Each fits different latency/consistency tradeoffs.`
   - **Prevents:** Mismatched expectations for recovery time and data loss; storage corruption from dual writes.  
   - **Evidence:** Documented architecture decision; measured RTO/RPO; successful failover tests showing clean promotions and no journal conflicts.

- **Recovery validation:** Measure startup and journal recovery time under realistic data volumes. Align readiness probes to avoid routing traffic before the broker is truly ready. Verify message integrity and ordering after crash/restart and post-failover. `A broker that reports "ready" while still replaying journals will drop or duplicate messages. Probes must wait for full initialization.`
   - **Prevents:** Premature traffic routing causing failed deliveries or duplicate processing.  
   - **Evidence:** Readiness probe delays match measured recovery time; no message loss or duplication detected in post-recovery audits.

</details>


4. **Networking and security**
      - **Mutual TLS:** Require mTLS between brokers, voters, and clients. Rotate certs regularly.  
      - **Private networking:** Use VNET integration and private DNS; avoid exposing broker control traffic publicly.  
      - **Least privilege:** Apply role-based access per queue/topic; restrict admin endpoints.  
      - **Health endpoint hygiene:** Protect liveness/readiness probes; avoid leaking broker state externally.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Mutual TLS:** Enable mTLS between brokers, voters, and clients to authenticate both ends and block rogue connections. Rotate certificates automatically (e.g., every 90 days), pin CA certificates, and disable legacy ciphers. Enforce TLS 1.2+ and perfect forward secrecy. `Authentication at both ends blocks rogue brokers/clients and man-in-the-middle attacks. Certificate rotation ensures long-term hygiene and limits exposure from compromised keys.`
   - **Prevents:** Unauthorized access, traffic interception, impersonation, and credential replay.  
   - **Evidence:** Certificate pinning logs; CA rotations tracked; rejected connection attempts from unknown identities; no weak cipher usage in TLS handshakes.

- **Private networking:** Use VNET integration and private DNS for broker-to-broker and voter traffic. Block public ingress for control channels and restrict egress to necessary destinations only. Control traffic should never traverse the public internet to reduce attack surface and network jitter. `Exposing election and replication channels to hostile networks invites DoS and eavesdropping. Private paths are faster and safer.`
   - **Prevents:** Exposure of election and replication channels to external attacks; latency variability from internet routing.  
   - **Evidence:** No public endpoints for broker-to-broker/voter links; network security groups enforce minimal egress; DNS resolution stays internal.

- **Least privilege:** Scope network security groups and firewall rules tightly. Segment broker admin endpoints from data paths. Use role-based authentication and per-queue/topic permissions. Apply role-based access control with per-queue scopes; restrict who can access admin interfaces. `Over-broad permissions turn minor misconfigurations into major breaches. Tight scopes limit blast radius.`
   - **Prevents:** Lateral movement, accidental access to admin interfaces, queue misuse, and privilege escalation.  
   - **Evidence:** Role-based policies enforce per-queue scopes; audit logs show denied attempts to access unauthorized queues or admin endpoints.

- **Health endpoint hygiene:** Protect liveness/readiness endpoints to prevent external manipulation or information disclosure. Avoid exposing broker management interfaces publicly. Monitor endpoints but don't let unauthenticated probes leak internal state. Gate and authenticate health checks where possible; rate-limit them. `Health probes can leak state (queue depths, connection counts) and be abused to trigger false failovers or gather reconnaissance data.`
   - **Prevents:** External manipulation of failover signals, information disclosure, and DoS via probe abuse.  
   - **Evidence:** Authentication required for detailed health checks; rate-limiting enforced; health endpoints accessible only from internal monitoring infrastructure.

</details>

5. **Client failover behavior**
      - **Multi-endpoint URIs:** Configure clients with multiple broker addresses for automatic failover.  
      - **Reconnect backoff/jitter:** Prevent thundering herds when brokers recover.  
      - **Delivery semantics:** Decide between at-least-once or at-most-once; implement idempotency for duplicates.  
      - **Flow control tuning:** Adjust producer credits and consumer prefetch to balance throughput and latency.  
      - **Graceful shutdowns:** Drain producers/consumers during maintenance to avoid unnecessary redeliveries.


<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Multi-endpoint URIs:** Provide clients with multiple broker addresses in connection strings. Use ordered or randomized lists based on locality preferences. Include backoff and jitter to avoid thundering herds during failover. `Clients need more than one door to walk through. Multi-endpoint configs remove DNS as a single point of failure and speed reconnection after broker loss.`
   - **Prevents:** Extended client downtime when a single broker or DNS endpoint fails.  
   - **Evidence:** Client reconnects complete within target RTO to alternate brokers; connection attempts distributed evenly, avoiding storms against one endpoint.

- **Reconnect backoff/jitter:** Configure bounded retries, exponential backoff, and circuit breaking. Prefer fast local retries, slower cross-region retries. Detect stale connections aggressively and close them to trigger reconnection logic. Add jitter to prevent synchronized retry storms. `Backoff and jitter prevent thundering herds that crush recovering brokers. Circuit breakers avoid futile retries and resource exhaustion.`
   - **Prevents:** Cascading failures during broker recovery; resource exhaustion from retry loops.  
   - **Evidence:** Even distribution of reconnection attempts over time; brokers see stable, gradual connection ramp-up; circuit breakers open predictably under sustained failures.

- **Delivery semantics:** Choose at-least-once or at-most-once delivery based on workload requirements. For at-least-once, implement idempotency keys and deduplication at consumers. For at-most-once, constrain scope carefully and test rigorously. For exactly-once, understand the limitations and test thoroughly. `HA changes delivery guarantees. Idempotency is your safety net for at-least-once; strict controls protect at-most-once from silent drops.`
   - **Prevents:** Double-processing or silent message loss during failover events.  
   - **Evidence:** Idempotent consumers handle duplicates safely; duplicate metrics tracked and managed; message loss rate stays within acceptable bounds for at-most-once workloads.

- **Flow control tuning:** Adjust producer credits and consumer prefetch to match network latency and throughput requirements. Keep queue depths stable; avoid oversized prefetch across high-latency regions. Balance in-flight message counts to prevent memory pressure. `Credits and prefetch govern how much data is in-flight. Mis-tuning amplifies latency (too low) or exhausts memory (too high).`
   - **Prevents:** Queue bloat, consumer starvation, producer stalls, and memory exhaustion from excessive in-flight messages.  
   - **Evidence:** Balanced throughput across producers/consumers; bounded in-flight message counts; stable queue depths even across regions.

- **Graceful shutdowns:** Drain producers before maintenance windows; close consumers cleanly to reduce redeliveries. Validate transaction boundaries across failovers to prevent partial commits. Planned maintenance should not look like a crash to clients. `Abrupt shutdowns cause unnecessary redeliveries and partial transactions. Draining ensures clean state transitions.`
   - **Prevents:** Unnecessary duplicate messages and inconsistent transactional state.  
   - **Evidence:** Maintenance windows show clean producer/consumer drains; zero unexpected redeliveries; transaction logs confirm no partial commits during planned shutdowns.

</details>

6. **Azure Container Apps specifics**
      - **Probes:** Align readiness probes with journal recovery; liveness probes should tolerate GC pauses.  
      - **Autoscaling:** Keep minimum replicas to preserve quorum; never scale voters below majority.  
      - **Revision rollouts:** Use rolling updates with surge capacity; ensure backup readiness before replacing live brokers.  
      - **Resource limits:** Right-size CPU/memory; set hard limits to avoid eviction.  
      - **Observability:** Monitor queue depth, consumer lag, connection churn, and election events with actionable alerts.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Probes:** Set liveness and readiness probes to accommodate journal recovery time and cluster handshakes. Container restarts are fast, but broker initialization isn't. Use readiness gates so traffic flows only after the broker is truly operational. Set readiness initial delay equal to measured journal recovery time; liveness timeout slightly longer than typical GC pauses. `Kubernetes reports containers ready when the process starts, not when the broker finishes recovery. Misaligned probes route traffic prematurely, causing errors.`
   - **Prevents:** Premature traffic routing, failed connection handshakes, and false positive health-check cycles.  
   - **Evidence:** Readiness probe passes only after journal replay and cluster initialization complete; liveness probe tolerates normal GC pauses without restart; no client connection failures during broker startup.

- **Autoscaling:** Keep minimum replica counts that preserve quorum during maintenance and scale-down events. Avoid scaling voters down below majority threshold. Use metrics like active connections or queue depth for scale decisions, not just CPU/memory. Never reduce voters below the count needed for majority (e.g., keep ≥3 for a 3-voter setup). `Autoscalers don't understand quorum. Scaling down voters can unintentionally remove your majority, halting elections and promotions.`
   - **Prevents:** Accidental quorum loss from autoscaler decisions; inability to elect a new live broker during scale-down.  
   - **Evidence:** Autoscaling policies enforce minimum replica floors that maintain quorum; scale events logged and reviewed; quorum remains intact during all scale actions.

- **Revision rollouts:** Use rolling updates with surge capacity so a new replica is ready before the old one terminates. Partition upgrades to ensure a live broker isn't replaced before its backup is confirmed ready. Validate new revisions against health endpoints before shifting traffic. `Rolling updates must preserve at least one live messaging path. Surge capacity and partitioned rollouts prevent update-induced outages.`
   - **Prevents:** Update-induced outages or mid-traffic role swaps causing message loss or connection drops.  
   - **Evidence:** Zero-downtime deployments; backup brokers report ready before live brokers terminate; traffic continues seamlessly during revision rollouts.

- **Resource limits:** Right-size CPU and memory allocations based on measured peak usage. Set hard limits to prevent node eviction from resource contention. Pin replicas to availability zones when possible; avoid noisy-neighbor impacts by reserving baseline resources. `Under-provisioning causes throttling and OOM kills. Over-provisioning wastes cost. Noisy neighbors and memory spikes can evict critical brokers.`
   - **Prevents:** Container preemption, out-of-memory crashes, CPU throttling under load, and noisy-neighbor interference.  
   - **Evidence:** Stable resource usage patterns; no CPU throttling or memory pressure events; no evictions in container logs; consistent latency under load.

- **Observability:** Centralize logs and metrics covering connections, queue depth, page usage, and election outcomes. Implement actionable alerts tied to SLOs. Sign or encrypt logs and keep retention aligned to audit and compliance needs. `You can't fix what you can't see. Fine-grained metrics and tamper-proof logs let you act before SLOs break and provide forensic trails.`
   - **Prevents:** Blind spots leading to silent message buildup, election failures, or security incidents going undetected.  
   - **Evidence:** Dashboards show queue depth, consumer lag, connection churn, and election events; alerts fire before SLO breaches; log integrity verified via signatures.

</details>
      
7. **Operations and DR drills**
      - **Regular failover tests:** Simulate broker crash, zone outage, and region outage.  
      - **Backup/restore rehearsals:** Test restores to staging; validate journal integrity.  
      - **Config drift detection:** Keep configs in Git; alert on unauthorized changes.  
      - **Runbooks:** Document voter replacement, broker promotion/demotion, and planned maintenance.  
      - **Post-incident reviews:** Tune timeouts and probes based on real incident data.

<details>
<summary><b> Expand for detailed explanation</b> (Click to expand)</summary>

- **Regular failover tests:** Simulate broker crashes, zone outages, and full region loss scenarios. Verify voter quorum behavior, promotion timing, and client continuity during each test. Record actual RTO/RPO and compare against targets. `High availability isn't real until it's rehearsed. Testing validates timing, correctness, and actual client experience under realistic failure conditions.`
   - **Prevents:** Discovering HA gaps, misconfigured timeouts, or broken failover logic during actual incidents.  
   - **Evidence:** Documented RTO/RPO from drill runs; clean promotions within target windows; no data anomalies or message loss; client reconnections succeed automatically.

- **Backup/restore rehearsals:** Test full and point-in-time restores to staging environments regularly. Validate journal integrity, certificates/keys, and configuration after recovery. Automate backups with documented retention policies. `Backups you've never restored are hope, not strategy. Rehearsals reveal corruption, missing dependencies, and restore-time gaps.`
   - **Prevents:** Discovering broken or incomplete backups during a crisis; prolonged downtime from restore failures.  
   - **Evidence:** Successful restores to staging within RTO targets; journal integrity checks pass; all certificates, keys, and configs usable post-restore.

- **Config drift detection:** Keep broker and voter configurations under version control (Git). Continuously compare running state to desired state in source control. Alert on unauthorized or manual changes. `Small manual edits accumulate into dangerous divergence. Drift creates inconsistent HA behavior and surprises during failover.`
   - **Prevents:** Inconsistent HA behavior across nodes; unknown configuration changes breaking failover logic.  
   - **Evidence:** Git-backed configurations; periodic automated diff checks; alerts fire on unauthorized changes; all config changes traceable to commits and approvals.

- **Runbooks:** Create time-boxed, step-by-step runbooks with clear rollback triggers for common operations: voter replacement, broker promotion/demotion, and planned maintenance. Test runbooks during drills to validate accuracy and timing. `Clear steps reduce decision-making overhead and human error when stress is high. Time-boxing ensures teams don't get stuck.`
   - **Prevents:** Human error, slow response during incidents, and incomplete or incorrect operational changes.  
   - **Evidence:** Teams execute voter replacement or broker demotion quickly and consistently; runbook steps completed within documented time windows; rollback procedures validated.

- **Post-incident reviews:** Capture metrics, timelines, decisions, and communication during incidents. Tune timeouts, resource limits, and probe thresholds based on actual failure data. Update chaos tests and runbooks to cover newly discovered failure modes. `Learning turns pain into resilience. Real incidents reveal assumptions and gaps that no amount of planning catches.`
   - **Prevents:** Repeated failures from the same root cause; gradual erosion of HA guarantees from undocumented changes.  
   - **Evidence:** Timeouts and probes adjusted based on real latency data; capacity planning updated with actual usage patterns; new chaos tests added for observed failure modes; incident learnings documented and shared.

</details>

## Q&A sample

> `Discovery questions`, is about the **number and distribution of quorum voters**. Because quorum logic depends on majority, the design must use an **odd number** (3, 5, 7…) and spread them across independent sites.

- **Ask about voter count**: Must be odd (3, 5, 7).  
- **Ask about distribution**: Spread across DC1, DC2, and Azure so no single site dominates.  
- **Check quorum resilience**: Ensure quorum survives if Azure voter fails.  
- **Validate latency/security**: Azure voter must communicate reliably and securely with brokers.  
- **Monitor and expand**: Voter health monitoring and multi‑region expansion strengthen HA.  

| **Question** | **Why You’re Asking** | **Possible Answers (Signals)** |
|--------------|-----------------------|--------------------------------|
| How many quorum voters are deployed in total, and is the count odd (e.g., 3, 5)? | Odd number ensures clear majority; even numbers risk ties and stalled elections. | - 3 voters → safe baseline.<br>- 4 voters → risk of tie.<br>- 5 voters → stronger resilience. |
| How are voters distributed across sites (on‑prem DC1, DC2, Azure)? | Distribution prevents one site from controlling quorum; Azure adds geo‑redundancy. | - Majority in one DC → risk if that DC fails.<br>- Spread across DC1, DC2, Azure → resilient. |
| If Azure voter goes offline, does quorum still hold? | Ensures Azure is additive, not a single point of failure. | - Quorum remains with on‑prem voters → safe.<br>- Quorum lost without Azure → risky. |
| Are brokers configured as live/backup pairs or clustered across DCs? | Clarifies failover model; affects how voters arbitrate. | - Live/backup pairs → simpler elections.<br>- Clustered brokers → more complex, need careful tuning. |
| What’s the latency between Azure voter and on‑prem brokers? | High latency can delay elections or cause false failovers. | - <100ms → acceptable.<br>- >300ms → may need timeout tuning. |
| How are voter processes monitored in Azure? | Silent voter failures can break quorum unexpectedly. | - Integrated with Azure Monitor → good.<br>- No monitoring → hidden risk. |
| Do you plan to expand voters into multiple Azure regions? | Multi‑region voters avoid dependency on one Azure region. | - Yes → stronger geo‑redundancy.<br>- No → risk if Azure region fails. |


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->
