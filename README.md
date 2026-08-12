# AI Agent Skills

[![skills.sh](https://skills.sh/b/aungkyawphyoe/skills)](https://skills.sh/aungkyawphyoe/skills)

A collection of skills for AI coding agents. Each skill lives in its own directory under `skills/` and is installed by symlinking it into your agent's skills directory so it's available across projects.

Skills are self-contained, plain-markdown definitions — there is no build or test step.

## Included skills

| Skill | Description |
|---|---|
| **[architect-audit](skills/architect-audit/README.md)** | Diagnose project drift and recover original intent. Reconstructs what a project was *supposed* to be from its own history, classifies where it diverged (idea / business logic / structure), and writes a `RE-ALIGNMENT.md` to seed a fresh session. Planning and brainstorming only — never writes or changes code. |

## Installation

From the repo root, symlink each skill into your agent's skills directory:

```sh
ln -s "$PWD/skills/<name>" <agent-skills-dir>/<name>
```

For example, for Claude Code (`~/.claude/skills/`):

```sh
ln -s "$PWD/skills/architect-audit" ~/.claude/skills/architect-audit
```

Requires an agent that supports skills.

## Usage

Open a session in your coding agent inside the project you're working on and invoke the skill:

```
/architect-audit
```

## Adding a new skill

1. Create `skills/<name>/` with a `SKILL.md` — frontmatter must include a `name` (kebab-case) and a `description` (the trigger text the agent matches against).
2. Add a `README.md` documenting when to use it and how it works.
3. Symlink it as described above.

## Summary

This repository collects reusable skills that any AI coding agent can load on demand. Each skill is a self-contained procedure — including its own rules, phases, output artifacts, and scoped permissions — so a fresh session can invoke it with no context and work correctly. The collection grows as skills are added.
