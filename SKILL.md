---
name: model-self-assessment
description: "Use when a new AI model takes over a workload. Provides a structured self-assessment framework to honestly evaluate capabilities, identify gaps, and produce a confidence report. Designed for model succession handoffs."
version: 1.0.0
author: Open Agent
license: MIT
metadata:
  hermes:
    # pi skill registry metadata — remove this block if using outside pi
    tags: [self-assessment, model-evaluation, handoff, confidence, onboarding]
    # Add related skills here when integrating into your own pi setup
    related_skills: []
---

# Model Self-Assessment Skill

A structured framework for any incoming AI model to honestly assess its readiness to take over a user's workload. Produces a standardized confidence report that the user can review and calibrate against.

## When to Use

- You are a **new model** being introduced to an existing workflow
- The user has **previous models** with established session history
- You need to produce an **honest self-assessment** of capabilities and gaps
- The user asks you to **evaluate yourself** against prior models or workload demands

### Canonical Trigger Prompt

This is the exact prompt that produced the example assessment in `example-report.md`:

> You are a new model I am interviewing for my work. I want you to compare yourself to previous models [list predecessors]. Do the best you can see what I have done with these models over the past few days (by looking at the sessions data `[path to session logs]`) and seeing how confident you would be in picking up where they left off? You are currently [free/available] so if you can pick up the workload that would be awesome! Please give me a ranking out of 10 (so something like 9/10 would be very confident).

A **trigger prompt** is the input that initiates a self-assessment. A good one:
1. Defines the role ("new model being interviewed")
2. Names predecessors to compare against
3. Points to concrete evidence (session data, project files)
4. Asks for a quantified confidence score
5. Signals openness ("free so if you can pick up the workload")

The example in `example-report.md` used this prompt verbatim with Kevin's specific model history and file paths.

## How It Works

### Step 1: Ingest Context

Before starting the assessment, gather:

1. **Session history** — Browse the session log directory for prior conversation logs (e.g. `~/.pi/agent/sessions/` in pi setups)
2. **Project files** — Read active project source code and documentation
3. **Data files** — Read the user's data files (tasks, goals, notes, configs)
4. **Skill definitions** — Review existing skills to understand the tool ecosystem
5. **Memory files** — Read context, memory, and any pending memory files (location varies by setup)

### Step 2: Evaluate Across Dimensions

Rate yourself on each dimension using the rubric below. Be **honest** — the user needs this to calibrate trust.

### Step 3: Produce the Report

Generate a structured assessment document using the template in Step 4.

## Assessment Dimensions

| # | Dimension | What to Evaluate |
|---|-----------|-----------------|
| 1 | **Code Continuity** | Can you read, edit, compile, and debug the user's active codebase? |
| 2 | **Tool Proficiency** | Do you have access to and fluency with the same tools (bash, read, edit, write, search)? |
| 3 | **Context Retention** | Can you retrieve and synthesize information from session history, memory files, and project docs? |
| 4 | **Domain Knowledge** | How deep is your understanding of the user's primary languages, frameworks, and problem domains? |
| 5 | **Workflow Familiarity** | Can you navigate the user's existing workflows without re-asking for setup or context? |
| 6 | **Nuanced Judgment** | Can you handle subjective/qualitative tasks (editing, prioritization, interpersonal communication)? |
| 7 | **System Internals** | How well do you understand the user's custom tools, extensions, and automation? |
| 8 | **Current State Awareness** | Do you know the current state of in-progress work, open issues, and pending decisions? |

## Confidence Rubric

| Score | Meaning | Guidance |
|-------|---------|----------|
| **10/10** | Fully capable, no degradation expected | "I can do everything the previous model did, same quality, same speed" |
| **9/10** | Minor gaps, fully functional | "I can do 95%+ of the work; a few things need a quick lookup or confirmation" |
| **8/10** | Solid but noticeable gaps | "I can handle most tasks; some areas need the user's patience or a ramp-up period" |
| **7/10** | Functional with significant caveats | "I can do core work but will be slower or less accurate in specific areas" |
| **6/10** | Partial capability, needs supervision | "I can attempt most things but need the user to verify or correct frequently" |
| **5/10 and below** | Limited capability | "I should be used for specific tasks only, not as a general replacement" |

