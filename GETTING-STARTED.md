# Getting Started with AI Strategy Evaluator

**A thinking partner for PMs evaluating AI use cases**

---

## What Is This?

A structured evaluation framework that helps you answer: *Should we build this AI feature?*

It surfaces the questions most teams skip:
- Is this actually an AI problem, or would deterministic logic work?
- What's the most likely reason this fails?
- Should we start with AI-Augmented (fast) or AI-Native (ambitious)?
- What's the fastest way to validate before committing?

---

## Three Ways to Use It

Choose based on your comfort level and data sensitivity:

| Option | Best For | Setup Time | Data Privacy |
|---|---|---|---|
| **A. Hosted App** | Quick tryout, non-sensitive use cases | 0 min | Data stored in shared Supabase |
| **B. Claude Project** | Regular use, moderate sensitivity | 5 min | Your Claude account, your data |
| **C. Fork & Self-Host** | Enterprise, sensitive use cases | 30-60 min | Fully private, your infrastructure |

---

## Option A: Hosted App (Fastest)

### When to Use
- You want to try it immediately
- Your use case description isn't confidential
- You're okay with data stored in a shared database

### How to Start
1. Go to: https://ai-pm-partner.lovable.app/
2. Enter access code (Email for access)
3. Describe your use case → Run Evaluation

### Limitations
- Need access token to use pre-built app
- Data stored in shared Supabase instance
- No customization

---

## Option B: Claude Project (Recommended for Regular Use)

### When to Use
- You want the skill in your own Claude account
- You want to run evaluations without visiting a separate app
- Moderate sensitivity — Claude's standard data handling is acceptable

### Setup (5 minutes)

1. **Get the skill file**
   ```
   Download: github.com/nithyach/ai-pm-skills/ai-strategy-evaluator/SKILL.md
   ```

