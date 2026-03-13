---
name: roadmap-dev
description: Use when creating simple feature roadmaps for personal projects or small teams. Triggers on "create a roadmap", "track features", "feature list", "what's the plan", or "project status".
---

# Roadmap Dev

Create simple, maintainable feature roadmaps with markdown. No scripts, no complexity - just a clear view of what you're building.

## When to Use

- Personal project planning
- Simple feature tracking
- Small team coordination
- Quick status overviews

**Don't use for:**
- Complex enterprise roadmaps with multiple workstreams
- Detailed sprint planning with story points
- Scrum ceremonies or formal agile processes

## Core Pattern

**Simple structure, minimal tracking:**

```markdown
# [Project Name] Roadmap

## [Time Period: e.g., Q1 2026]

### Features
- [ ] Feature name - *optional notes or dependencies*
- [x] Completed feature
- [~] In progress feature - *depends on API from vendor*

### Milestones
- [~] Beta launch - *targeting end of quarter*
- [ ] Public release

## [Time Period: e.g., Q2 2026]

### Features
- [ ] Mobile app - *depends on API v2*
- [ ] Analytics dashboard

### Milestones
- [ ] Version 2.0
```

**That's it.** No scripts, no tables, no complex status systems.

## Status Values

Only 3 statuses - keep it simple:

- `[ ]` **Not Done** - Not started yet
- `[~]` **In Progress** - Currently being worked on
- `[x]` **Done** - Completed and deployed

## Time-Based Grouping

Organize features by time period:

- **Quarters:** Q1 2026, Q2 2026, Q3 2026, Q4 2026
- **Months:** January, February, March
- **Phases:** Phase 1, Phase 2, Phase 3
- **Releases:** v1.0, v1.1, v2.0

Choose what makes sense for your project. Be consistent.

## Dependencies

Mention dependencies in italics after the feature name:

```markdown
- [ ] Search feature - *depends on Elasticsearch setup*
- [ ] Payment integration - *blocked on Stripe account*
- [~] User dashboard - *waiting for design mockups*
```

Keep it brief. This is for your reference, not formal dependency tracking.

## Milestones vs Features

**Features** = work items you build
**Milestones** = significant events or achievements

Both use the same 3 statuses:

```markdown
### Features
- [~] User authentication
- [ ] Profile pages

### Milestones
- [x] MVP complete
- [~] Private beta
- [ ] Public launch
```

## Quick Reference

| What | How |
|------|-----|
| Mark not started | `- [ ] Feature name` |
| Mark in progress | `- [~] Feature name` |
| Mark done | `- [x] Feature name` |
| Add dependency | `- [ ] Feature - *depends on X*` |
| Add note | `- [ ] Feature - *any context*` |
| Track changes | Use git: `git diff`, `git log` |

## Common Mistakes

**❌ Over-complicating status:**
```markdown
- [ ] Feature (blocked on API, waiting for review, at risk)
```
Use the notes field for context, don't invent new statuses.

**❌ Creating complex tables:**
```markdown
| Feature | Status | Priority | Owner | Date | Dependencies |
```
Tables are harder to maintain. Simple lists scale better.

**❌ Multiple status systems:**
```markdown
- [~] Feature (In Progress, 50% complete, started 2026-03-01)
```
One status per feature. Keep notes brief.

**❌ Forcing Now/Next/Later:**
```markdown
## Now
## Next
## Later
```
Use time periods that match your project. Now/Next/Later is just one option.

## Real-World Impact

**Before (with scripts):**
- 97-line roadmap file
- 3 Python scripts to maintain
- 7 different statuses
- Command-line syntax with 7 parameters
- Table formatting bugs

**After (simplified):**
- 20-line markdown file
- No dependencies
- 3 statuses
- Edit with any text editor
- Works everywhere

## Example: Complete Roadmap

```markdown
# Side Project Roadmap

## Q1 2026

### Features
- [x] Project setup
- [x] User authentication - *used Auth0*
- [~] Dashboard UI - *waiting on design feedback*
- [ ] API integration - *depends on vendor docs*
- [ ] Mobile responsive design

### Milestones
- [x] MVP scope defined
- [~] Alpha release - *internal testing*
- [ ] Beta signup page live

## Q2 2026

### Features
- [ ] Data export feature - *CSV and PDF*
- [ ] Search and filtering
- [ ] User settings page
- [ ] Performance optimization

### Milestones
- [ ] Public beta
- [ ] First paying customer
- [ ] v1.0 launch

## Q3 2026

### Features
- [ ] Mobile app (iOS)
- [ ] Advanced analytics
- [ ] Team collaboration features

### Milestones
- [ ] 100 users
- [ ] Mobile app store approval
```

## Maintenance

**Weekly:** Update status of current features
**Monthly:** Review upcoming quarter
**Quarterly:** Archive completed quarter, plan next one

**Use git for history:**
```bash
git add ROADMAP.md
git commit -m "Update Q1 roadmap: Dashboard now in progress"
git log --oneline ROADMAP.md  # See history
```

No change log section needed - git tracks everything.

## The Bottom Line

Simple markdown lists. Three statuses. Time-based grouping. Nothing more.

If you're adding scripts, tables, or complex status systems, you've over-engineered it. Start over with just the basics.
