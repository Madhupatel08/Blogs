# Microsoft SDE2 (L61/L62) — Interview Process (2026)

> Compiled from real interview experiences on **LeetCode Discuss**, **GeeksforGeeks**, **InterviewBit / interviewexperiences.in**, **IGotAnOffer**, **gitGood.dev**, **DesignGurus**, **Prepfully**, **Medium**, **LinkedIn**, and **YouTube** (~Dec 2025 – Jun 2026).
>
> **Disclaimer:** Exact rounds vary by team and level. This reflects the *most consistently reported* structure for SDE2 (Software Engineer II, L61/L62).

---

## Timeline
- **Total duration:** ~3–6 weeks from recruiter contact to offer.
- **Total rounds:** 4–6 (1 screen + 3–5 loop rounds, including the AA round).

---

## Stage 1 — Recruiter Screen (~30 min)
- Background, motivation, role/level, location, compensation expectations.
- Recruiter explains the loop format and which areas each round covers.
- Microsoft often probes genuine interest: *"Why Microsoft?"* / *"What's your favorite Microsoft product?"*

## Stage 2 — Online Assessment (OA) or Phone Screen (60–90 min)
- **Mid-level (SDE2):** usually an **online coding assessment** (Codility / HackerRank), **2–3 LeetCode medium (sometimes medium-hard)** problems, often on Arrays/Strings. Custom test cases must all pass.
- **Senior (L63+):** a **live technical phone screen** with one coding problem + a short design discussion replaces the OA.

## Stage 3 — Onsite Loop (4–5 rounds, ~60 min each, virtual on Teams)
Microsoft typically schedules rounds in **pairs (2 per day)**. A common loop:

| Round | Focus |
|-------|-------|
| **Coding Round 1 (DSA)** | Data structures & algorithms, LeetCode medium. Clean, readable code + edge cases. |
| **Coding Round 2 (DSA / OOD)** | Second coder with a different interviewer — often more open-ended or design-shaped (e.g., design a class hierarchy, small data processor). |
| **Low-Level Design (LLD / OOD)** | Object-oriented design of a feature — class structure, SOLID, design patterns, sometimes actual code. Microsoft weights OOD more than most companies. |
| **System Design (HLD)** | 60 min designing a moderate-complexity distributed system (bounded scope at SDE2). |
| **Behavioral** | Often **woven into every round** rather than standalone — Growth Mindset focus. |

> **Note:** Several recent candidates report **2 DSA + 2 LLD/HLD** loops, with the relative weighting of DSA vs. design depending heavily on the team. Microsoft is notably **LLD-heavy** compared to other big tech.

## Stage 4 — The "As Appropriate" (AA) Round
- Microsoft's **unique final interview** — only happens **if earlier rounds go well** (an invite is a strong positive signal).
- Conducted by a **senior leader** (Principal Engineer / Engineering Manager several levels above the role) — often the **Hiring Manager ("as-app")**.
- The AA interviewer has **read all prior feedback** and **probes flagged gaps**:
  - Technical gap flagged → expect more technical / architecture deep-dives.
  - Culture-fit unclear → expect more behavioral.
- Blends **architectural deep-dives into past projects** + **behavioral** (Growth Mindset, handling disagreement).
- Their recommendation **carries the most weight** and can override earlier feedback. The AA interviewer may also **"sell" the company** to you if you did well.

## Stage 5 — Decision & Offer (~1–2 weeks)

---

## What Microsoft Evaluates
- **Clean, readable, maintainable code** — interviewers are explicitly instructed to judge code quality, not just correctness.
- **The "why"** behind every technical choice (sharding key, consistency model, data structure).
- **System design trade-off judgment** — ~68% of SDE2+ rejections (2025 HC data) were from weak trade-off analysis, *not* coding errors.
- **Growth Mindset** (Satya Nadella's defining value) — learning from failure, handling ambiguity, collaboration, measurable impact.
- **Object-oriented design** ability — more emphasized at Microsoft than at peers.

## Quick Prep Map
- **Weeks 1–2:** Arrays, Strings, Linked Lists.
- **Weeks 3–4:** Trees, Graphs, Hash Maps.
- **Weeks 5–6:** DP basics, LLD patterns, mock loops (coding + OOD + system design + behavioral).
- Filter LeetCode for **Microsoft-tagged** problems; revise design patterns with use cases; prepare **5–7 STAR stories** anchored on Growth Mindset & measurable impact.

*Last updated: June 2026.*
