# Company Interview Styles — MANG & General

Each MANG company has a distinct interview style, question framing, and evaluation criteria. This reference guides question generation and feedback to match company expectations.

---

## Amazon

### Interview Structure
- **Format:** Behavioral + technical (often interleaved)
- **Rounds:** 1–2 technical rounds (45 min each)
- **Style:** STAR format (Situation, Task, Action, Result) embedded in answers
- **Evaluation:** Leadership principles weighted heavily

### Leadership Principles (Expect These in Questions)
1. **Customer Obsession** — Think about impact, not just code
2. **Ownership** — You own outcomes end-to-end
3. **Invent and Simplify** — Innovative solutions, but pragmatic
4. **High Standards** — Quality matters, even under time pressure
5. **Bias for Action** — Move fast, iterate, learn

### Question Framing
- "Tell me about a time when..."
- "Describe a situation where you had to..."
- "Walk me through how you'd approach..."
- Often include **scale:** "How would you design this for 1B users?"

### Example Re-Phrasings
**Generic Q:** How do you optimize database queries?
**Amazon Q:** Tell me about a time you improved database performance at scale. Walk me through the situation, what you did, and the business impact. How did your leadership principles guide your approach?

**Generic Q:** How would you design a notification system?
**Amazon Q:** We need a notification system for Prime members (100M users). You own this end-to-end. Tell me about your approach—what would you consider first? How would you measure success? What trade-offs would you make?

### What They Value
- **Scale thinking** — Comfortable with large numbers
- **Pragmatism** — Solutions that work, even if not perfect
- **Ownership mentality** — You follow through
- **Customer impact** — Always tie back to business value
- **Bias for action** — Prototype quickly, learn fast

### Red Flags
- Over-engineering for unproven use cases
- Waiting for perfect information before acting
- Blaming others or external factors
- Lack of metrics or success criteria

---

## Google

### Interview Structure
- **Format:** Algorithmic + system design (depth-focused)
- **Rounds:** 2–3 technical rounds (45 min each)
- **Style:** Whiteboard / deep dive with follow-up questions
- **Evaluation:** Algorithmic rigor, distributed systems understanding, correctness proof

### Core Themes
1. **Algorithmic Thinking** — Complexity analysis (time, space), optimality
2. **Distributed Systems** — Understanding of consensus, fault tolerance, scaling
3. **Correctness** — Proofs, edge cases, why your solution works
4. **Optimization** — Iterative improvement, not settling on first solution

### Question Framing
- "Design [system]. What are the hard constraints?"
- "Prove this approach works. What are edge cases?"
- "Can you optimize this further? What's the lower bound?"
- Expect deep probing on **correctness** and **complexity**

### Example Re-Phrasings
**Generic Q:** How do you handle distributed transactions?
**Google Q:** You need a distributed transaction system across 5 data centers with network partitions. Define the consistency model you'd provide. Prove it handles your constraints. What about Byzantine failures? What's the minimum message complexity for your solution?

**Generic Q:** Design a caching layer.
**Google Q:** Design a distributed cache for 10K servers, 1M requests/sec. You have 1TB cache. What's your eviction policy? Prove it minimizes cache misses under your access pattern. How do you handle the thundering herd on cache miss?

### What They Value
- **Algorithmic rigor** — Complexity analysis, proofs
- **Distributed systems depth** — Consensus, fault models, Byzantine failures
- **Optimization mindset** — Iterate on solutions, push lower bounds
- **Edge cases** — Think deeply about failure modes
- **Correctness** — Can you justify why your approach works?

### Red Flags
- Hand-waving without proof
- Not analyzing complexity
- Ignoring edge cases or failure modes
- Settling on first solution without optimization
- "It should work" without rigorous justification

---

## Meta

### Interview Structure
- **Format:** Product-focused system design + pragmatism
- **Rounds:** 1–2 technical rounds (45 min each)
- **Style:** Problem-solving under constraints, real-time systems
- **Evaluation:** Speed, pragmatism, product intuition, scale

### Core Themes
1. **Speed at Scale** — Move fast, optimize later if needed
2. **Real-Time Systems** — Latency guarantees matter
3. **Product Intuition** — Understand user experience
4. **Pragmatic Trade-Offs** — Choose the right tool, not the fanciest one
5. **Operational Excellence** — Systems that are easy to run and debug

### Question Framing
- "How would you build this for real at Meta scale?"
- "What's the MVP? How do you iterate?"
- "Where would you cut corners to ship faster?"
- Focus on **real-world constraints** and **operational concerns**

### Example Re-Phrasings
**Generic Q:** Design a real-time notification system.
**Meta Q:** We need to push 100M notifications/sec to mobile users. Some must be delivered <100ms. Design this—but first, what's the minimum viable system? What would you ship in week 1 vs. week 4? How do you monitor and debug in production?

**Generic Q:** How do you optimize a slow endpoint?
**Meta Q:** An endpoint serving the feed is at p99 = 2 seconds (unacceptable). You have 1 week to fix it. What's your investigation approach? What would you optimize first? How do you validate the fix without breaking other things?

