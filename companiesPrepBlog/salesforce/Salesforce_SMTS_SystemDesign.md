# Salesforce SDE2 / MTS — System Design (HLD) Questions (Last 6 Months)

> Compiled from real interview experiences on **gitGood.dev**, **System Design Handbook**, **Medium**, **interviewexperiences.in**, and **sirjohnnymai.com** (~Dec 2025 – Jun 2026).

---

## How the HLD Round Works
- **60–75 minutes**. Conducted in the onsite loop, sometimes by the Hiring Manager / a Director + SMTS panel.
- The dominant theme is **multi-tenant SaaS** — Salesforce design is an exercise in **multi-tenancy**, not just raw scale.
- **Expected approach:**
  1. **Clarify requirements first** — internal users? enterprises? ISVs? (scope changes everything).
  2. Functional & non-functional requirements, scale estimates.
  3. **Tenant isolation** & data partitioning from the start.
  4. APIs, data model, storage selection.
  5. **Noisy-neighbor mitigation** (rate limiting, quotas, fairness).
  6. Justify trade-offs: consistency vs. availability, caching, latency.

> **Real debrief:** a candidate designed a standard distributed cache and was **rejected for lacking tenant-level isolation**. Multi-tenancy must be front-and-center.

---

## Reported / Common HLD Prompts

| Prompt | Key Areas Discussed |
|--------|---------------------|
| **Multi-tenant platform feature customers can extend** (think Apex triggers) | One customer's bad code must not break another's experience; sandboxing, limits |
| **Shard a service across hundreds of thousands of tenants** | Partitioning by org/tenant ID, rebalancing, hot tenants |
| **Handle a "noisy neighbor"** (customer with 1000× avg data/traffic) | Rate limiting, quotas, resource isolation, fairness |
| **Metadata-driven configuration system** | Extensibility without redeploys; per-tenant customization |
| **Large-scale distributed backend service** | Consistency vs. availability, geo-distribution, caching, event-driven patterns, data modeling, storage, API design |
| **CRM-flavored designs** | Accounts/contacts/opportunities data model; workflow automation (triggers, queues, event pipelines); real-time notifications |

---

## What Interviewers Probe
- **Tenant isolation** & data security across shared infrastructure.
- **Data partitioning / sharding** — usually by **org ID / tenant ID** or region.
- **Noisy-neighbor mitigation** — rate limiting, quotas, resource fairness.
- **Consistency vs. availability (CAP)** — strong consistency for workflow/opportunity updates; availability OK for analytics dashboards.
- **Caching** hot data (Redis/Memcached); low latency via queues & event buses.
- **Extensibility** — customer customization that can't break other tenants.
- **API stability & versioning** — enterprise customers depend on stable contracts.

## Sample Follow-up Questions
- "How do you guarantee one tenant can't exhaust resources for others?"
- "How do you handle a customer with 1000× the data of an average tenant?"
- "How do customers extend this feature without breaking other tenants?"
- "Where do you need strong consistency vs. eventual consistency?"
- "How do you shard, and how do you rebalance hot tenants?"

## Resources
- **System Design Handbook** — Salesforce System Design guide.
- *Designing Data-Intensive Applications* (Kleppmann).
- Study **multi-tenant architecture**, partitioning by tenant, and noisy-neighbor patterns; review Salesforce public API versioning.

*Last updated: June 2026.*