2. **Create a Claude Project**
   - Go to [claude.ai](https://claude.ai)
   - Click "Projects" → "New Project"
   - Name it: "AI Strategy Evaluator"

3. **Add the skill**
   - In your project, click "Add Content"
   - Upload `SKILL.md`

4. **Test it**
   ```
   Evaluate this AI use case:
   
   **Who:** [describe the user and their task]
   **What's broken:** [describe current pain]
   **Success:** [describe what good looks like]
   **Constraints:** [any technical/compliance constraints]
   ```

### Usage Tips
- Start messages with "Evaluate this AI use case:" for best results
- After evaluation, you can say "expand on the moat section" or "plan the pilot"
- Your conversation history stays in your Claude account

---

## Option C: Fork & Self-Host (Full Privacy) 

### When to Use
- Enterprise environment with sensitive use cases
- You need audit logs and data residency control
- You want to customize the skill for your team
- Instructions for this are AI generated. Please reach out if you have any issues

### What You'll Need
- GitHub account
- Supabase account (free tier works)
- Anthropic API key
- Basic familiarity with deploying web apps

### Setup (30-60 minutes)

#### Step 1: Fork the Repository
```bash
# Fork on GitHub, then clone
git clone https://nitsjuly/ai-pm-skills.git
cd ai-pm-skills
```

#### Step 2: Set Up Supabase
1. Create account at [supabase.com](https://supabase.com)
2. Create new project
3. Go to SQL Editor, run the schema from `app/lovable-app-prompt.md`
4. Note your project URL and anon key

#### Step 3: Get Anthropic API Key
1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Create new API key
3. Set spending limit (recommend $25-50/month to start and test)

#### Step 4: Deploy to Lovable (or Your Preferred Platform)
1. Go to [lovable.dev](https://lovable.dev)
2. Paste contents of `app/lovable-app-prompt.md`
3. Connect your Supabase project
4. Add environment variables:
   - `ANTHROPIC_API_KEY`
   - `SUPABASE_URL`
   - `SUPABASE_ANON_KEY`

#### Step 5: Configure Secrets
In Supabase Dashboard → Settings → Edge Functions → Secrets:
- `ANTHROPIC_API_KEY`: your key
- `RESEND_API_KEY`: (optional, for budget alerts)
- `ALERT_EMAIL`: your email

#### Step 6: Initialize Budget
```sql
INSERT INTO budget (total_spent_usd, budget_limit_usd, is_paused) 
VALUES (0, 50.00, false);
```

### Customization Options
- **Edit SKILL.md:** Add your company's frameworks, change terminology
- **Adjust budget:** Increase `budget_limit_usd` in Supabase
- **Add team auth:** Configure Supabase Auth for your SSO
- **Custom domain:** Point your domain to Lovable deployment

---

## Using the Skill Directly (No App)

If you just want the evaluation framework without any app:

### In Claude.ai (Free)
1. Copy the contents of `SKILL.md`
2. Paste at the start of any conversation
3. Then paste your use case

### Via API (BYOK)
```python
import anthropic

client = anthropic.Anthropic(api_key="your-key")

skill_prompt = open("SKILL.md").read()
user_context = """
Evaluate this AI use case:
**Who:** [user and task]
**What's broken:** [current pain]
**Success:** [desired outcome]
**Constraints:** [any constraints]
"""

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=3000,
    messages=[
        {"role": "user", "content": skill_prompt + "\n\n" + user_context}
    ]
)

print(response.content[0].text)
```

---

## Example: Running Your First Evaluation

### Input
```
Evaluate this AI use case:

**Who:** Finance teams (2-5 people) at mid-market companies who manually 
review and categorize expense reports weekly.

**What's broken:** Reviewers spend 4-6 hours/week checking receipts against 
policy, flagging violations, and categorizing expenses. Errors slip through. 
Month-end close is stressful.

**Success:** AI auto-categorizes expenses, flags policy violations with 
explanations, and surfaces a "review queue" of only the edge cases.

**Constraints:** SOC2, NetSuite integration, finance teams are conservative 
adopters, competitors already have AI features.
```

### What You'll Get
- **Jobs-to-Be-Done:** Functional + emotional job
- **Sub-tasks:** What's AI vs. deterministic
- **Reality Checks:** Flags optimism bias
- **Risks:** Specific blockers with severity
- **Moat:** Data/Workflow/Governance assessment
- **Risk Factor:** The uncomfortable truth
- **Phased Recommendation:** Phase 1 (speed) → Phase 2 (transformation)
- **Next Step:** Concrete validation this week

---

## Feedback & Contributions

### Found a Bug?
Open an issue: `github.com/nithyach/ai-pm-skills/issues`

### Want to Improve the Framework?
I built this as a tool that i wished my team had when we started down this road. It overlays specific context, structured thinking and frameworks and leverages Claude models to provide a structured, grounded "thinking partner". 

PRs welcome! Areas of interest:
- Industry-specific examples
- Additional risk categories
- Integration with other PM tools

### Share Your Experience
If this helped you make a better roadmap decision, I'd love to hear about it:
- LinkedIn: [linkedin.com/in/nithyach](https://linkedin.com/in/nithyach)
- Tag with #AIStrategyEvaluator

---

## FAQ

### "Is my data safe in the hosted app?"
Data is stored in Supabase with encryption at rest. For sensitive use cases, use Option B (Claude Project) or Option C (Self-Host).

### "How much does it cost to self-host?"
- Supabase: Free tier works for low volume
- Anthropic API: ~$0.02 per evaluation
- 1,000 evaluations ≈ $20

### "Can I use this commercially?"
Yes — MIT License. Attribution appreciated but not required.

### "Can I customize the framework for my team?"
Yes! Fork the repo, edit SKILL.md, deploy your own version.

---

## Quick Links

| Resource | URL |
|---|---|
| Hosted App | https://ai-pm-partner.lovable.app | DM me for Access
| GitHub Repo | `github.com/nithyach/ai-pm-skills` |
| SKILL.md (raw) | `github.com/nithyach/ai-pm-skills/ai-strategy-evaluator/SKILL.md` |
| Author LinkedIn | `linkedin.com/in/nithyach` |

---

*Built by Nithya Chandrasekaran · MIT License*
