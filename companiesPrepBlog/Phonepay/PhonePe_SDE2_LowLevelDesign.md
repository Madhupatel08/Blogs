# PhonePe SDE-2 — Low-Level Design / Machine Coding Questions

> Compiled from real candidate experiences (LeetCode Discuss, GeeksforGeeks, Glassdoor, Desi QnA,
> Medium, roundz.substack). This is PhonePe's **most heavily weighted** round.

## How the Machine Coding / LLD round works (quick recap)
- **90–120 min** to write a complete, runnable solution (console or in-memory DB is fine; any language, **Java most common**).
- Formats: take-home on CodeSignal/CodePair, mailed problem with **24-hour** deadline (submit ZIP), or live.
- **5–7 test cases** typically must pass.
- Followed by a **30-min evaluation**: code walkthrough + scaling/extension follow-ups + concurrency questions.

### What interviewers grade
- **SOLID principles** & clean OOP modeling
- **Design patterns** (Strategy, Factory, Observer, Repository, Singleton, State, Builder)
- **Extensibility** — can you add a feature with minimal code change?
- **Separation of concerns** — entity / repository / service layers
- **Thread-safety / concurrency** (race conditions, ConcurrentHashMap, locks)
- **Exception handling**, input validation, readability
- Working code that passes all required test cases

> ⚠️ Note from candidates: passing all tests is **not** sufficient. Some interviewers compare against a
> fixed reference solution and expect specific structures (e.g., a Repository class). Design quality and
> your walkthrough reasoning matter as much as correctness.

---

## Reported / commonly asked LLD problems at PhonePe

### Confirmed from candidate experiences
1. **Vehicle / Car Rental Service** *(very frequently asked)*
   - Multiple branches in a city; vehicle types: Sedan, Hatchback, SUV.
   - Price defined **per branch, per vehicle type** (not per vehicle).
   - APIs: `addBranch`, `allocatePrice(branch, type, price)`, `addVehicle(id, type, branch)`,
     `bookVehicle(type, startTime, endTime)` using **lowest-rental-price** allocation strategy,
     `viewVehicleInventory(startTime, endTime)`.
   - Tests time-slot booking conflicts, strategy for branch selection, inventory snapshot.

2. **Multi-level Cache** *(frequently asked)*
   - L1…Ln cache hierarchy.
   - **Pluggable eviction strategy** (implement LFU; design so LRU/others can drop in).
   - Read/write propagation across levels, thread-safety.

3. **Coupon Management System**
   - Distributor creates a **batch** and ingests coupons; system **grants** coupons from batch to users.

4. **Issue / Ticket Handling System (Customer Support)**
   - Customers raise tickets of different **types**; support team has **specializations**.
   - Assign tickets to the right agent. Follow-ups: add reviews & incentives for staff, scale, race conditions.

5. **Order Management System.**

6. **To-do / Task list application**
   - 90-min CodeSignal challenge with a feature list (add/update/track tasks, etc.).

7. **IoT / Home Automation tool** (rules to automate devices).

8. **Fitness / Slot Booking system.**

### Strongly recommended (asked at PhonePe / peer fintechs — Razorpay, CRED, Slice; standard LLD set)
9. **Splitwise / Expense Splitter**
   - Split types: EQUAL / EXACT / PERCENTAGE via **Strategy pattern**.
   - Balance tracking via Repository; **debt simplification** (minimize transactions) algorithm.
   - Entities: User, Group, Expense, Balance, Settlement, SplitStrategy.

10. **Parking Lot**
    - Multi-level, multiple vehicle types (car/bike/truck), slot allocation, ticketing, pricing.

11. **Rate Limiter** (Token Bucket / Sliding Window; pluggable algorithm).

12. **Wallet System (PhonePe/Paytm-style)** — add money, debit/credit, transaction ledger, idempotency.

13. **Snake & Ladder / Ludo / Chess (multiplayer board game).**

14. **Movie Ticket Booking (BookMyShow)** — seat locking/concurrency.

15. **Logging Framework (log4j-style)** — levels, pluggable appenders/sinks (Strategy/Chain).

16. **Elevator System.**

17. **Food Delivery (Zomato/Swiggy-style) ordering core.**

---

## Patterns to map to common problems
| Problem | Primary pattern(s) |
|---------|--------------------|
| Cache eviction (LRU/LFU) | Strategy + Repository |
| Splitwise splits | Strategy (+ Repository, Service layer) |
| Vehicle rental allocation | Strategy (lowest price), Factory |
| Logging framework | Strategy / Chain of Responsibility |
| Notifications / reviews | Observer |
| Rate limiter algorithms | Strategy |
| Payment/processor selection | Strategy + Factory |
| Game state (Snake&Ladder/Chess) | State + Factory |
| Single config/registry | Singleton |

---

## How to ace it (candidate-tested tips)
- Spend the first 5–10 min clarifying requirements and sketching classes before coding.
- Layer your code: `entity` / `repository` / `service` / `strategy` packages.
- Default to **thread-safe** collections (`ConcurrentHashMap`) and call out where locks would be needed.
- Make eviction/split/pricing logic **pluggable** so you can answer "add a new type" instantly.
- Add a small `main`/demo + the given test cases so you can demo a clean run.
- Handle invalid inputs with custom exceptions, not silent failures.
- During the walkthrough, lead with **why** each design decision was made and how it supports extension/scale.

## Sources
- Desi QnA — PhonePe SDE 2 Set-2 (Coupon), Set-12 (Car Rental), Set-17 (Vehicle Rental OA)
- GeeksforGeeks — PhonePe SDE (2–5 yrs): Multi-level cache + LFU
- LeetCode Discuss — Issue/ticket system
- Glassdoor — Splitwise, ride-matching, Snake & Ladder
- Medium (lldhub, Chakresh Tiwari) — Splitwise/standard LLD set
- roundz.substack #174 — To-do list machine coding
