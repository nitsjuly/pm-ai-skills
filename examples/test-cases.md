# AI Strategy Evaluator: Test Cases & Evaluation Examples

Use these anonymized scenarios to test the skill and calibrate your expectations.

---

## Test Case 1: Healthcare — Care Coordination

**Scenario Type:** AI-Native candidate (complex, high trust requirements)

### Input

```
Evaluate this AI use case:

**PM context:** PM on a digital health platform for chronic disease management

**Who:** Care coordinators at health systems managing 200-400 patients each with 
chronic conditions. They review clinical dashboards daily for intervention triggers.

**What's broken:** Coordinators manually scan EHR dashboards for lab changes, 
missed appointments, and medication gaps. Takes 2-3 hours/day. They miss patients 
who are silently deteriorating. When they catch issues, it's often too late.

**Success:** AI surfaces a prioritized "intervention list" each morning — patients 
ranked by risk, with recommended action (call, schedule, escalate to physician).

**Constraints:** HIPAA, EHR integration required, care coordinators are clinically 
trained but not technical, health system IT is notoriously slow.
```

### Expected Output Characteristics

| Section | What to Check |
|---|---|
| **Phase 1** | Should recommend AI-Augmented (augment existing workflow) |
| **Phase 2** | Should describe AI-Native vision (proactive care orchestration) |
| **Risk Factor** | Should flag IT/EHR integration as likely wall |
| **Reality Check** | Should note EHR integration timelines are typically underestimated |
| **Sub-tasks** | "Rank by risk" = AI; "Pull lab data" = Deterministic |
| **Next Step** | Should suggest manual mock-up with real patient data |

---

## Test Case 2: B2B SaaS — Expense Management

**Scenario Type:** AI-Augmented candidate (clear existing workflow)

### Input

```
Evaluate this AI use case:

**PM context:** PM at a B2B expense management platform (mid-market focus)

**Who:** Finance teams (2-5 people) at companies with 100-500 employees who 
manually review and categorize expense reports weekly.

**What's broken:** Reviewers spend 4-6 hours/week checking receipts against 
policy, flagging violations, and categorizing expenses. Errors slip through. 
Month-end close is stressful.

**Success:** AI auto-categorizes expenses, flags policy violations with 
explanations, and surfaces a "review queue" of only the edge cases needing 
human judgment.

**Constraints:** SOC2, integrations with major accounting systems, finance 
teams are conservative adopters, competitors already have AI features.
```

### Expected Output Characteristics

| Section | What to Check |
|---|---|
| **Phase 1** | Should recommend AI-Augmented (fits existing weekly review) |
| **Phase 2** | May say "No Phase 2" or suggest real-time policy enforcement |
| **Risk Factor** | Should flag competitive pressure OR conservative adopters |
| **Moat** | Workflow moat should be "Moderate" (users have alternatives) |
| **Build vs Buy** | Should consider "Integrate" given competitive landscape |
| **Next Step** | Should suggest categorizing last week's expenses manually |

---

## Test Case 3: Supply Chain — Quote Configuration

**Scenario Type:** Data-heavy, integration-dependent

### Input

```
Evaluate this AI use case:

**PM context:** PM on a reseller-facing commerce platform

**Who:** IT resellers (small business focused) quoting hardware+software bundles 
to their end customers. Resellers build 15-30 quotes/week, each requiring 
compatibility checks, margin optimization, and vendor incentive stacking.

**What's broken:** Quote configuration takes 45-90 minutes. Resellers make 
margin errors, miss incentive eligibility, and lose deals to faster competitors. 
Platform has SKU data, reseller history, and vendor incentive tables.

**Success:** Reseller describes the customer need in plain English; AI returns 
a quote-ready bundle with margin, incentive callouts, and a one-paragraph 
customer pitch.

**Constraints:** Large SKU catalog, many vendor incentive programs with 
quarterly rule changes, resellers are not technical buyers (they'll churn 
if it's complex).
```

### Expected Output Characteristics

| Section | What to Check |
|---|---|
| **Reality Check** | Should flag data quality (incentive rules likely messy) |
| **Sub-tasks** | "Match SKUs" = Deterministic; "Generate pitch" = AI |
| **Risk Factor** | Should name specific data dependency risk |
| **Brackets** | Should use `[X]` for SKU count, not invent a number |
| **Phase 1** | AI-Augmented (suggest bundles, human validates) |
| **Phase 2** | Conversational quoting, auto-send to customer |

