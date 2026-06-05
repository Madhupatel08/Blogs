# Amazon SDE2 — System Design (HLD) Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **interviewexperiences.in**, **HelloInterview**, **CrackingWalnuts**, **Medium**, and **interviewhelp.io** (~Dec 2025 – Jun 2026).

---

## How the HLD Round Works
- **60-minute** round (sometimes runs longer if you're on track); **1 dedicated HLD round** in the SDE2 loop.
- Often conducted by the **Hiring Manager** — doubly important for the final decision.
- **Expected approach (customer-first):**
  1. Clarify **functional & non-functional requirements** (customer framing first).
  2. Estimate **scale** (QPS, storage, read/write ratio).
  3. Define **APIs** and **data model**.
  4. Draw the **high-level architecture**.
  5. **Justify trade-offs** (DB choice, caching, consistency vs. availability).
  6. Address **bottlenecks**: traffic spikes, hot keys, sharding, replication.
- **Watch-outs:** jumping to tech before requirements; ignoring data-first thinking; not defending trade-offs.

---

## Reported HLD Prompts

| Prompt | Key Areas Discussed |
|--------|---------------------|
| **Coursera-like platform** | User management, course catalog, payments, notifications, video streaming |
| **Google Docs** | Collaborative real-time document editing; conflict resolution / OT-CRDT |
| **YouTube** | Video uploads, likes/dislikes, comments; storage scaling; high-concurrency read/write |
| **Uber (HLD)** | Handling sudden cab-demand surge from a location; API architecture + DB schema |
| **Event Logging System** | Scalability, reliability, data processing pipeline |
| **WhatsApp Read Receipts (ticks)** | Delivery/read status tracking at scale |
| **FastTag / electronic toll collection** | Requirements gathering, Redis, scalability |
| **Amazon Ads Server** | Thousands of ad requests/sec; data storage, caching, real-time analytics; traffic-spike handling; DB choice |

### Common Amazon Prompts (worth pre-practicing)
- **Order Service** / order tracking
- **Notification System**
- **API Rate Limiting** (distributed)
- **Recommendation Cache**
- **URL Shortener** with analytics
- **S3-lite** file storage / file system with versioning

---

## Sample Follow-up Questions Interviewers Ask
- "How would you handle traffic spikes?"
- "What database would you use and why?"
- "How do you ensure idempotency / handle retries and failures?"
- "How does this scale to 10× the traffic?"
- "Where are the bottlenecks and single points of failure?"

## Resources
- **HelloInterview** (HLD guides).
- *Designing Data-Intensive Applications* (Kleppmann).
- Practice 4-tiered software architecture; be comfortable whiteboarding by hand.

*Last updated: June 2026.*
