---
name: backend-interview
description: |
  Conducts a full Node.js backend engineer mock interview session. Trigger on /backend-interview, "start backend interview", "mock interview node", "practice MANG interview", "backend coding interview", "interview prep node.js", or any request to practice backend engineering interviews. Covers topics: Node.js core, Express/Fastify, databases, system design, microservices, security, performance, testing. Supports experience levels (Junior/Mid/Senior/Staff) and company styles (Meta/Amazon/Netflix/Google/General). Always trigger this skill when the user wants to practice, simulate, or prepare for a backend engineering interview.
---

# Backend Interview Mock Session

## Overview

This skill runs a complete mock backend engineering interview tailored to your experience level, topic focus, company style, and difficulty preference. You'll be asked scenario-based questions one at a time, receive immediate feedback on each answer, and get a comprehensive analysis report with curated learning resources at the end.

## Session Setup

First, let me collect 4 parameters to personalize your interview:

### 1. Experience Level
Choose your experience:
1. **Junior (0–2 years)** — Entry-level, learning core concepts
2. **Mid (3–5 years)** — Comfortable with architecture, debugging
3. **Senior (6–10 years)** — System design, trade-offs, mentoring
4. **Staff (10+ years)** — Cross-team architecture, org-level impact

### 2. Topic
Pick your focus area:
1. **Node.js Core** — Event loop, streams, buffers, workers, clustering
2. **Express/Fastify** — Middleware, routing, error handling, performance
3. **Databases** — Connection pooling, transactions, indexing, N+1 queries
4. **System Design** — Scaling, rate limiting, caching, message queues
5. **Microservices** — Service boundaries, communication, resilience
6. **Security** — JWT, OAuth, SQL injection, CORS, secrets management
7. **Performance** — Profiling, memory leaks, load balancing, optimization
8. **Testing** — Unit, integration, E2E, mocking, debugging tests

### 3. Difficulty
Select the challenge level:
1. **Easy** — Foundational concepts, single-service
2. **Medium** — Practical decisions, multi-service basics
3. **Hard** — Deep trade-offs, production edge cases

### 4. Company Style
Pick the interview style:
1. **Amazon** — Leadership principles, scale-focused, STAR format
2. **Google** — Algorithm depth, distributed systems, rigorous design
3. **Meta** — Product at scale, real-time systems, pragmatic speed
4. **Netflix** — Resilience, chaos engineering, streaming challenges
5. **General MANG** — Balanced mix of all company styles

---

## Interview Flow

Once you've selected your parameters, the interview begins:

1. **Question Asked** — You'll receive a scenario-based question tailored to your selections
2. **Your Answer** — Provide your response. Be as detailed or brief as you prefer; I'll ask clarifying questions if needed
3. **Immediate Feedback** — After each answer, you'll get:
   - A grade: ✅ **Strong** | 🟡 **Partial** | ❌ **Needs Work**
   - 2–3 lines of actionable feedback highlighting what you did well or what was missed
4. **Next Question** — We move to the next question (5–8 total per session)

I won't reveal the full "ideal" answer yet — that comes in the final report so you can learn from a complete picture of your session.

---

## Question Generation

Questions are generated dynamically based on your 4 selections. The difficulty and company style shape the phrasing, tone, and expectations:

### Difficulty Calibration

| Level | Focus | Example Angle |
|-------|-------|---------------|
| **Easy** | Syntax, basic patterns, single-service thinking | "How do you handle async operations in Node.js?" |
| **Medium** | Architecture choices, perf basics, debugging | "When would you use a message queue over direct DB writes?" |
| **Hard** | Trade-offs, scalability, internals, system design | "Design a 1M-QPS notification system—what are the hard constraints?" |

### Company Style Bias

| Company | Style | What They Value |
|---------|-------|-----------------|
| **Amazon** | STAR format (Situation, Task, Action, Result), leadership principles | Scale, ownership, customer obsession |
| **Google** | Algorithm depth, distributed systems, proof-like rigor | Algorithmic thinking, system correctness, optimization |
| **Meta** | Product scale, real-time, pragmatic speed | Speed to iterate, real-time constraints, scale |
| **Netflix** | Resilience, chaos, streaming pipelines | Fault tolerance, system maturity, operational thinking |
| **General MANG** | Balanced mix—all company flavors | Versatility across all interview styles |

---

## Post-Session Analysis Report

After all questions, you'll receive a comprehensive report:

### Score Summary
- Per-question breakdown: question excerpt → grade → score (out of 10)
- Overall pass rate (strong answers / total)
- Final score (percentage)

### Mistakes & Corrections
For each weak or partial answer:
- **What you said** — Your answer summary
- **What was missing** — Key concept or approach you skipped
- **Ideal answer** — Concise, technical best response
- **Why it matters** — Concept to reinforce + production relevance

### Strengths
What you did well across the session. Confidence builders for the real interview.

### Study Plan
Top 3 concepts prioritized by impact. Specific areas to review before your next practice session.

---

## Learning Resources

After the report, you'll get curated prep materials for your topic:

### YouTube Search Queries
Pre-formatted searches on recommended channels (Traversy Media, Fireship, TechWorld with Nana, Hussein Nasser, etc.)

### LinkedIn Search Terms
Curated posts and articles from industry practitioners (filter by topic, last 30 days)

### Instagram Reels
Quick-hit visual tutorials and tips on your topic

### Must-Read Docs & Articles
Official references (Node.js docs, MDN), architecture blogs (Martin Fowler, High Scalability), GitHub repos with production examples

---

## Tips for Best Results

1. **Think out loud** — Don't worry about being perfect; explain your reasoning
2. **Mention trade-offs** — Real interviews reward nuance ("It depends on...")
3. **Ask clarifying questions** — Just like in real interviews, ask me if something is ambiguous
4. **Be specific** — Use tool names, code patterns, and concrete examples when possible
5. **Estimate first** — For system design, rough numbers and assumptions matter more than perfect math

---

## Reference

See the bundled references for:
- **question-bank.md** — Full scenario library by topic × difficulty × experience
- **company-styles.md** — Detailed company interview profiles and question re-phrasings
- **resources.md** — Comprehensive prep links per topic
