# Examples: Developer Tooling & Supply Chain (Skill 1 — AI Strategy Evaluator)

---

## Case 3: Code Migration Assistance (Developer Tooling — Passes)

**Input:** "We're a developer platform. We want to add AI that helps engineering teams migrate legacy codebases to newer frameworks or languages. Engineers currently do this manually — it's slow, high-error, and nobody wants to own it."

---

### Jobs-to-Be-Done

**Functional job:** Complete a legacy-to-modern migration with 80%+ of the mechanical work handled automatically, so the engineering team focuses on edge cases and validation rather than line-by-line translation.

**Emotional/social job:** Ship the migration without it becoming the 6-month project nobody wants their name on. Demonstrate to leadership that the platform investment reduced a high-dread work type.

**Sub-task breakdown:**

| Sub-task | Type | Notes |
|---|---|---|
| Parse and map existing codebase structure | Deterministic | AST analysis, rule-based dependency mapping |
| Generate migrated code for each module | AI | Large model — requires language reasoning, framework idiom awareness, context across files |
| Flag untranslatable patterns for human review | AI + Deterministic | Model identifies, rule-based threshold triggers HITL queue |
| Engineer reviews and approves flagged sections | Deterministic (HITL required) | Never fully automated — code enters production under human attestation |

---

### Activation & Adoption Risk

**Risk 1 — Trust calibration (High):** Engineers will over-rely on AI output early, then over-reject it after the first bad migration. The HITL queue design determines whether trust stabilizes or collapses. Make the "flag for review" surface prominent — not a footnote.

**Risk 2 — Context window limits (Moderate):** Large migrations span hundreds of files. Models lose coherence across long contexts. A chunking strategy with cross-file dependency tracking is a technical prerequisite, not a v2 item.

---

### Moat Assessment

- **Data moat: Moderate** — Migration patterns improve with customer codebase exposure, but foundation models already have significant training on public code.
- **Workflow moat: Strong** — If the tool is embedded in the CI/CD pipeline with reviewer tooling, it becomes the migration workflow. Switching means re-training the team.
- **Governance moat: Weak** — Low regulatory surface for developer tooling.

Overall: moderate moat, primarily in workflow embedding. Durable if the review tooling is genuinely better than manual alternatives.

---

### Build vs. Buy vs. Integrate

**Integrate.** Foundation model code generation (GPT-4o, Claude, Gemini) handles the core translation task. Build differentiation in: (1) cross-file context management, (2) the HITL review interface, and (3) migration telemetry that learns from engineer corrections.

---

### Kill Factor

If the first migration attempt on a real customer codebase produces output that requires more review time than a manual migration would have, adoption dies in the pilot. The first customer case must be a high-confidence win — start with well-defined migration paths (e.g., Python 2 → 3, jQuery → React) before taking on ambiguous multi-framework migrations.

*Reference: Spotify documented 90% reduction in engineering time on code migrations using AI-assisted tooling embedded in existing developer workflows — grounded in workflow integration, not model quality alone.*

---

### Bottom Line

**Pursue.** Real job, strong workflow moat, clear integration path. Start with the highest-confidence migration type, instrument the HITL review queue from day one, and measure engineer correction rate as the primary quality signal.

---
---

## Case 4: AI-Generated Demand Forecast Explanation (Supply Chain — Pursue with Conditions)

**Input:** "We're a supply chain SaaS platform. Our customers already have AI-generated demand forecasts. We want to add a feature that explains, in plain language, why the forecast changed week-over-week — surfaced to supply chain planners each Monday."

---

### Jobs-to-Be-Done

**Functional job:** Walk into Monday's S&OP meeting able to explain why the forecast moved — without spending Sunday night pulling data and building a slide.

**Emotional/social job:** Maintain credibility with the business when the forecast is questioned. Not be the person who says "the model said so."

**Sub-task breakdown:**

| Sub-task | Type | Notes |
|---|---|---|
| Detect week-over-week forecast delta by SKU/region | Deterministic | Structured calculation, rule-based |
| Identify top drivers of the delta (promotions, weather, supplier signals) | AI | Large model — requires pattern attribution across multiple signal types |
| Generate plain-language explanation | AI | Small model sufficient — structured narrative from attributed drivers |
| Surface in planner dashboard, Monday morning | Deterministic | Scheduled job, notification trigger |

---

### Activation & Adoption Risk

**Risk 1 — Attribution accuracy (Critical):** If the explanation confidently names the wrong driver, planners stop trusting it — and start trusting it less than the raw forecast they had before. Attribution explainability is load-bearing, not decorative.

**Risk 2 — Planner workflow fit (Moderate):** S&OP planners often prep in their own tools (Excel, Google Sheets). A dashboard notification they don't see Monday morning defeats the use case. Confirm where they actually start their week.

---

### Moat Assessment

- **Data moat: Strong** — Explanation quality improves with customer-specific signal history (their promotions, their supplier patterns, their anomaly types). Generic explanations are commodity; institution-specific explanations are not.
- **Workflow moat: Moderate** — If embedded in the S&OP workflow, it becomes the pre-meeting briefing. Replaceable but sticky.
- **Governance moat: Weak** — No significant regulatory surface.

---

### Build vs. Buy vs. Integrate

**Build.** The core value is the attribution layer on top of the customer's own forecast model — not the language generation. That attribution logic is proprietary and institution-specific. Language generation can use any foundation model. Build the attribution; integrate the narration.

---

### Kill Factor

The explanation will be confidently wrong on some Mondays. A planner who walks into an S&OP meeting with a wrong explanation — and gets called out — will never use the feature again. The kill factor is not accuracy on average; it's accuracy on the Monday that matters. A confidence indicator ("high confidence" vs. "multiple drivers, review manually") is not optional.

---

### Bottom Line

**Pursue with conditions.** The job is real, the data moat is strong, and the workflow fit is high. Two prerequisites: (1) build a confidence signal into every explanation, not just the output, and (2) run a Wizard-of-Oz test — have a human analyst generate the explanation manually for 4 weeks and measure whether planners act on it before building the model.
