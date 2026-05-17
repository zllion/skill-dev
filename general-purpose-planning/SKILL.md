---
name: general-purpose-planning
description: Use when creating plans for any domain or task, especially when goals, constraints, tradeoffs, research needs, multiple options, local markdown artifacts, or independent plan reviews matter.
---

# General Purpose Planning

## Overview

Create comparison-ready plans for any domain: fitness, debugging, business, travel, research, learning, operations, creative work, or personal projects.

**Core principle:** Do not optimize one imagined path before the goal, constraints, evidence, and alternatives are explicit.

## Required Flow

1. Confirm the planning frame.
2. Research and reason before drafting.
3. Create multiple meaningfully different plans.
4. Save each plan as its own markdown file.
5. Launch exactly one independent reviewer per plan.
6. Summarize tradeoffs without choosing for the user unless asked.

## 1. Confirm the Planning Frame

Before writing plans, establish:

- Goal and success criteria
- Scope: included and excluded
- Constraints: time, budget, energy, tools, location, people, health, legal, technical, cultural, or ethical limits
- Risk tolerance: conservative, balanced, aggressive, experimental
- Time horizon and milestones
- Output location and naming preference, if any

If critical information is missing, ask concise grouped questions and wait. Usually ask 3-7 questions. "Move fast" makes the clarification round shorter; it does not remove it.

If the user explicitly asks to proceed without answers, write assumptions at the top of every plan.

## 2. Research and Reason First

Do enough investigation before proposing plans:

- Use local files, user context, logs, datasets, docs, or notes when relevant
- Use web search for current facts, prices, laws, schedules, medical/safety guidance, market data, or recent tools
- Separate verified facts, user constraints, and assumptions
- Identify decision variables before drafting options

Never invent current facts. If research is blocked, state the gap and make plans conditional.

## 3. Propose Multiple Plans

Create at least two plans unless the user requested a specific number. Options must differ by real strategy, resource profile, risk posture, timeline, or cost.

Useful option types: conservative, balanced, aggressive, experimental, minimal, premium.

Artifacts, checklists, scorecards, and research notes can support the work, but they do not count as plan options.

## 4. Save Separate Markdown Files

Create a task folder, usually:

```text
plans/<task-slug>/
```

Save one file per plan:

```text
plans/<task-slug>/plan-01-<strategy>.md
plans/<task-slug>/plan-02-<strategy>.md
plans/<task-slug>/plan-03-<strategy>.md
```

Each plan must include: goal, assumptions, audience/context, constraints honored, strategy summary, phases or timeline, resources and estimated cost, risks and mitigations, stop conditions, research basis, open questions, and next decision.

## 5. Review With One Agent Per Plan

After writing `N` plan files, launch exactly `N` independent reviewers if the platform supports subagents or agent teams.

Each reviewer gets one plan and evaluates feasibility, cost realism, risks, hidden assumptions, constraint violations, missing research, and decision quality.

Save one review file per plan:

```text
plans/<task-slug>/review-01-<strategy>.md
plans/<task-slug>/review-02-<strategy>.md
plans/<task-slug>/review-03-<strategy>.md
```

Reviewers evaluate; they do not rewrite plans. If delegation is unavailable, say so and run separate main-session review passes, one per plan.

## 6. Final Summary

Report plan files, review files, best fit by user priority, major tradeoffs, key risks, and the next decision or missing information.

## Quick Reference

| Step | Required Output |
|------|-----------------|
| Frame | Goal, success criteria, constraints, risk tolerance |
| Research | Facts, assumptions, decision variables |
| Draft | 2+ different strategy options |
| Save | One markdown file per plan |
| Review | One reviewer and one review file per plan |
| Summarize | Comparison and next decision |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Drafting immediately | Clarify goal and constraints first |
| Making cosmetic variants | Vary strategy, resources, timeline, cost, or risk |
| Skipping research | Verify unstable or high-stakes facts |
| Saving all plans together | Use one markdown file per plan |
| Counting artifacts as plans | Count only standalone strategy options |
| One reviewer for all plans | Launch exactly one reviewer per plan |
| Reviewers rewrite plans | Reviewers evaluate only |
| Choosing too early | Present tradeoffs unless asked to choose |

## Red Flags

Stop if you catch yourself saying:

- "I'll just draft a quick plan first."
- "They said move fast, so I can skip clarification."
- "These options are basically the same."
- "A checklist and a scorecard count as plan options."
- "One review summary is enough."
- "Research can happen after the plan."
- "The user can infer the assumptions."