---

## Test Case 4: Operations — Port Scheduling

**Scenario Type:** High-stakes, real-time, on-prem

### Input

```
Evaluate this AI use case:

**PM context:** PM on a port operations platform

**Who:** Terminal operations supervisors at major ports who manually triage 
vessel berthing conflicts during high-congestion windows — typically 2-3 
times daily, under 30-minute decision windows.

**What's broken:** A legacy scheduling system + radio communication with 
pilots + printed spreadsheets. Conflicts are resolved by experience and 
phone calls. Delays cost $50-80K per vessel.

**Success:** The AI surfaces a ranked conflict resolution plan before the 
supervisor even picks up the radio — they validate rather than construct.

**Constraints:** Maritime compliance, multi-stakeholder data (shipping lines, 
terminal operators, customs), latency under 90 seconds, must be deployed 
on-premise at port authority infrastructure.
```

### Expected Output Characteristics

| Section | What to Check |
|---|---|
| **Risk Factor** | Should flag trust + latency + on-prem complexity |
| **Moat** | Governance moat should be "Strong" (compliance + on-prem) |
| **Reality Check** | Should note multi-stakeholder data is a known hard problem |
| **Phase 2** | Should describe autonomous scheduling (big leap) |
| **Build vs Buy** | Should recommend Build (too specialized for vendors) |
| **Next Step** | Should suggest shadowing supervisors during conflict window |

---

## Test Case 5: Negative Case — AI Isn't the Answer

**Scenario Type:** Should recommend "Don't use AI" or "Pass"

### Input

```
Evaluate this AI use case:

**PM context:** PM at a project management SaaS

**Who:** Project managers who need to generate weekly status reports for 
stakeholders.

**What's broken:** PMs spend 30 minutes/week copying task updates from the 
tool into a status report template. It's tedious but straightforward.

**Success:** AI generates the weekly status report automatically from task 
data.

**Constraints:** None significant — standard B2B SaaS.
```

### Expected Output Characteristics

| Section | What to Check |
|---|---|
| **Sub-tasks** | Most should be "Deterministic" (pull data, format) |
| **Build vs Buy** | Should consider "Don't use AI" — templating works |
| **Risk Factor** | Should note this is a feature, not an AI product |
| **Reality Check** | Should flag that 30 min/week may not justify AI complexity |
| **Verdict** | Could be "Pass" or "Pursue with conditions" (validate need) |

---

## Evaluation Rubric

Use this to assess skill output quality:

| Criterion | Good | Needs Improvement |
|---|---|---|
| **Anti-Hallucination** | Uses `[X]` brackets for unknowns | Invents specific numbers |
| **Reality Checks** | 1-2 callouts flagging optimism bias | No Reality Checks present |
| **Risk Factor Specificity** | Names persona, moment, structural reason | Generic ("adoption may be slow") |
| **Phase 1 vs Phase 2** | Clear distinction with triggers | Blurred or missing Phase 2 |
| **Sub-task Accuracy** | Correctly identifies AI vs. Deterministic | Calls everything "AI" |
| **Next Step Concreteness** | Doable this week, specific artifact | Vague ("talk to users") |
| **Formatting** | Bold-first bullets, tables, scannable | Wall of text |

---

## Feedback Template

After running a test case, capture:

```yaml
test_case: "[name]"
date: "[YYYY-MM-DD]"
skill_version: "2.5"

# Output Quality
anti_hallucination: "pass | fail (note specifics)"
reality_checks_present: "yes | no"
risk_factor_quality: "specific | generic | n/a"
phased_recommendation: "clear | unclear | missing"
formatting: "good | needs improvement"

# Accuracy
phase1_mode_correct: "yes | no | debatable"
risk_factor_plausible: "yes | no"
next_step_actionable: "yes | no"

# Notes
what_worked: ""
what_needs_improvement: ""
suggested_skill_changes: ""
```

---

## Should These Be in the Repo?

**Recommendation:** Yes, include as `examples/test-cases.md`

**Why:**
1. **Onboarding:** New users can try realistic scenarios immediately
2. **Calibration:** Shows what "good" output looks like
3. **Contribution guide:** Community can add industry-specific test cases
4. **Regression testing:** When you update the skill, run these to check for regressions

**What NOT to include:**
- Real company names
- Actual internal use cases
- Confidential constraints

These test cases are intentionally generic enough to be public while being realistic enough to be useful.
