# PhonePe SDE-2 — Other Rounds (Hiring Manager, Behavioral, CS Fundamentals, OA)

> Covers everything outside the core DSA / LLD / HLD rounds: the Hiring Manager (HM) round,
> behavioral questions, CS-fundamentals/Java rounds, and Online Assessment notes.
> Compiled from real candidate experiences (LeetCode, GeeksforGeeks, Glassdoor, Desi QnA, LinkedIn, blogs).

---

## 1. Hiring Manager (HM) / Managerial Round
- ~45–60 min, taken by a Senior Engineering Manager / hiring manager.
- Usually the **final** round; often a gating round (a candidate who failed HLD didn't reach it).
- Heavy focus on **past projects, impact, and behavior** — with technical cross-questions.

### Project & technical-experience questions
- Walk through your **current/past project architecture** in detail (sometimes a mini-HLD of your own system).
- What was **your specific contribution**? What is your **recent work / impact created**?
- **How much scale/load** was your system handling?
- What **datastore** does your team use — **SQL vs NoSQL**, and why?
- How would you **start and proceed** with developing a new feature? Explain your **SDLC**.
- What would you do / focus on in your **first 90 days** at PhonePe?

### Behavioral questions (reported)
- **Why are you looking for a switch?** Why are you leaving your current company?
- **Why do you want to join PhonePe?**
- Describe a **conflict on code reviews** with a reviewer — how did you manage it?
- A time you faced an **unrealistic / tight deadline** — how did you handle it?
- How do you handle / take **ownership of production issues**?
- **Team conflict** situations; team ethics & collaboration.
- What does **your day look like** in your current company?
- Adaptability questions; ends with **Q&A** for the interviewer.

> Tip: Prepare 5–6 **STAR-format** stories (Situation, Task, Action, Result) covering impact, conflict,
> failure/learning, ownership, deadlines, and leadership/mentoring.

---

## 2. CS Fundamentals / Core Java Round (appears in some pipelines)
Some candidates (especially backend/Java) reported a dedicated fundamentals round or fundamentals woven into other rounds.

### Java internals
- `HashMap` internals (buckets, hashing, resizing, treeification).
- `synchronized` vs `ConcurrentHashMap`; thread-safety.
- **Garbage collection**, JVM memory model.
- Implement an **LRU cache** with **thread-safety** discussion.

### General CS
- **DBMS**: ACID, indexing, transactions, normalization, **CAP theorem**, MongoDB specifics.
- **Operating Systems**: processes/threads, concurrency, deadlocks, scheduling.
- **Computer Networks**: basics, HTTP, TCP/IP.
- **OOPS** concepts and SOLID.
- Microservices, API design, fintech **security practices**.

---

## 3. Online Assessment (OA) — for pipelines that include it
- Platform: HackerRank / CodeSignal / company portal.
- Format: typically **3–4 coding problems**; for mobile roles, **MCQs** (e.g., 10 Android MCQs) + 1 DSA problem.

### Reported OA problems
- **Matrix / grid paths** problem.
- **Array frequency optimization.**
- **Game theory** problem.
- **Tree-based DP.**
- **Top API endpoints** — HashMap + Min-Heap (top-K).
- **String rotation** check.
- **Count islands** — graph traversal.

---

## 4. Quick prep checklist for these rounds
- [ ] Rehearse your project's architecture end-to-end (you may need to whiteboard it).
- [ ] Have crisp **"why PhonePe"** and **"why leaving"** answers.
- [ ] 5–6 STAR behavioral stories ready.
- [ ] Brush up Java internals (HashMap, ConcurrentHashMap, GC) + LRU cache.
- [ ] Revise DBMS/OS/CN/OOPS fundamentals + CAP theorem.
- [ ] Be ready to justify SQL vs NoSQL choices from your own work.

## Sources
- GeeksforGeeks — PhonePe SDE-2 (HM round questions)
- LeetCode Discuss — PhonePe HM round
- LeetCode Discuss (Pune, Accepted) — behavioral questions, SDLC
- placementpreparation.io — Core Java round, OA breakdown, HR round
- roundz.substack #101 & #174 — HM round details
- LinkedIn — Hari Krishna Doradla — OA/round breakdown
