# PhonePe SDE-2 — System Design / High-Level Design (HLD) Questions

> Compiled from real candidate experiences (LeetCode Discuss, GeeksforGeeks, Glassdoor, Desi QnA,
> Medium, roundz.substack).

## How the HLD round works (quick recap)
- ~60 min, **one open-ended problem**; **you drive** the conversation.
- Expected structure:
  1. **Requirements** — functional (FR) + non-functional (NFR)
  2. **Capacity estimation** / back-of-envelope (be ready — many candidates got caught here)
  3. **High-level architecture** — components, services, data flow
  4. **API design**
  5. **Data model + DB choice** (SQL vs NoSQL with justification)
  6. **Deep dives** — caching, search, feeds, fault tolerance, scaling hotspots
  7. **Trade-offs** — present 2–3 approaches per major decision and defend choices
- It is **not just drawing boxes** — it's about **defending decisions with trade-offs**.

---

## Reported / commonly asked HLD problems

### Confirmed from candidate experiences
1. **Quora-like Q&A forum** *(asked multiple times)*
   - First for internal company use, then extensible to other companies.
   - Probes: foreign keys if RDBMS chosen; efficient search-result display; separate vs combined DB for user data and Q&A; **auth/authz in API gateway**; passing **auth tokens across microservices**; **Cassandra vs other NoSQL vs RDBMS** trade-offs; feed generation & search indexing; capacity estimation.

2. **Online multiplayer game (Ludo / Chess / Snake & Ladder)** *(asked)*
   - Drive: FR/NFR → HLD → APIs → tech stack → exception handling, fault tolerance, DB choices.
   - Core logic: **matchmaking** (Noob vs Noob, Pro vs Pro), 2–3 approaches per step with trade-offs.

3. **Flight Aggregator System** *(asked)*
   - Aggregate data from multiple airlines; user search + book.
   - Probes: how flight data is fetched & stored; **microservice segregation**; handling **high-traffic search API**; **connecting flights** when no direct flight; booking across airlines; **API-failure handling**.
   - Follow-up that stumped a candidate: if traffic spikes, spawning a new read **slave + replication takes time** — how do you handle it?

4. **Simplified UPI Payment System** *(asked)*
   - **Idempotency**, **ACID transactions**, concurrency control, scaling to **~1B daily requests**.

5. **Payment Gateway System** *(asked — Glassdoor + blog)*
   - Secure auth, transaction validation, **idempotency**, logging, load balancers, distributed DBs, encryption.

6. **E-commerce subscription suggestion** *(asked)*
   - Suggest subscription tier (gold/platinum) based on cart amount; add as default-unselected cart item; recompute on cart change; service segregation.

7. **Design the HLD of your current project** *(asked — be ready to whiteboard your own system)*

8. **Google News-style system** *(asked — clustering/aggregating news)*

9. **URL Shortening Service** *(asked in HM round as a design question)*

10. **Scalable Notification Service** *(reported)*

11. **Transaction Ledger System** *(reported)*

12. **Farmer app** *(asked in HR/HM)* — downloads, storage, engagement features.

---

## Topics the interviewers consistently probe
- **SQL vs NoSQL** justification; **Cassandra/MongoDB vs RDBMS**; foreign keys in NoSQL; **CAP theorem**.
- **Scalability**: read replicas/slaves, **sharding**, replication lag, handling sudden traffic spikes on hot APIs (e.g., search).
- **Microservices**: service segregation, **API gateway**, **auth/authz** + token propagation across services.
- **Idempotency** & exactly-once for payments; **ACID** vs eventual consistency.
- **Capacity estimation** / back-of-envelope math.
- **Caching**, **search indexing**, **feed generation**.
- **Fault tolerance**, **API-failure handling**, retries, **circuit breakers**.
- **Async processing** with message queues (**Kafka**), **outbox pattern / CDC** for atomic write + event.
- Concurrency control: **optimistic locking**, distributed locks, queueing.

---

## Fintech-flavored building blocks worth mastering (PhonePe context)
- **Idempotency keys** on payment APIs to prevent duplicate charges (double-click Pay).
- **Outbox pattern + Debezium/CDC → Kafka** so DB write and event publish never diverge.
- **Double-entry ledger** (append-only) + **reconciliation** batch jobs.
- **Strategy pattern** for multiple payment processors (Card/UPI/NetBanking); **Circuit Breaker** around processor calls.
- **Async notifications** (email/SMS/push) via Kafka — never inline in the payment path.
- Sharded SQL (e.g., MySQL/Postgres) for ACID at scale.

---

## Practice list (high ROI)
1. Quora / Q&A forum (with search + feed)
2. UPI / payment gateway (idempotency, ledger, reconciliation)
3. Flight / hotel aggregator (high-read search, connecting routes)
4. Online multiplayer game with matchmaking
5. URL shortener
6. Notification service (multi-channel, async)
7. News aggregator (Google News)
8. E-commerce cart + subscription suggestion
9. Transaction ledger
10. Your own current project (rehearse it!)

> Tip: Always start with requirements + estimation before architecture, and proactively give
> **2–3 alternatives with trade-offs** for each major decision (DB, scaling, consistency).

## Sources
- roundz.substack #101 & #174 — Quora-like forum
- LeetCode Discuss — Ludo/Chess game; Google News
- GeeksforGeeks — Flight aggregator
- placementpreparation.io / Glassdoor — UPI, payment gateway, e-commerce subscription
- Desi QnA — PhonePe SDE 2 sets; URL shortener (HM)
