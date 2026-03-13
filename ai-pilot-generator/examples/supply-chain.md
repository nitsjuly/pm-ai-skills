# Example: Supply Chain Demand Forecast Explanation (Skill 2 — AI Pilot Generator)

**Input (from Skill 1 output):**
JTBD: Supply chain planners walk into Monday's S&OP meeting able to explain why the forecast changed — without Sunday-night prep. Kill factor: confidently wrong explanations destroy trust faster than no explanation. Pursue with conditions.

---

## Recommended Pilot Tasks

### Task 1: Weekly Forecast Delta Summary (Start Here)
Surface a plain-language summary of the top 2–3 reasons the week-over-week forecast changed, for the planner's 5 highest-volume SKUs.

- **HITL.** Planner reviews before taking the summary into an S&OP meeting. Trust isn't established yet — and one wrong explanation in front of leadership is a trust-killer. Make the review surface prominent, not buried.
- **Starting point:** Push as a Monday 6am email digest (matches where planners actually start their week, before they open the dashboard). Link back to the full dashboard for drill-down.

---

### Task 2: Anomaly Explanation on Demand
When a planner clicks on an anomalous SKU in the forecast dashboard, AI generates a one-paragraph explanation of likely drivers on demand.

- **HITL (light).** The explanation is advisory — the planner decides whether to act on it. No approval gate needed, but include a "flag as incorrect" button from day one. That feedback loop is the training signal.
- **Starting point:** Inline in the existing forecast dashboard, triggered by clicking an anomaly indicator. No new surface — no new login, no new habit required.

---

### Task 3: Pre-S&OP Briefing Doc (Phase 2 — not the pilot)
AI generates a structured one-pager summarizing forecast changes, top drivers, and recommended discussion points for the S&OP meeting.

- **HITL required.** This goes to leadership. Planner edits before distributing.
- **Why phase 2:** This only works if Task 1 has established trust in the explanation quality. Don't ship this first.

---

## Success Metrics

| Task | Good Metric | Bad Metric |
|---|---|---|
| Forecast delta summary | % of planners who reference the summary in S&OP (observed, not self-reported) | Open rate on the Monday email |
| Anomaly explanation | % of clicked anomalies where planner takes an action within 48hrs | Clicks on the explanation |
| Briefing doc | % of S&OP meetings where AI-generated doc is used with <30% edits | Doc generation volume |

**Why "open rate" is a bad metric for Task 1:**
Week 1 opens will be high — novelty. Week 4 opens tell you whether it became a habit. Measure return open rate at weeks 3 and 6, not launch week.

**The metric that predicts survival past month one:**
Did the planner use the explanation to answer a question in the S&OP meeting — yes or no? Self-reported is fine for the pilot. Observable is better. Add one question to your biweekly planner check-in: "Did the forecast summary change anything you said or did this week?"

---

## Discovery Script

Use this before building — or before expanding from pilot to GA.

**Opening (30 seconds):**
> "I want to understand how you prep for S&OP today — not pitch anything, just understand the actual workflow. Walk me through what last Monday looked like, from when you woke up to when the meeting started."

**Q1:** What's the first thing you look at when you sit down? What are you trying to answer before the meeting?

**Q2:** When the forecast moves significantly week-over-week, how do you figure out why? Walk me through the steps.

**Q3:** Has there been a time when you walked into S&OP and got a question you couldn't answer confidently? What happened?

**Q4:** If you had a tool that gave you a plain-language explanation of why the forecast changed — what would make you trust it enough to repeat it in the meeting?

**Q5 (optional):** What's the format you'd actually want — email, dashboard alert, something else? When do you want to see it?

**Closing:**
> "If this worked exactly as you hoped, what would be different about your Monday morning? What would you stop doing?"

---

## Relevant AI Adoption Patterns (generated from JTBD context)

1. **Forecast explanation (this case)** — AI narrates model output changes; human uses in planning meeting. Close analogs: financial variance analysis tools, clinical deterioration explainability in EHR.

2. **Exception-based briefings** — AI surfaces only the anomalies that matter, not all the data. Reduces cognitive load from dashboard overload. Used in: retail replenishment, demand sensing for CPG.

3. **S&OP meeting prep automation** — AI aggregates cross-functional signals (sales, ops, finance) into a pre-read. Human edits. Closest public analog: Anaplan's AI-assisted scenario modeling.

4. **Planner knowledge assistant** — AI answers "why did this SKU spike last April?" from historical data. Replaces tribal knowledge. Used in: distribution and logistics planning.

5. **Confidence-banded forecast display** — AI shows not just the forecast but the confidence interval, with plain-language explanation of what would cause the upper vs. lower bound. Changes the conversation from "what's the number" to "what's the risk."
