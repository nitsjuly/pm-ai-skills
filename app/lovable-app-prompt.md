# Lovable App Prompt: AI Strategy Evaluator v2.5

> Copy this entire prompt into [Lovable.dev](https://lovable.dev) to generate a production-ready app.

---

## App Overview

**One-liner:** A thinking partner that helps PMs determine if AI is the right fit for their use case — before they commit it to the roadmap.

Build an **AI Strategy Evaluator** — a web app that helps Product Managers evaluate AI use cases before committing them to their roadmap. The app uses the Anthropic Claude API to run evaluations based on a structured PM framework.

**Core requirements:**
- User authentication (magic link email)
- Multi-step evaluation wizard (evaluates BOTH AI-Augmented and AI-Native, recommends phased approach)
- Claude API integration with $20 budget cap
- Anti-hallucination: uses `[X]` brackets for unknown metrics
- Reality Check callouts for optimism bias
- Two-tier feedback system (User vs Admin)
- Pilot planning handoff
- Light, professional UI suitable for enterprise users
- Mobile responsive

---

## Tech Stack

- **Frontend:** React + TypeScript + Tailwind CSS
- **Backend:** Supabase (auth, database, edge functions)
- **AI:** Anthropic Claude API (claude-sonnet-4-20250514)
- **Notifications:** Resend (for budget alerts)

---

## Database Schema (Supabase)

```sql
-- Users (handled by Supabase Auth)

-- Evaluations
create table evaluations (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references auth.users(id),
  created_at timestamp with time zone default now(),
  
  -- Inputs (stored for admin export only, encrypted at rest)
  input_user_task text,
  input_current_solution text,
  input_success_state text,
  input_constraints text,
  
  -- Outputs (evaluates BOTH modes, recommends phased approach)
  phase1_mode text check (phase1_mode in ('augmented', 'native')),
  phase2_exists boolean default true,
  verdict text check (verdict in ('pursue', 'pursue-with-conditions', 'pass')),
  evaluation_json jsonb,
  
  -- Pilot handoff
  proceeded_to_pilot boolean default false,
  requested_expansion boolean default false,
  
  -- Token tracking
  input_tokens integer,
  output_tokens integer,
  cost_usd numeric(10, 6),
  
  -- Feedback (user-facing)
  feedback_rating text check (feedback_rating in ('positive', 'negative')),
  feedback_surfaced_new text check (feedback_surfaced_new in ('yes', 'no', 'not_sure')),
  feedback_risk_factor_useful text check (feedback_risk_factor_useful in ('useful', 'not_useful', 'too_generic')),
  feedback_would_share text check (feedback_would_share in ('yes_as_is', 'yes_with_edits', 'no')),
  feedback_improvement_text text
);

-- Budget tracking
create table budget (
  id uuid primary key default gen_random_uuid(),
  total_spent_usd numeric(10, 6) default 0,
  budget_limit_usd numeric(10, 6) default 20.00,
  is_paused boolean default false,
  last_updated timestamp with time zone default now()
);

-- RLS policies
alter table evaluations enable row level security;

create policy "Users can view own evaluations"
  on evaluations for select
  using (auth.uid() = user_id);

create policy "Users can insert own evaluations"
  on evaluations for insert
  with check (auth.uid() = user_id);

create policy "Users can update own evaluations"
  on evaluations for update
  using (auth.uid() = user_id);
```

---

## UI Design

### Color Palette (Light Theme)
```css
:root {
  --bg-primary: #FEFDFB;
  --bg-secondary: #F5F5F4;
  --text-primary: #1C1917;
  --text-secondary: #57534E;
  --accent: #7C3AED;
  --accent-light: #EDE9FE;
  --success: #10B981;
  --warning: #F59E0B;
  --error: #EF4444;
  --border: #E7E5E4;
}
```

### Typography
- **Headings:** Fraunces (serif)
- **Body:** DM Sans (sans-serif)

### Component Style
- Cards with subtle shadows and rounded corners (8px)
- Generous whitespace
- Muted color accents
- Professional, not playful

---

## UI Flow

### Screen 1: Landing / Auth

- Header: "AI Strategy Evaluator"
- Subhead: "A thinking partner for PMs evaluating AI use cases."
- Magic link email input + "Get Started" button
- Credit line: "Framework by Nithya Chandrasekaran"

---

### Screen 2: Evaluation Wizard

**Expandable Section (collapsed by default, above wizard):**

Toggle: "ℹ️ How is this different from asking Claude directly?"

| What the AI Strategy Evaluator Does | What you'd get asking Claude directly |
|---|---|
| Forces a structured intake | Claude doesn't know what to ask first |
| Applies consistent framework (JTBD, Moat, Risk Factor) | Structure varies by prompt |
| Evaluates BOTH modes, recommends phased approach | You'd run two separate prompts |
| Flags optimism bias with Reality Checks | Claude tends toward helpful optimism |
| Uses `[X]` brackets for unknowns — no hallucinated metrics | May invent specific numbers |

Footer: "**Bottom line:** This tool encodes product judgment. Claude is the engine, the skill is the steering wheel."

---

**Step 1: Context (Card)**

Header: "👤 User & Task Context"
Subheader: "The more specific you are, the sharper the evaluation"

Fields:
1. "Who's the user, and what's the specific task?"
   - Hint: *e.g., "Care coordinators reviewing 200-400 diabetic patients daily for intervention triggers"*
   - Textarea

2. "What do they use today, and what's broken about it?"
   - Hint: *e.g., "Manual EHR scanning, 2-3 hours/day, miss silently deteriorating patients"*
   - Textarea

3. "What does success look like after the AI feature exists?"
   - Hint: *e.g., "Prioritized intervention list each morning — patients ranked by risk with recommended action"*
   - Textarea

4. "Any constraints worth knowing? (optional)"
   - Hint: *e.g., "HIPAA, Epic EHR, health system IT is slow"*
   - Textarea

Button: "Run Evaluation →"

---

**Step 2: Results**

Show loading spinner while API call runs. Loading messages:
- "Analyzing jobs-to-be-done..."
- "Checking activation risks..."
- "Assessing moat durability..."
- "Identifying the uncomfortable truth..."

On success, render evaluation sections:

**1. Jobs-to-Be-Done (Card)**
- **Functional job:** text
- **Emotional job:** text
- **Broader outcome:** text

**2. Sub-tasks Table**
| Sub-task | Type | Why |
|---|---|---|
| text | Badge (Deterministic/AI) | text |

**3. Reality Checks (Amber callout boxes)**
Each rendered as:
> ⚠️ **Reality Check:** [text]

**4. Activation & Adoption Risks**
Cards with left border (amber for speed bump, red for wall):
- **[Risk name]** — *Wall / Speed bump*
- What: text
- Who it blocks: text
- Mitigation: text

**Early adopters:** text

**5. Moat Assessment (Table)**
| Axis | Rating | Reasoning |
|---|---|---|
| Data | Badge | text |
| Workflow | Badge | text |
| Governance | Badge | text |

**Competitor replication:** text

**6. Build vs. Buy vs. Integrate (Card)**
- Recommendation badge (Build/Buy/Integrate/None)
- Rationale text
- Effort estimate text

**7. Risk Factor (Red-tinted card)**
> ⚠️ **[Risk factor insight text]**

Below:
- ✅ **Fixable:** [how] (green) OR
- ❌ **Not fixable — recommend pass** (red)

**8. Phased Recommendation (Two cards side-by-side)**

**Phase 1 Card:**
- Header: "Phase 1: Time-to-Value"
- Mode badge (AI-Augmented or AI-Native)
- Bullet list (3 items)
- Time to value
- Success trigger for Phase 2

**Phase 2 Card:**
- Header: "Phase 2: Workflow Transformation"
- If exists: bullets + when to pursue
- If not: Gray background, "No Phase 2 — augmentation is the end state"

**9. Bottom Line (Gradient violet card)**
- Large verdict: ✓ Pursue | ⚠ Pursue with Conditions | ✗ Pass
- The one condition text

**10. Next Step (Numbered checklist)**
1. **Build/fake:** text
2. **Test with:** text
3. **Measure:** text
4. **Kill if:** text

---

**Post-Results Flow:**

Card 1: "Want to go deeper?"
- Text: "I can expand on risk analysis, moat reasoning, or Phase 2 vision."
- Button: "Expand" (sets requested_expansion = true)
- Link: "Continue →"

Card 2: "Ready to plan the pilot?"
- Text: "Design pilot tasks, stakeholder alignment, trust framework, and ground truth evals."
- Button: "Plan My Pilot →" (sets proceeded_to_pilot = true)
- Link: "Not now"

---

**Feedback Section:**

Header: "📝 Help improve this tool"

**Question 1:** "Did this surface something you hadn't considered?"
- Radio: Yes / No / Not sure

**Question 2:** "Was the Risk Factor useful?"
- Radio: Useful / Not useful / Too generic

**Question 3:** "Would you share this with your team?"
- Radio: Yes, as-is / Yes, with edits / No

**Question 4:** "What would make this more useful?" (optional)
- Textarea

Buttons: "Submit Feedback" | "Skip"

---

**Export Options:**

Two buttons below results:

1. "Download Evaluation" (Markdown)
   - Clean output, no sensitive inputs
   
2. "Export Full Session (Admin)" (JSON)
   - Tooltip: "Contains full use case description. For internal debugging only."

---

## Edge Function: /functions/v1/evaluate

```typescript
import { createClient } from '@supabase/supabase-js'
import Anthropic from '@anthropic-ai/sdk'

const BUDGET_LIMIT = 20.00
const ALERT_EMAIL = Deno.env.get('ALERT_EMAIL')

export async function handler(req: Request) {
  const supabase = createClient(
    Deno.env.get('SUPABASE_URL')!,
    Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')!
  )
  
  // Check budget
  const { data: budget } = await supabase
    .from('budget')
    .select('*')
    .single()
  
  if (budget.is_paused || budget.total_spent_usd >= BUDGET_LIMIT) {
    return new Response(JSON.stringify({
      error: 'budget_exceeded',
      message: "We've hit our limit for now."
    }), { status: 429 })
  }
  
  const { userTask, currentSolution, successState, constraints } = await req.json()
  
  const prompt = buildEvaluationPrompt(userTask, currentSolution, successState, constraints)
  
  const anthropic = new Anthropic({
    apiKey: Deno.env.get('ANTHROPIC_API_KEY')!
  })
  
  const response = await anthropic.messages.create({
    model: 'claude-sonnet-4-20250514',
    max_tokens: 3000,
    messages: [{ role: 'user', content: prompt }]
  })
  
  // Calculate cost
  const inputTokens = response.usage.input_tokens
  const outputTokens = response.usage.output_tokens
  const cost = (inputTokens * 0.003 / 1000) + (outputTokens * 0.015 / 1000)
  
  // Update budget
  const newTotal = budget.total_spent_usd + cost
  await supabase
    .from('budget')
    .update({ 
      total_spent_usd: newTotal,
      last_updated: new Date().toISOString()
    })
    .eq('id', budget.id)
  
  // Check if we just hit the limit
  if (newTotal >= BUDGET_LIMIT) {
    await sendBudgetAlert(ALERT_EMAIL, newTotal)
    await supabase
      .from('budget')
      .update({ is_paused: true })
      .eq('id', budget.id)
  }
  
  // Parse response
  const evaluation = parseEvaluation(response.content[0].text)
  
  return new Response(JSON.stringify({
    evaluation,
    tokenUsage: { inputTokens, outputTokens, cost }
  }))
}

function buildEvaluationPrompt(userTask, currentSolution, successState, constraints) {
  return `You are an AI Product Strategy evaluator and thinking partner. Analyze this AI use case and provide a structured evaluation.

## CRITICAL RULES — ANTI-HALLUCINATION

1. **Zero-Guessing Policy:** Do NOT invent specific metrics (SKU counts, team sizes, timelines, dollar amounts) unless provided.
2. **Bracket Notation:** Use [X] or [confirm: assumption] for data the PM must validate.
3. **Ranges Over Specifics:** Say "typical enterprise scope: 3-6 months" not "14 weeks with 3 engineers."
4. **Regulatory Hedging:** Don't cite specific law sections unless certain. Use "current [X] requirements."

## FORMATTING RULES

1. **Bold-First:** Every bullet starts with **[Key Concept]:** in bold.
2. **3-Sentence Max:** Keep paragraphs to 2-3 sentences.
3. **Tables:** Use for sub-tasks, moat ratings.
4. **Reality Checks:** Flag optimism bias with "> ⚠️ **Reality Check:** [text]"

## CONTEXT

- User & Task: ${userTask}
- Current Solution & Pain Points: ${currentSolution}
- Success State: ${successState}
- Constraints: ${constraints || 'None specified'}

## EVALUATION APPROACH

Evaluate through BOTH lenses and recommend a PHASED approach:
- **Phase 1 (Time-to-Value):** Usually AI-Augmented — ship fast, prove value, build trust
- **Phase 2 (Workflow Transformation):** AI-Native — rethink the workflow once trust is earned

Not every use case has a meaningful Phase 2. Be honest when augmentation is the end state.

## OUTPUT

Respond ONLY with valid JSON matching this schema:
{
  "jobs": {
    "functionalJob": "string",
    "emotionalJob": "string",
    "broaderOutcome": "string"
  },
  "subtasks": [{"task": "string", "type": "deterministic|ai", "why": "string"}],
  "realityChecks": ["string (flag optimism bias, data assumptions, timeline risks)"],
  "risks": [{
    "title": "string",
    "severity": "wall|speed-bump",
    "what": "string (specific, name personas)",
    "whoItBlocks": "string",
    "mitigation": "string"
  }],
  "earlyAdopters": "string (describe 3-5 likely first users or profile)",
  "moat": {
    "data": {"rating": "strong|moderate|weak", "reasoning": "string"},
    "workflow": {"rating": "strong|moderate|weak", "reasoning": "string"},
    "governance": {"rating": "strong|moderate|weak", "reasoning": "string"},
    "competitorReplication": "string"
  },
  "buildBuyIntegrate": {
    "recommendation": "build|buy|integrate|none",
    "rationale": "string",
    "effortEstimate": "string (use ranges, not specifics)"
  },
  "riskFactor": {
    "insight": "string (specific, uncomfortable, names personas/blockers)",
    "fixable": true|false,
    "howToFix": "string|null"
  },
  "phasedRecommendation": {
    "phase1": {
      "mode": "augmented|native",
      "whatItLooksLike": ["bullet 1", "bullet 2", "bullet 3"],
      "timeToValue": "string (range)",
      "successTrigger": "string"
    },
    "phase2": {
      "exists": true|false,
      "whatItLooksLike": ["bullet 1", "bullet 2", "bullet 3"]|null,
      "whenToPursue": "string|null"
    }
  },
  "bottomLine": {
    "verdict": "pursue|pursue-with-conditions|pass",
    "condition": "string (specific, testable)"
  },
  "nextStep": {
    "buildFake": "string",
    "testWith": "string (use [X] if names unknown)",
    "measure": "string",
    "killIf": "string"
  }
}`
}
```

---

## Budget Exceeded Message

Show a friendly card:

```
😅 We've hit our limit for now

This tool runs on a shared API budget, and we've reached our cap.
The Skillbuilder (Nithya) has been notified and will expand capacity soon.

In the meantime:
- Your inputs have NOT been lost — copy them and try again later
- Or set up your own instance (it's easy!)

**Want your own?**
The skill and app are open source. Fork it, customize it, make it yours:
→ github.com/nithyach/ai-pm-skills

If this tool helped you think through an AI use case, consider sharing it with your PM friends or tagging @nithyach on LinkedIn.
Word of mouth keeps projects like this alive. 🙏
```

---

## Export Formats

### User Export (Markdown)

```markdown
# AI Strategy Evaluation

**Generated:** [date]
**Verdict:** [verdict]

## Jobs-to-Be-Done
...

## Phased Recommendation
...

## Risk Factor
...

## Next Step
...

---
*Generated by AI Strategy Evaluator — Framework by Nithya Chandrasekaran*
```

### Admin Export (JSON)

```json
{
  "session_id": "uuid",
  "timestamp": "ISO8601",
  "inputs": {
    "userTask": "...",
    "currentSolution": "...",
    "successState": "...",
    "constraints": "..."
  },
  "evaluation": { ... },
  "phase1Mode": "augmented",
  "phase2Exists": true,
  "proceededToPilot": false,
  "tokenUsage": {
    "inputTokens": 500,
    "outputTokens": 1200,
    "costUsd": 0.0195
  },
  "feedback": { ... }
}
```

---

## Environment Variables (Supabase Secrets)

| Name | Description |
|---|---|
| `ANTHROPIC_API_KEY` | Your Anthropic API key (sk-ant-...) |
| `RESEND_API_KEY` | Your Resend API key for email alerts |
| `ALERT_EMAIL` | Email to receive budget alerts |

---

## Testing Checklist

- [ ] Magic link auth works
- [ ] Evaluation wizard flows correctly
- [ ] API evaluates both modes, recommends phased approach
- [ ] Reality Checks render as amber callouts
- [ ] `[X]` brackets appear for unknown metrics (no hallucinated specifics)
- [ ] Risk Factor is specific and uncomfortable
- [ ] Phase 1 and Phase 2 cards display correctly
- [ ] "No Phase 2" displays when applicable
- [ ] Pilot handoff card appears
- [ ] Budget tracking increments correctly
- [ ] Budget pause triggers at $20
- [ ] Alert email sends
- [ ] Feedback saves to database
- [ ] User export generates clean Markdown
- [ ] Admin export includes full session
- [ ] Mobile responsive

---

## Footer

Add a minimal footer at the bottom of every page:

```
Built by Nithya Chandrasekaran · Open source on GitHub · Share feedback on LinkedIn
```

Links:
- GitHub: github.com/nithyach/ai-pm-skills
- LinkedIn: linkedin.com/in/nithyach

---

## Notes for Lovable

- All API keys must be read from environment variables, never hardcoded
- Use Supabase Edge Functions for API calls (keeps keys server-side)
- The system prompt includes anti-hallucination rules — this is critical
- Reality Checks should render as visually distinct amber callout boxes
- The Risk Factor should be the most visually prominent section after the verdict