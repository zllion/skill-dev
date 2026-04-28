---
name: repo-architect
description: >
  Use when analyzing an unfamiliar repository, documenting codebase architecture,
  or explaining how a project is structured, how its main flows work, and why it
  is designed that way.
---

# Repo Architect

Analyze a repository and produce structured docs in `docs/analysis/` using a **总分总** (overview → spotlights → synthesis) structure.

Skills may reference Claude Code tool names. On other platforms, use the closest equivalent tools and agent workflows.

## Input

- Nothing → analyze current working directory
- Local path: `/path/to/repo`
- GitHub URL or `owner/repo`: if the current environment allows remote access and temporary filesystem writes, clone to `/tmp/repo-architect-<name>`, analyze, then delete. Otherwise, ask for a local path or analyze the current repository only.

## Step 1: Overview Analysis

Announce: "Using repo-architect to analyze this repository."

Start with fast scoping before deep analysis:

- Identify the primary manifests, entry points, and top-level packages first
- Exclude obvious noise such as build outputs, vendored dependencies, generated files, and large lock or cache directories
- If the repository is large, prioritize the main application path and the modules it directly depends on instead of trying to cover every package equally

Analyze the repo directly using Glob, Grep, Bash, and Read tools across 4 dimensions:

**Structure** — directory tree (3 levels), manifest files, tech stack, entry points

**Modules** — top-level packages or major directories, each module's responsibility, key public symbols or entry files with `file:line`

**Flows** — 2–3 key user-facing flows traced from entry to output with `file:line` at each step

**Tech Decisions** — 3–5 notable technical choices, rationale, and plausible alternatives grounded in visible code or configuration

Write a single overview document:

> `docs/analysis/overview.md` — 中文；项目摘要、结构、模块、流程、技术栈、关键设计决策

## Step 2: Spotlight Selection (required user negotiation)

Do not jump directly from `overview.md` to a final spotlight list. Build the candidate set progressively.

### 2.1 Build an Architecture Map

First, group the repository into major architectural areas. Use the repo's actual structure rather than a fixed taxonomy. Common examples include:

- Core entry points and main user flows
- Domain modules or service boundaries
- Shared infrastructure and internal platforms
- Distinctive mechanisms, algorithms, or data pipelines
- Performance-sensitive paths
- External integrations and system boundaries

### 2.2 Expand Candidate Spotlights

Within each architectural area, identify candidate spotlights that are worth deep-diving. A spotlight is justified when it helps explain the repository in a way the overview cannot.

Good spotlight types include:

- Novel algorithms or data structures
- Non-obvious architectural patterns
- Performance-critical subsystems
- Interesting design tradeoffs
- Key abstractions that unlock the rest of the codebase

Generate enough spotlight candidates to cover the repository's meaningful complexity.
Start with the most central architectural areas, then keep expanding until the candidate list captures the major subsystems, distinctive mechanisms, and important tradeoffs without devolving into a file-by-file dump.
For large or layered repositories, it is expected that the spotlight list may grow well beyond 5 items.

For each candidate, note:

- What it is
- Why it matters
- Whether it is central, supporting, or optional for understanding the repository
- What other spotlights or flows it connects to

### 2.3 Negotiate Spotlight Scope With the User

Present the grouped candidate set to the user in a way that supports explicit scope discussion:

```
Found N spotlight candidates across M areas:

Area A: [name]
  1. [candidate] — [why it matters]
  2. [candidate] — [why it matters]

Area B: [name]
  3. [candidate] — [why it matters]
  4. [candidate] — [why it matters]

Recommended for the first round: [numbers]
Optional but valuable: [numbers]
Deferred unless requested: [numbers]

Please confirm:
- which spotlights to analyze now,
- which areas need more candidate expansion,
- whether any important area is missing.
```

The user must explicitly confirm the spotlight scope before any deep-dive reports begin.
If the user says the list is incomplete, too broad, or misprioritized, revise the candidate set and ask again.
Repeat until the spotlight scope is explicitly confirmed.

## Step 3: Parallel Spotlight Reports

Only begin this step after the user has explicitly confirmed the spotlight scope.

For each confirmed spotlight, use parallel subagents if the current platform supports delegation. Otherwise, generate the deep-dive reports sequentially in the main session.

Each subagent or main-session pass should receive:
- The repo path
- The specific spotlight topic
- Instructions to produce a deep-dive report (see template below)

Each subagent writes its report to `docs/analysis/<N>-<slug>.md` where N is the spotlight number (1, 2, 3...).

### Spotlight Report Template

**All reports must be written in Chinese (中文).** Each report must include:
1. **是什么** — 简洁描述
2. **为什么重要** — 解决了什么问题，为什么这个方案不显而易见
3. **如何工作** — 逐步说明，附 `file:line` 引用和代码片段
4. **设计权衡** — 得到了什么，牺牲了什么
5. **横向对比** — 与代码中可见替代方案、常见实现路径或相关竞品的比较；若涉及仓库外信息，先验证来源，再明确区分“代码可证实事实”与“经验性推断”

## Step 4: Synthesis

After all spotlight reports are written, write one final document **in Chinese**:

**`docs/analysis/guide.md`** — 开发指导与未来设计，包含：
- 开发环境搭建
- 建议阅读顺序（关键文件）
- 如何添加新功能/模块/后端
- 常见陷阱
- 当前架构局限性
- 自然扩展点
- 代码中可见的开放设计问题（TODO/FIXME）
- 与竞品的差距与改进方向；涉及仓库外信息时，先验证来源，并明确区分“代码可证实事实”与“经验性推断”

## Step 5: Report

```
✓ Analysis complete → docs/analysis/
  - overview.md        (中文)
  - 1-<slug>.md        (中文)
  - 2-<slug>.md        (中文)
  - ...
  - guide.md           (中文)
```
