# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A collection of Claude Code skills. Each skill is a directory under `skills/` that gets symlinked into `~/.claude/skills/` so it's available across projects. Currently contains one skill: `architect-audit`.

## Skill anatomy

Every skill directory follows the same layout:

- `SKILL.md` — the skill definition and entry point. Frontmatter must include `name` (kebab-case) and `description` (the trigger text Claude Code matches against). The body is the procedure the skill runs.
- `README.md` — human-facing docs: when to use it, how it works, install steps.
- `templates/` — output templates the skill writes from. `architect-audit` writes `RE-ALIGNMENT.md` into the audited project from `templates/re-alignment.md`.
- `.claude/settings.local.json` — permission allowlist scoped to the skill. `architect-audit` is read-only, so it only allows a few read-only Bash commands.

## Conventions

- **Skills are self-contained.** A fresh session invokes the skill with no context, so `SKILL.md` must carry everything the skill needs — rules, phases, and output format.
- **Skills define their own output artifacts.** The written output (e.g. `RE-ALIGNMENT.md`) must be self-sufficient enough for a fresh, context-free session to act on it without the audit conversation.
- **Planning-only skills state so explicitly and never modify project files.**
- Anything beyond this in `SKILL.md` (the drift taxonomy, `artifact`/`inferred`/`memory` confidence grades, the phases) is specific to `architect-audit`, not a repo-wide convention.

## Commands

There is no build, test, or lint step — skills are plain markdown. The workflow is:

- Install a skill (from repo root): `ln -s "$PWD/skills/<name>" ~/.claude/skills/<name>`
- Verify: open a Claude Code session in a target project and invoke `/architect-audit` (or the new skill's name) to confirm it loads and runs.
