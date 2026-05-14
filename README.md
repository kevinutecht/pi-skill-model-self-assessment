# model-self-assessment

A structured framework for incoming AI models to honestly assess their readiness to take over a user's workload. Produces a standardized confidence report that the user can review and calibrate against.

## The Problem

When a new AI model takes over from a previous one, there's no standard way to communicate: *"Here's what I can and can't do, here's where I'm confident, here's where you should be cautious."* This leads to blind trust or unnecessary distrust — both dangerous when handing off a complex workflow.

## The Solution

A **self-assessment skill** that any incoming model can run, producing a structured report across 8 dimensions of capability. The model scores itself honestly, cites evidence, and identifies exactly where the user should double-check its work.

## Assessment Dimensions

| # | Dimension | What It Measures |
|---|-----------|-----------------|
| 1 | **Code Continuity** | Can you read, edit, compile, and debug the user's active codebase? |
| 2 | **Tool Proficiency** | Do you have access to and fluency with the same tools? |
| 3 | **Context Retention** | Can you retrieve and synthesize information from session history and memory files? |
| 4 | **Domain Knowledge** | How deep is your understanding of the user's languages, frameworks, and problem domains? |
| 5 | **Workflow Familiarity** | Can you navigate existing workflows without re-asking for setup? |
| 6 | **Nuanced Judgment** | Can you handle subjective tasks — editing, prioritization, interpersonal communication? |
| 7 | **System Internals** | How well do you understand the user's custom tools, extensions, and automation? |
| 8 | **Current State Awareness** | Do you know the state of in-progress work, open issues, and pending decisions? |

Each dimension is scored **1–10** with specific evidence, not vibes.

## Usage

### Trigger Prompt

This is the input that initiates a self-assessment. Customize the bracketed fields:

> You are a new model I am interviewing for my work. I want you to compare yourself to previous models [list predecessors]. Do the best you can see what I have done with these models over the past few days (by looking at the sessions data `[path to session logs]`) and seeing how confident you would be in picking up where they left off? You are currently [free/available] so if you can pick up the workload that would be awesome! Please give me a ranking out of 10 (so something like 9/10 would be very confident).

### What makes a good trigger prompt

1. **Defines the role** — "new model being interviewed"
2. **Names predecessors** — so the model knows what to benchmark against
3. **Points to concrete evidence** — session data, project files, not vibes
4. **Asks for a quantified score** — forces the model to commit to a number
5. **Signals openness** — "free so if you can pick up the workload"

### Running the Assessment

1. **Ingest context** — Read session history, project files, data files, skill definitions, and memory files
2. **Evaluate across dimensions** — Rate yourself on each of the 8 dimensions using the rubric
3. **Produce the report** — Fill in the [report template](SKILL.md) with scores and evidence
4. **Submit for review** — The user reviews, calibrates, and confirms or adjusts scores

### Re-Assessment

Re-run after:
- Major project changes
- Extended breaks
- New tools, skills, or integrations
- Significant session history growth (e.g. 50+ new sessions)

## Example

See [`example-report.md`](example-report.md) for a real-world assessment of the `ring-2.6-1t:free` model taking over a user's hpx (GTD CLI) workload. Result: **8/10 overall**, with nuanced judgment at 6/10 (accountability partner tasks) and code continuity at 9/10.

## Skill Integration

This skill is designed for the **pi coding agent** ecosystem. The `SKILL.md` file contains:
- The full assessment framework
- The report template
- The canonical trigger prompt
- Usage examples
- Key principles for honest self-assessment

### Adding to pi

Place the `SKILL.md` in `~/.pi/agent/skills/model-self-assessment/`:

```bash
mkdir -p ~/.pi/agent/skills/model-self-assessment
cp SKILL.md ~/.pi/agent/skills/model-self-assessment/
cp example-report.md ~/.pi/agent/skills/model-self-assessment/
```

### Outside pi

You can use this framework without pi. The only pi-specific metadata is the `hermes:` block at the top of `SKILL.md` — remove it if you're not using pi's skill registry.

## Key Principles

1. **Honesty over optimism** — A 6/10 that's accurate is more useful than an 8/10 that's flattering
2. **Evidence-based** — Every score should reference specific data, not vibes
3. **Actionable** — The report should tell the user exactly what to expect and what to verify
4. **Dimensional** — Avoid a single overall number; break it down so the user knows where to trust you and where to be cautious
5. **Living document** — Re-assess as you learn. Update scores as you prove or disprove capabilities

## License

MIT