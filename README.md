# gochal-plugin

A Claude Code plugin that transforms Claude from a solution-provider into a **senior engineer thinking partner**. Instead of listing A/B/C options and recommending one, Gochal (고찰) maps the solution landscape together with you — teaching trade-offs so you can make grounded decisions yourself.

## Motivation

AI coding assistants tend to recommend solutions. The problem? Research shows that when AI presents recommendations, users follow them even when they conflict with their own judgment ([Klingbeil et al., 2024](https://doi.org/10.1016/j.chb.2024.108100)). This short-circuits learning and produces decisions without understanding.

Gochal takes a different approach. Inspired by Applied Cognitive Task Analysis (ACTA) and preference construction theory, it:

- **Teaches trade-offs** instead of recommending solutions
- **Simulates concrete scenarios** before abstract discussion
- **Lets you converge** when you're ready — never pushes you toward a choice
- **Produces transferable mental models** — patterns you'll recognize in future decisions

The name 고찰 (go-chal) means "deep contemplation" in Korean. It reflects the skill's philosophy: thinking deeply together is more valuable than getting a quick answer.

## How It Works

Gochal follows a 5-phase cognitive protocol:

```
1. Intent     — Understand what you're building and why
2. Simulate   — Walk through concrete end-to-end scenarios
3. Explore    — Map the solution landscape for each decision point
4. Anchor     — Surface core trade-offs as value questions
5. Converge   — Confirm your decision with full context
   → Decision Record (고찰록)
```

### Phase 1: Intent

Gochal reads your project context (files, docs, recent commits) and confirms understanding. Only asks what it genuinely doesn't know — no checklist interrogations.

### Phase 2: Simulate

Before any abstract discussion, you walk through 1-2 real scenarios **step by step** (3+ concrete steps each, not a one-sentence summary):

> "Let's walk through the actual usage. A user arrives at X — what happens next?"

Each step surfaces constraints, assumptions, and decision points. Then hard cases are probed from two angles — **technical failure** ("what breaks?") and **experiential failure** ("what feels wrong even if it works?"). These scenarios become the **evaluation criteria** for Phase 3.

### Phase 3: Explore

For each decision point, Gochal maps the landscape — not as a numbered menu, but as a guided exploration with enforced depth:

- Why each approach **exists** — specific problem context, not one-sentence labels
- Where each approach **shines and breaks** — at least **1 real-world example or failure case** per approach
- **Multiple perspectives** — at least **2 distinct viewpoints** per decision point ("performance engineer" / "product" / "maintainability")
- **Mandatory scenario application** — every approach is tested against Phase 2's hard cases
- **Hybrid approaches** — mixing elements from different approaches is encouraged

### Phase 4: Anchor

Core trade-offs are framed as **spectrum questions**, not binary choices. Most design decisions have at least **2 independent trade-off axes** — if only 1 is visible, the skill pauses to reconsider:

> "It comes down to two axes: **deployment complexity** vs **library access**. Where do you lean on each?"

### Phase 5: Converge

Only when you signal readiness ("let's go with this"). Gochal reflects the full picture — what you gain, what you trade off, and what patterns transfer to future decisions.

A **Decision Record** (고찰록) is generated — a shareable document capturing the landscape explored, trade-offs considered, and reasoning behind the decision.

## Installation

```bash
# Add the marketplace
/plugin marketplace add yungjurick/gochal-plugin

# Install the plugin
/plugin install gochal-plugin@gochal-plugin
```

## Usage

Invoke with any of these triggers:

```
/gochal-plugin:gochal
```

Or let Claude detect it automatically from natural language:

- "Let's think about how to approach X"
- "How should I design X?"
- "Design discussion"
- "Architecture decision"
- Korean: "고찰", "같이 생각해보자", "어떻게 접근하면", "설계 논의"

### Example

```
You: I need to add real-time notifications to our app. How should I approach this?

Claude: 고찰 시작합니다.

[고찰 1/5: 맥락 파악]
Looking at your project... you're running a Next.js app with a REST API.
So you want to add real-time notifications — is this for in-app alerts,
or do you also need push notifications when the tab is closed?
```

## When to Use

- Design discussions with multiple valid approaches
- Architecture decisions with meaningful trade-offs
- Feature brainstorming where you want to understand the landscape
- Any decision where you'd benefit from a thinking partner

## When NOT to Use

- Quick bug fixes with obvious solutions
- Simple CRUD implementations
- Tasks where the approach is already decided
- Code review or debugging (use dedicated tools for those)

## Depth Enforcement

Gochal includes built-in quality controls to prevent shallow exploration:

- **Self-checks** at each phase transition — Claude verifies depth criteria are met before moving on (invisible to the user)
- **Minimum thresholds** — at least 1 real example per approach, 2 perspectives per decision, 2 trade-off axes
- **Shallow exploration signals** — a red flags table catches common shortcuts (one-sentence scenarios, single-perspective analysis, missing scenario application)

These controls ensure the same quality of exploration whether the topic is simple or complex.

## Configuration

The skill works out of the box with no configuration. The Decision Record (고찰록) save location is asked at the end of each session.

## Requirements

- Claude Code CLI
- No external dependencies

## Contributing

Contributions are welcome! Here's how to help:

### Submitting Changes

1. Fork this repository
2. Create a feature branch (`git checkout -b feat/your-improvement`)
3. Make your changes to `skills/gochal/SKILL.md`
4. Test the skill by running it in Claude Code with `claude --plugin-dir ./`
5. Submit a pull request

### Quality Standards

**Required:**
- Changes must be tested in Claude Code before submitting
- Skill must remain a single `SKILL.md` file (no unnecessary complexity)
- Maintain the core philosophy: teach trade-offs, never recommend

**Recommended:**
- Include a before/after example showing the improvement
- Explain the reasoning behind behavioral changes
- Consider impact on non-English speakers (the skill supports Korean context)

### Ideas for Contribution

- **Translations** — adapt the cultural context sections for other team cultures
- **Phase improvements** — better prompting for specific decision types (infrastructure, API design, data modeling)
- **Decision Record templates** — alternative formats for different team workflows
- **Integration examples** — how to chain Gochal with other skills or workflows

## License

MIT

## Author

[@yungjurick](https://github.com/yungjurick)
