# Microsoft SDE2 — High-Level / System Design (HLD) Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **DesignGurus**, **gitGood.dev**, **Prepfully**, **Medium**, and **interviewexperiences.in** (~Dec 2025 – Jun 2026).
>
> **Scope at SDE2 is bounded:** design a **moderate-complexity service**, not "architect Azure globally." Questions often map to Microsoft products (Azure, Teams, Office 365, OneDrive, Xbox, LinkedIn). For **L63+**, system design carries more weight than coding.

---

## How the HLD Round Works
- **60 minutes** with a Microsoft engineer (sometimes blended with LLD).
- **Note:** System design is typically asked at **L61+**; junior levels (L59–60) may get a simplified version or none.
- **Expected approach:**
  1. Clarify **functional & non-functional requirements** and constraints (read/write ratios, scale, SLAs).
  2. Define **APIs** and **data model**.
  3. High-level architecture; pick storage; caching strategy.
  4. **Defend trade-offs** — consistency vs. availability, sharding key choice, replication.
  5. Address failure handling, bottlenecks, scaling.
- **Biggest failure point:** can't **defend** *why* you chose a sharding key or consistency model (~68% of SDE2+ rejections are weak trade-off analysis, not coding).

---

## Reported / Common HLD Prompts

| Prompt | Key Areas Discussed |
|--------|---------------------|
| **Distributed Key-Value Store** (Redis-like) | Data **sharding**, replication, consistency vs. availability trade-offs |
| **OneDrive-style file storage** | Upload/download, metadata, chunking, sync, dedup |
| **Notification system** | Fan-out, queues, delivery guarantees, retries |
| **URL shortener** | Hashing, key generation, redirect, analytics |
| **LRU / caching system** | Eviction, hit ratio, distributed cache |
| **Workday Leave Manager** (HLD + LLD mix) | Architecture + class design + core functions |
| Microsoft-product designs | Teams, Office 365, Azure services, Xbox, LinkedIn flavored |
| Cloud-adjacent designs | Azure **Service Bus**, **Blob Storage**, **Cosmos DB** patterns surface naturally |

---

## What Interviewers Probe
- **Trade-off judgment** — consistency vs. availability (CAP), latency vs. throughput.
- **Sharding / partitioning** — and *why* that partition key.
- **Caching** — where, what TTL, invalidation.
- **Reliability** — replication, failure handling, idempotency.
- **Scalability** with realistic constraints (read/write ratios, QPS).
- Cloud-native / **Azure** awareness for cloud-adjacent teams (not mandatory standalone).

## Sample Follow-up Questions
- "What metrics prove this design is successful?"
- "Why did you choose that sharding key / consistency model?"
- "How does this handle a node failure / network partition?"
- "How would you scale this 10×?"

## Resources
- DesignGurus — Microsoft System Design guide (scoring dimensions + questions by product area).
- *Designing Data-Intensive Applications* (Kleppmann).
- Practice bounded services with real constraints; learn core **Azure** primitives (Service Bus, Blob Storage, Cosmos DB).

*Last updated: June 2026.*