### What They Value
- **Speed to market** — MVP thinking, iteration over perfection
- **Real-time performance** — Latency awareness, tail percentiles
- **Operational simplicity** — Easy to debug, monitor, operate
- **Data-driven decisions** — Metrics, A/B testing, validation
- **Pragmatic choices** — Right tool for the job, not fanciest

### Red Flags
- Over-engineering for unproven needs
- Not thinking about operational costs
- Ignoring latency / tail percentiles
- Complex systems when simple would work
- Not considering iteration and learning

---

## Netflix

### Interview Structure
- **Format:** Resilience + streaming systems focused
- **Rounds:** 2 technical rounds (45 min each)
- **Style:** Failure scenarios, chaos thinking
- **Evaluation:** Resilience mindset, operational depth, streaming scale

### Core Themes
1. **Resilience** — Assume everything fails; design recovery
2. **Chaos Engineering** — Can you intentionally break it and survive?
3. **Streaming at Scale** — Handling millions of concurrent connections, billions of requests
4. **Operational Maturity** — Monitoring, alerting, incident response
5. **Cost Efficiency** — Streaming is expensive; optimize margins

### Question Framing
- "How does this system behave when [failure]?"
- "Walk me through an incident you've handled."
- "How would you chaos-test this design?"
- "What's the cost of running this? Can you optimize?"

### Example Re-Phrasings
**Generic Q:** Design a message queue.
**Netflix Q:** We use Kafka for distributed streaming. 1M topics, 10K partitions, 100M messages/sec. A broker fails—what happens? What about a network partition? A Zookeeper quorum loss? Walk me through your recovery strategies. How do you minimize data loss and latency impact?

**Generic Q:** How would you handle a DDoS attack?
**Netflix Q:** Our streaming service is under DDoS: 10M bogus requests/sec. How do you mitigate? Your mitigation itself might fail. How do you handle cascading failures? What's your recovery time? Who decides to trigger emergency mitigation (cost/availability trade-off)?

### What They Value
- **Failure mode thinking** — Enumerate, prepare for, test each
- **Operational maturity** — Monitoring, alerting, runbooks
- **Resilience** — Graceful degradation, circuit breakers, fallbacks
- **Chaos engineering** — Actively testing failure scenarios
- **Cost awareness** — Scale costs money; optimize thoughtfully

### Red Flags
- Happy path only ("it should work")
- No failure mitigation strategy
- Lack of monitoring / observability
- "It's fine, we can handle it" without evidence
- Not considering operational costs

---

## General MANG

### Interview Style
A balanced mix of all four companies. No single bias, but expect:
- **Technical depth** (Google-like)
- **Scale thinking** (Amazon-like)
- **Pragmatism and speed** (Meta-like)
- **Resilience awareness** (Netflix-like)

### Question Framing
- Straightforward technical questions
- Expect you to clarify requirements and trade-offs
- Value clarity of thought over buzzwords
- Want to see your reasoning process

### What They Value
- **Clear communication** — Explain your thinking
- **Trade-off awareness** — Understand costs/benefits
- **Balanced solutions** — Not over/under-engineered
- **Learning mindset** — Ask questions, iterate
- **Fundamentals** — Strong CS foundation

### Example Re-Phrasings
**Generic Q:** How would you scale a database?
**General MANG Q:** We need to scale our user database. First, what are the constraints? Traffic? Data size? Geography? Read/write ratio? Once we understand that, what approaches would you consider? What are the trade-offs?

---

## Applying Company Style in Interview

### For Question Generation
1. **Reframe questions** using company terminology and concerns
2. **Embed evaluation criteria** — Amazon wants STAR, Google wants proofs, Meta wants speed, Netflix wants resilience
3. **Include scale/constraints** specific to company focus
4. **Probe areas** the company cares about most

### For Feedback & Scoring
1. **Evaluate by company lens** — What would they think of this answer?
2. **Highlight alignment** — "You mentioned ownership, which Amazon values" or "You proved correctness, Google appreciates that"
3. **Identify gaps** — "You didn't mention failure scenarios; Netflix would have wanted that" or "Opportunity to discuss complexity analysis here"
4. **Calibrate difficulty** — Adjust follow-up questions to match company rigor level

### Example Session Feedback (by Company)

**Amazon Feedback (if weak answer):**
"You outlined a solution, but didn't focus on ownership or customer impact. Amazon would ask: How do you own this end-to-end? What's the customer impact? How do you measure success?"

**Google Feedback (if weak answer):**
"Your solution works, but you didn't analyze complexity or edge cases. Google would probe: What's the time complexity? Space complexity? Prove it handles Byzantine failures."

**Meta Feedback (if weak answer):**
"You went for a complex architecture. Meta would ask: What's the MVP? Can you ship something in week 1? Where would you cut corners to move faster?"

**Netflix Feedback (if weak answer):**
"You didn't discuss failures. Netflix would ask: What happens when [component] fails? How do you recover? Can you test this chaos scenario?"
