# Examples: Healthcare (Skill 1 — AI Strategy Evaluator)

Two cases. One passes. One doesn't.

---

## Case 1: Readmission Risk Scoring (Passes)

**Input:** "We want to add AI that flags patients at high risk of 30-day readmission, surfaced to care coordinators each morning inside the existing care management tool they already use."

---

### Jobs-to-Be-Done

**Functional job:** Start each morning knowing which discharged patients need a proactive outreach call today — without pulling a manual report.

**Emotional/social job:** Feel confident they caught the patients who needed them. Be able to defend the outreach decision in a care review or liability discussion.

**Sub-task breakdown:**

| Sub-task | Type | Notes |
|---|---|---|
| Pull patient discharge data from EHR | Deterministic | Structured query, rule-based |
| Score readmission risk from clinical signals | AI | Large model — requires pattern recognition across diagnosis codes, vitals, social determinants |
| Rank and surface top patients for the day | Deterministic | Threshold-based ranking, no AI needed |
| Log outreach and outcome per patient | Deterministic | Form-based, structured |

---

### Activation & Adoption Risk

**Risk 1 — Trust gap (High):** Care coordinators will not act on a score without understanding why a patient was flagged. Without explainability, the feature becomes a list they manually second-guess — which costs more time than the current workflow.
*Fixable before launch: yes. Add a 2–3 signal summary per patient ("flagged due to: prior readmission within 90 days, no PCP follow-up scheduled, diabetes comorbidity").*

**Risk 2 — EHR integration timeline (Moderate):** Real-time data pull requires HL7/FHIR integration with the EHR. If it ships on a nightly batch, the "morning briefing" use case breaks.
*Fixable: depends on EHR partnership status. Confirm before committing to the workflow.*

---

### Moat Assessment

- **Data moat: Strong** — Model improves on institution-specific readmission patterns (population mix, discharge protocols, local social determinants).
- **Workflow moat: Strong** — Embedded in morning workflow inside the existing tool. High switching friction once care coordinators build a routine around it.
- **Governance moat: Moderate** — HIPAA compliance required; trust in the model's clinical validity is an ongoing maintenance burden competitors share.

Overall: strong moat with a real data advantage. Durable if the institution's data is continuously used to retrain.

---

### Build vs. Buy vs. Integrate

**Integrate.** Foundation model capabilities (risk scoring from clinical signals) are available via third-party clinical AI vendors (Health Catalyst, Arcadia). Build the surrounding product — workflow embedding, explainability layer, outcome feedback loop — on top of an integrated model. Time-to-value matters more than full differentiation at this stage.

---

### Kill Factor

The care coordinator workflow is only as good as the EHR data quality. If discharge data is incomplete or delayed, the model surfaces the wrong patients — and one bad week of missed flags destroys trust that takes months to rebuild. Data quality SLA from the EHR integration is the dependency nobody is tracking.

---

### Bottom Line

**Pursue with conditions.** The job is real, the moat is strong, and the workflow fit is high. Three prerequisites before launch: (1) confirm real-time EHR data availability, (2) add per-patient signal explanation, (3) run a Wizard-of-Oz test with 2–3 care coordinators using manually generated scores before writing model code.

---
---

## Case 2: Ambient Clinical Note Generation (Does Not Pass as Scoped)

**Input:** "We want to add AI that listens to patient-physician conversations and auto-generates clinical notes, reducing documentation burden for physicians."

---

### Jobs-to-Be-Done

**Functional job:** Complete clinical documentation without manual typing after each visit — while still in the room with the patient.

**Emotional/social job:** Reclaim the cognitive space currently spent on documentation during the visit. Be present with the patient instead of looking at a screen.

**Sub-task breakdown:**

| Sub-task | Type | Notes |
|---|---|---|
| Capture audio of clinical encounter | Deterministic | Consent, recording infrastructure, legal sign-off |
| Transcribe speech to text | AI | Small model (Whisper-class) — commodity, fast |
| Extract clinical entities and structure note | AI | Large model — requires clinical reasoning, SOAP format, specialty awareness |
| Physician review and attestation | Deterministic (HITL required) | Physician must review before note enters EHR — not optional |

---

### Activation & Adoption Risk

**Risk 1 — Consent and legal infrastructure (Critical):** Ambient recording requires explicit patient consent per encounter. This is a legal and workflow design problem that must be solved before any model work begins. In some states, two-party consent laws apply.
*Not fixable post-launch. Consent UX and legal sign-off are prerequisites.*

**Risk 2 — Specialty variance (High):** A note generation model that works for primary care fails for surgical oncology. If the first rollout covers the wrong specialty mix, physician rejection spreads fast.
*Fixable: start with one specialty, validate deeply before expanding.*

---

### Moat Assessment

- **Data moat: Weak** — Nuance DAX, Abridge, and Nabla are already trained on millions of clinical encounters. A new entrant's data moat takes years to close.
- **Workflow moat: Moderate** — Deep EHR integration creates switching costs, but competitors (Nuance/Microsoft) have this too.
- **Governance moat: Weak** — All vendors face the same HIPAA and attestation requirements.

Overall: weak moat against entrenched players. This is a feature, not a platform, for anyone entering now.

---

### Build vs. Buy vs. Integrate

**Integrate or partner.** Building from scratch against Nuance DAX (now Microsoft-backed) and Abridge (UPMC partnership) is a capital and data disadvantage. Integrate a best-in-class ambient model via API and build differentiation in EHR embedding, specialty tuning, and the physician review workflow.

---

### Kill Factor

Physician trust is binary. The first time a note contains a clinical error that makes it into the EHR — even one — adoption freezes organization-wide. The attestation step is not a UX nicety; it's the trust mechanism. If the workflow is designed to make attestation feel optional or fast, it will be skipped, and the first error will be catastrophic.

---

### Bottom Line

**Pass as currently scoped (build from scratch).** The job is real and the demand is genuine — but the competitive moat is weak against Microsoft-backed Nuance and well-funded specialists. Reframe as an integration play: embed a best-in-class ambient model, differentiate on specialty tuning and EHR workflow. That's a credible product. Building the core model from scratch is not.
