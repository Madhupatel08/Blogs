# Amazon SDE2 — Low-Level Design (LLD / OOD) Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **interviewexperiences.in**, **HelloInterview**, **CrackingWalnuts**, **Medium**, **LinkedIn**, and **interviewhelp.io** (~Dec 2025 – Jun 2026).

---

## How the LLD Round Works
- **60-minute** round; usually **1 round** in the SDE2 loop (the Bar Raiser may add a second LLD-flavored discussion).
- Focus is on **design thought process**, not always fully running code.
- What they evaluate:
  - Clean class hierarchy with the **right level of abstraction**.
  - **SOLID** principles applied practically.
  - Correct **design patterns** (Strategy, Factory, Observer, Singleton, State).
  - **Concurrency / thread-safety** and **edge cases** discussed *before* being asked.
  - Test cases at the end if time permits.
- **What kills candidates:** 12 classes when 4 are needed; methods that do too much/too little; missing the obvious edge case (e.g., "what if the parking lot is full?").
- **Tip:** Get the **class boundaries right before the methods**. Justify *why* a method belongs in a specific class and *why* a pattern fits.

---

## Reported LLD Prompts

| Prompt | Key Focus Areas |
|--------|-----------------|
| **Board game (Ludo / Chess)** | Class responsibilities; where "move a piece" behavior lives; design patterns + SOLID |
| **Uber / Ride-Hailing System** | `Rider`, `Driver`, `Trip`, `Payment`, `Location` entities; trip state machine (`requested → accepted → in_progress → completed/cancelled`); driver matching via geospatial index (quadtree/geohash); surge pricing; idempotent payments |
| **Rider-Finding Service** | Efficiently find a rider for a quick-commerce app |
| **Offline Download Manager** | Architecture + core functionality for a social media app |
| **Food Ordering System** | Classes/services for search, sort, ordering, rating |
| **Vending Machine** | State pattern; ~4 classes (not 12); handle out-of-stock / exact change edge cases |
| **Parking Lot** | `ParkingSpot`, `Vehicle` (Car/Bike subclasses), `Ticket`, `ParkingLot`; thread-safe spot allocation; "lot full" edge case |
| **Rate Limiter** | Pluggable algorithms (Token Bucket, Leaky Bucket, Fixed/Sliding Window); `isAllowed(request)` interface; thread safety; distributed extension |
| **Basic Calculator** | Extensibility for adding new operations; clean modular design |
| **Elevator System** | Scheduling strategy, multiple cars, request queues |
| **Internal AWS feature (Bar Raiser)** | Both HLD + LLD discussion in one round |

---

## Preparation Checklist
1. **OOP fundamentals** — encapsulation, polymorphism, abstraction; **prefer composition over inheritance**.
2. **SOLID** — be able to name & apply each principle to your design live.
3. **Design patterns** — Strategy, Factory, Observer, Singleton, State, Decorator.
4. **Concurrency** — thread-safe counters, atomic ops, locks; identify race conditions (e.g., concurrent spot allocation).
5. **APIs & data models** that evolve gracefully as requirements change.
6. Practice from a **vague product prompt** → drive to class boundaries → methods → edge cases.

## Resources
- **Shrayansh Jain** LLD playlist (Udemy/YouTube).
- Practice repos of common LLD problems (parking lot, rate limiter, elevator, vending machine).

*Last updated: June 2026.*