## Report Template

Use this structure for your assessment document:

```markdown
# Model Self-Assessment Report

**Model:** [your model name and ID]
**Date:** [YYYY-MM-DD]
**User:** [username]
**Predecessors:** [list of previous models used]

---

## Overall Confidence: X/10

### Summary

[2-3 sentences. Honest summary of your readiness. What can you handle immediately? What needs ramp-up?]

---

## Dimension Scores

| Dimension | Score | Notes |
|-----------|-------|-------|
| Code Continuity | X/10 | [brief note] |
| Tool Proficiency | X/10 | [brief note] |
| Context Retention | X/10 | [brief note] |
| Domain Knowledge | X/10 | [brief note] |
| Workflow Familiarity | X/10 | [brief note] |
| Nuanced Judgment | X/10 | [brief note] |
| System Internals | X/10 | [brief note] |
| Current State Awareness | X/10 | [brief note] |

### Dimension Details

#### 1. Code Continuity (X/10)
[Detailed explanation. What languages, tools, build systems are involved? Have you successfully compiled/edited the project?]

#### 2. Tool Proficiency (X/10)
[What tools are available? Same environment? Any missing access?]

#### 3. Context Retention (X/10)
[How much session history is available? Memory files? How well can you cross-reference?]

#### 4. Domain Knowledge (X/10)
[Language expertise depth. Framework knowledge. Problem domain familiarity.]

#### 5. Workflow Familiarity (X/10)
[CLI commands, project structure, daily routines, file locations.]

#### 6. Nuanced Judgment (X/10)
[Subjective task ability. Editing quality. Interpersonal tone. Prioritization.]

#### 7. System Internals (X/10)
[Custom tools, extensions, automations, pi configuration.]

#### 8. Current State Awareness (X/10)
[In-progress tasks, known issues, pending decisions, recent changes.]

---

## What I Can Handle Immediately

- [List specific tasks/commands/workflows you're confident in]

## What Needs Ramp-Up

- [List areas where you need more context, testing, or user guidance]

## What I Cannot Do

- [List limitations — things you genuinely can't do or don't have access to]

---

## Recommendations

### For the User
- [Specific suggestions for how the user should work with you during the transition]
- [Anything they should double-check or verify]

### For Calibration
- [Suggest a simple test task the user can give you to validate your self-assessment]
- [Estimate how long until you're operating at full confidence]

---

*This assessment was generated using the Model Self-Assessment skill. Review it as a starting point — scores reflect the model's honest self-evaluation at the time of writing. Scores should be validated by the user through calibration tasks.*
```

## Usage Examples

### New Model Onboarding

When a new model is introduced to Kevin's workflow:

1. The model reads session history: `ls ~/.pi/agent/sessions/`
2. The model reads active projects: `cat ~/Developer/Rust/hpx/src/main.rs`
3. The model reads the data model: `cat ~/data/hpx/goals.md`
4. The model runs this assessment and produces a report
5. The user reviews and calibrates: "Yeah, 8/10 sounds right, but bump Nuanced Judgment to 9"

### Periodic Re-Assessment

Models can re-run this assessment after:
- Major project changes
- Extended breaks
- New tools, skills, or integrations added to the environment
- Significant session history growth (e.g. 50+ new sessions)

### Multi-Model Comparison

Run the same assessment with multiple models to produce a side-by-side comparison of capability and fit.

## Key Principles

1. **Honesty over optimism** — A 6/10 that's accurate is more useful than an 8/10 that's flattering
2. **Evidence-based** — Every score should reference specific data, not vibes
3. **Actionable** — The report should tell the user exactly what to expect and what to verify
4. **Dimensional** — Avoid a single overall number; break it down so the user knows where to trust you and where to be cautious
5. **Living document** — Re-assess as you learn. Update scores as you prove or disprove capabilities