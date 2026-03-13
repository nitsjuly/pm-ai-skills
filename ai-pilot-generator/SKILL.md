---
name: ai-pilot-generator
description: "Generates AI pilot plans from a strategy evaluation. Use when a PM needs next steps after evaluating an AI use case: pilot tasks, HITL vs. automated guidance, success metrics, and a discovery script."
---

# AI Pilot Generator

**Turns a JTBD + risk assessment into an actionable next-step plan.**

> Pairs with `ai-strategy-evaluator`. You can paste its output directly and ask "what do I do next?"

## When to use this skill

Invoke when a PM or product leader asks any of the following — or anything semantically close:

"next steps for this AI feature" · "how do I pilot this" · "what should I test first" · "how do I validate this AI idea" · "pilot plan for AI" · "HITL vs automated" · "human in the loop AI" · "success metrics for AI feature" · "how to run discovery for AI" · "discovery script for AI interviews" · "how do I know if this AI feature is working" · "what's the right metric" · "vanity metrics AI" · "how to test AI before building it" · "quick win for AI" · "low-risk AI pilot" · "high-ROI AI task" · "what to build first" · "how to sequence AI rollout" · "enterprise AI pilot" · "AI adoption plan" · "what questions to ask users about AI features" · "interview script AI" · "AI feature discovery" · "how to measure AI adoption"

Also triggers when someone pastes output from `ai-strategy-evaluator` and asks what to do next.

*Framework by Nithya Chandrasekaran — [linkedin.com/in/nithyach](https://linkedin.com/in/nithyach)*

---

## Intake

If the PM has already provided a JTBD (from Skill 1 output or their own description), use it. If context is thin, ask:

> What's the core job-to-be-done you're trying to enable with AI? And who's the user — roughly?
> *e.g., "Procurement managers who want to flag late purchase orders without manual spreadsheet work"*

That's all you need to generate a useful pilot plan. More context = more specific output.

---

## Output Framework

Produce an **action-focused plan** structured as follows. Use headings, bullets, and tables where useful.

---

### 1. Recommended Pilot Tasks (2–3 tasks)

Identify 2–3 specific sub-tasks from the JTBD that are:
- Repetitive (happen weekly or more)
- Bounded (clear input/output, not open-ended)
- Low-blast-radius if wrong (failure doesn't damage trust catastrophically on the first attempt)

For each task, provide:

**Task name**
- **HITL or Automated?** Choose one and give a one-sentence rationale.
  - HITL when: output goes into a high-stakes decision, user trust isn't established yet, or errors are hard to reverse.
  - Automated when: output is advisory/informational, errors are low-cost, and the user's first instinct is to trust the output.
- **Starting point suggestion:** Where in the existing workflow does this plug in? What's the trigger and the surface?

---

### 2. Success Metrics (1 good, 1 bad per task)

For each pilot task:

| Task | Good Metric | Bad Metric |
|---|---|---|
| Task name | Metric that measures actual behavior change | Metric that looks good but doesn't predict adoption |

**Good metric principles:**
- Measures action taken as a result of AI output (not just views or opens)
- Has a baseline to compare against
- Is observable within 2–4 weeks of launch

**Bad metric examples to call out explicitly:**
- Feature adoption rate (week 1 is always high — novelty, not habit)
- Model accuracy on a test set (doesn't predict whether users act on the output)
- Time saved (self-reported, not observed)

---

### 3. Discovery Script

A starter set of 3–5 interview questions for customer or internal discovery. Ready to use or adapt. Focus on surfacing:
- The current workflow in detail (what they actually do, not what they say they do)
- The moment of friction (when does the current approach fail them?)
- The trust question (what would make them act on AI output without checking it manually?)

Format as a usable script:

> **Opening (30 seconds):**
> "I want to understand how you [task] today — not pitch anything, just learn the workflow. Walk me through what last [Monday / quarter / cycle] actually looked like."

> **Q1:** ...
> **Q2:** ...
> **Q3:** ...
> **Closing:** "If this tool existed and worked perfectly, what would you be able to do differently in your next [meeting / cycle / review] that you can't do today?"

---

### 4. Enterprise AI Adoption Examples (Optional)

If the JTBD context is strong enough, generate 5–10 examples of enterprise AI adoption patterns that are directly analogous to the use case. Focus on:
- Same user type or workflow type
- Similar trust/activation challenges
- Real public deployments where outcome data exists

If context is thin, fall back to this reference list of patterns that apply across most enterprise AI use cases:

1. **Morning briefing automation** — AI surfaces top 3–5 actionable items from overnight data. User reviews and acts. (CRM, supply chain, clinical)
2. **Exception flagging** — AI flags anomalies from a baseline; human decides on response. (Finance, operations, quality control)
3. **Draft generation + human edit** — AI produces a first draft (note, summary, email); human reviews and sends. (Clinical, legal, sales)
4. **Semantic search over institutional data** — AI replaces keyword search for internal knowledge bases. (HR, legal, engineering)
5. **Classification + routing** — AI categorizes inbound requests and routes them; human handles edge cases. (Support, procurement, compliance)
6. **Forecast explanation** — AI narrates why a model output changed; human uses it in a meeting. (Finance, supply chain, marketing)
7. **Compliance pre-check** — AI flags potential issues before a human submits or approves. (Legal, procurement, clinical)
8. **Meeting summarization + action item extraction** — AI produces a structured summary; human edits and distributes. (Sales, product, executive)
9. **Onboarding acceleration** — AI answers new-user questions in context of their specific workflow. (SaaS, internal tools)
10. **Risk scoring with explanation** — AI scores entities (customers, patients, vendors) and explains top drivers. Human decides on action. (Clinical, financial services, supply chain)

---

## Output Principles

- Pilot tasks should feel like something a PM could propose in a sprint planning meeting tomorrow
- Every metric should have a baseline and a measurement method, not just a name
- The discovery script should be copy-paste ready — no placeholder questions
- If examples are generated dynamically, ground them in real public deployments where possible
