# Microsoft SDE2 — Low-Level Design (LLD / OOD) Questions (Last 6 Months)

> Compiled from real interview experiences on **LeetCode Discuss**, **interviewexperiences.in**, **Medium** (esp. Prashant Priyadarshi's Microsoft LLD list & Neha Goyal's experience), **LinkedIn**, and **YouTube** (~Dec 2025 – Jun 2026).
>
> **Microsoft is notably LLD-heavy** — they value object-oriented design more than most big-tech peers. LLD/OOD questions appear in dedicated rounds **and** inside DSA rounds.

---

## How the LLD Round Works
- 60–75 min; often starts with **Java / OOP concept questions** and a project deep-dive.
- Problems are frequently **open-ended** — clarify requirements & edge cases first.
- Evaluated on:
  - Clean **class hierarchy** with the right abstraction.
  - **SOLID** principles (esp. **OCP** — extend without modifying).
  - Correct **design patterns** — **State**, **Strategy**, Factory, Observer, Command, Singleton.
  - **Concurrency / thread-safety**, race conditions.
  - **Actual code implementation**, not just diagrams — and the **"why"** behind DSA choices.

---

## Reported LLD Prompts (last 6 months)

| Prompt | Key Pattern / Focus |
|--------|---------------------|
| **Parking Lot** (single & **multi-floor**) | THE most common; `Vehicle`/`Spot`/`Ticket` classes; Strategy for allocation; "lot full" edge case |
| **Vending Machine** | **State pattern**; extensibility via SOLID |
| **Undo/Redo for a text editor** with configurable limits | Right data structures for efficient history (two stacks / deque) |
| **Microsoft Excel-like platform** (pages, sheets, rows, columns, cells holding text/image/video) | Class hierarchy; create/delete page/row/column/cell; row/column-wide operations; **OCP** for new properties; interfaces vs. abstract classes |
| **Board game** (Snake & Ladder-like) | `Player`, `Board`, `Dice`, `GameManager`; **Strategy** for dice; **Singleton** for game state; power-ups / multi-threaded turns |
| **Logging system** using multithreading | Thread safety, race conditions, async appenders |
| **Workday Leave Manager** (HLD + LLD mix) | Class design + edge cases (prevent overlapping leaves, max 3 continuous leaves) + code core functions |
| **Elevator Management System** | **State pattern** (Moving Up/Down/Idle); single-lift feasibility, single-lift simulation, multi-lift |
| **Container Orchestrator** | Manage machine CPU/memory; **Strategy** for machine-selection algorithm |
| **Dictionary App** (words & meanings) | Trie / map design |
| **Job Scheduler** | Scheduling, priorities, recurrence |
| **Movie ticket booking (BookMyShow)** | Seat locking, concurrency |
| **Hit counter / webpage visits counter** | Sliding-window counts (DSA-flavored LLD) |
| **Excel SUM formula** | Dependency graph, recalculation |
| **Google Search Autocomplete** | Trie + ranking |
| **Chess / Tic-Tac-Toe** | Piece hierarchy, move validation |

---

## Preparation Checklist
1. **OOP fundamentals** — interfaces vs. abstract classes, composition over inheritance, **Java internals**.
2. **Design patterns** — **State** & **Strategy** are Microsoft favorites; also Factory, Observer, Command, Singleton.
3. **SOLID** — especially **Open/Closed Principle** (add features without modifying existing code).
4. **Concurrency** — thread-safe loggers/schedulers; locks, race conditions.
5. **Write real code** for core classes, plus edge-case handling — not just diagrams.
6. Be ready for LLD to appear **inside a DSA round** (and vice versa).

## Resources
- Prashant Priyadarshi — "Microsoft Most Frequent Low Level Design Questions" (Medium).
- Practice State/Strategy on Elevator, Vending Machine, Parking Lot; build full class code.

*Last updated: June 2026.*
