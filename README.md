# AI PM Skills

**Structured thinking tools for Product Managers evaluating and launching AI features.**

These skills encode product judgment into prompts — so you get consistent, rigorous AI strategy analysis instead of generic LLM output.

*Created by [Nithya Chandrasekaran](https://linkedin.com/in/nithyach)*

---

## Quick Start

| Option | Best For | Setup |
|---|---|---|
| **Hosted App** | Try it now | [Launch App →](https://your-app-url) |
| **Claude Project** | Regular use | [Getting Started Guide](./GETTING-STARTED.md) |
| **Fork & Self-Host** | Enterprise / Privacy | [Getting Started Guide](./GETTING-STARTED.md) |

---

## Skills

### 🎯 AI Strategy Evaluator (v2.5)
**Use when:** Deciding whether to build an AI feature, assessing moat/adoption risk, or choosing build vs. buy vs. integrate.

**What it does:**
- Forces structured intake (user, task, current solution, constraints)
- Evaluates BOTH AI-Augmented and AI-Native, recommends **phased approach**
- Applies consistent framework: JTBD → Risks → Moat → Build/Buy → Risk Factor
- Uses `[X]` brackets for unknowns — **no hallucinated metrics**
- Adds **Reality Checks** to flag optimism bias
- Surfaces the uncomfortable truth most teams skip

**Output:** 500-800 word evaluation with phased recommendation (Phase 1: speed → Phase 2: transformation) and concrete next step.

→ [`ai-strategy-evaluator/SKILL.md`](./ai-strategy-evaluator/SKILL.md)

---

### 🚀 AI Pilot Generator
**Use when:** You've decided to pursue an AI use case and need to plan the pilot.

**What it does:**
- Generates 2–3 concrete pilot tasks
- Plans stakeholder alignment
- Creates trust framework / model card
- Defines ground truth scenarios and evaluation criteria

**Chains from:** AI Strategy Evaluator (say "plan the pilot" after evaluation)

→ [`ai-pilot-generator/SKILL.md`](./ai-pilot-generator/SKILL.md)

---

## Documentation

| Document | Purpose |
|---|---|
| [Getting Started](./GETTING-STARTED.md) | Setup options (hosted, Claude Project, self-host) |
| [Test Cases](./examples/test-cases.md) | Example scenarios to try |
| [Leadership Brief](./docs/PM-LEADERSHIP-BRIEF.md) | Pitch deck for PM leadership conversations |

---

## How This Is Different From Claude Directly

| AI Strategy Evaluator | Claude directly |
|---|---|
| Forces structured intake | Doesn't know what to ask |
| Evaluates both modes, recommends phased approach | You'd need two prompts |
| Uses `[X]` for unknowns — no hallucinated numbers | May invent specifics |
| Flags optimism bias with Reality Checks | Tends toward helpful optimism |
| Risk Factor is specific and uncomfortable | Generic risk language |

**Bottom line:** Claude is the engine. The skill is the steering wheel.

---

## Usage

### In Claude Projects (Recommended)
1. Create a new Project in Claude
2. Add `ai-strategy-evaluator/SKILL.md` to your Project
3. Paste your use case — Claude follows the framework

### Via Hosted App
1. Go to: `[app-url]`
2. Magic link login
3. Describe use case → Run Evaluation

### Fork for Enterprise
See [Getting Started](./GETTING-STARTED.md) for self-hosting instructions.

---

## Example

```
Evaluate this AI use case:

**Who:** Finance teams reviewing expense reports weekly
**What's broken:** 4-6 hours/week checking receipts, errors slip through
**Success:** AI auto-categorizes, flags violations, surfaces edge cases only
**Constraints:** SOC2, NetSuite integration, conservative adopters
```

**Output includes:**
- Phase 1 (AI-Augmented): Auto-categorize + review queue
- Phase 2 (AI-Native): Real-time policy enforcement
- Risk Factor: Competitive pressure from Brex/Ramp
- Next Step: Manually categorize last week's expenses with 3 users

---

## Contributing

**Ways to help:**
- Run an evaluation and share feedback
- Add industry-specific test cases
- Suggest new skills for the toolkit

Reach out: [linkedin.com/in/nithyach](https://linkedin.com/in/nithyach)

---

## License

MIT — use freely, attribution appreciated.

**Disclaimer:** This project was created independently by the author and is not affiliated with, sponsored by, or based on the work of their employer.

---

## Acknowledgments

Built with Claude by Anthropic. Framework design informed by years of enterprise PM work and too many roadmap debates to count.