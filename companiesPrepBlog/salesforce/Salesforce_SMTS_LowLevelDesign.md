# Salesforce SDE2 / MTS — Low-Level Design (LLD / OOD) Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **interviewexperiences.in**, **Medium** (esp. Prashant Priyadarshi's recent-interviews list), **Substack (roundz)**, and **gitGood.dev** (~Dec 2025 – Jun 2026).

---

## How the LLD Round Works
- Often combined with a **DSA round** (e.g., array problem first, then LLD).
- **Requirements are deliberately vague** — the interviewer expects you to **ask clarifying questions** before designing.
- Evaluated on:
  - **SOLID** principles applied practically.
  - **Clean API signatures**, abstraction, and interfaces.
  - Correct **design patterns** — Strategy, State, Factory, Observer.
  - **Concurrency / thread-safety** (Salesforce cares deeply — locks, CAS, queues).
  - Edge cases and extensibility.

---

## Reported LLD Prompts

| Prompt | Key Pattern / Focus |
|--------|---------------------|
| **Parking Lot** (THE most common — must-do) | **Strategy pattern** for parking strategies; `Vehicle`, `ParkingSpot`, `Ticket`, `ParkingLot`; "lot full" edge case |
| **Meeting Room Scheduler** | Book / cancel / view rooms; handle **conflicting meetings**; search by room or by employee |
| **Elevator System** | **State pattern** (Moving Up / Moving Down / Idle) — each state behaves differently for stop/add-request decisions; scheduling |
| **Notification Library** | Pluggable channels (email, SMS, push); **Strategy / Factory**; extensibility |
| **Connection Pool with internal request queue** | Fixed pool of reusable connections; assign by `requestId`; queue waiters until a connection frees; **thread-safety** |
| **LRU Cache / LFU Cache** | HashMap + doubly linked list; O(1) ops; eviction policy |
| **In-Memory Cache with custom eviction policy** | Pluggable eviction **strategy** |
| **Rate Limiter** | Per-`resourceId` limits; Token Bucket / Sliding Window; thread-safe |
| **RPC Framework** | Serialization, client stubs, transport abstraction |
| **Stack with Increment operation** | Amortized O(1) `increment(k, val)` |
| **Movie Ticket Booking (BookMyShow)** | Seat locking, concurrency, search by movie |
| **Chess Game** | Piece class hierarchy, move validation, board state |

---

## Preparation Checklist
1. **OOP fundamentals** — encapsulation, polymorphism, abstraction; prefer **composition over inheritance**.
2. **Design patterns** — **Strategy** & **State** are the most-requested at Salesforce; also Factory, Observer, Singleton, Decorator.
3. **SOLID** — name & apply each principle live.
4. **Concurrency** — thread-safe pools/caches/queues; identify race conditions; locks, CAS, executors, deadlocks.
5. **Clarify first** — drive out hidden requirements via questions before coding.
6. **Class boundaries before methods** — keep the design lean (avoid over-engineering).

## Resources
- Prashant Priyadarshi's "Salesforce LLD Questions from recent Interviews" (Medium).
- Machine-coding practice repos (parking lot, elevator, connection pool, caches, rate limiter).

*Last updated: June 2026.*
