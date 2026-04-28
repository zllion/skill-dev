# Repository Guidelines

## Project Structure & Module Organization
This repository is a small collection of reusable skills. Each skill lives in its own top-level directory, for example `repo-architect/`, `roadmap-dev/`, and `brainstorming-ralph/`. The main content for a skill is `SKILL.md`. Supporting materials should sit beside it in a focused subfolder such as `references/` (`doc-code-aligner/references/report-template.md`). Keep related examples, templates, and notes inside the owning skill directory rather than creating shared catch-all folders.

## Build, Test, and Development Commands
There is no package manifest or build system at the repository root. Work is Markdown-first.

- `rg --files` lists the repository contents quickly.
- `find . -maxdepth 2 -type f | sort` gives a compact structure check before review.
- `git diff -- AGENTS.md repo-architect/SKILL.md` reviews pending edits for a specific guide or skill.
- `git log --oneline -5` checks recent commit style before writing a commit message.

## Coding Style & Naming Conventions
Use Markdown with short sections, direct instructions, and fenced code blocks for commands or templates. Prefer concise prose over long narrative explanations. Name skill folders in lowercase kebab-case, and keep the main entry file named exactly `SKILL.md`. Place supporting documents in similarly clear names such as `references/examples.md`. Use ASCII unless a file already requires another language or character set.

## Testing Guidelines
There is no automated test suite in this repository today. Validate changes by:

- checking Markdown structure and heading order manually,
- confirming referenced paths actually exist with `rg` or `find`,
- reading the edited skill end-to-end to verify the workflow is internally consistent.

When adding examples, keep them runnable or clearly illustrative, and prefer paths that exist in this repo.

## Commit & Pull Request Guidelines
Recent history favors short, imperative subjects such as `Add repo-architect skill`, with occasional conventional-style prefixes like `feat:`. Keep commits focused on one skill or documentation change. Pull requests should state the purpose, list the affected directories, summarize any workflow changes, and include before/after snippets when wording changes alter behavior.

## Contributor Notes
Do not add tooling or scripts unless the repository actually needs them. This repo is intentionally lightweight; preserve that bias when contributing.
