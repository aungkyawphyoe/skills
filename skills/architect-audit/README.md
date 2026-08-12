# architect-audit

A Claude Code skill that rescues a project from **drift** — where code, business logic, or the core idea has silently diverged from its original intent, usually after a long agent-driven build.

It reconstructs what the project was *supposed* to be, classifies where the drift happened, and writes a `RE-ALIGNMENT.md` that seeds a fresh, clean agent session. It is a **planning and brainstorming** tool: it never writes or changes code.

## When to use

Invoke it manually, the moment you feel "something's off" and can't name why — no scheduled checkpoints, no overhead during normal work. It complements (doesn't overlap) existing skills:

- **grill-me** pressure-tests an idea *before* you commit
- **code-review** audits the *diff* once you're in implementation
- **architect-audit** re-aligns the *whole project* when you've gone too deep to see the drift yourself

## The drift taxonomy

The skill classifies each divergence into one of three types, because the fix differs:

| Type | What it is | Fix direction |
|---|---|---|
| **Idea drift** | the core idea is flawed or was silently replaced | re-examine product assumptions, not code |
| **Business logic drift** | defined rules diverged through edits | re-derive from the source-of-truth |
| **Structure drift** | code structure diverged from the plan | plan a refactor, not a re-think of the idea |

## How it works

1. **Gate** — refuses to run if no git history / docs / CLAUDE.md exist to anchor the original intent. (If the skill guessed, it would just invent a "should-be" that matches what it finds.)
2. **Intake** — a short interview capturing your *felt* sense of wrong and your current mental model.
3. **Reconstruct "should-be"** — mines earliest commits, initial docs, and CLAUDE.md for original intent, each claim graded `artifact` / `inferred` / `memory`.
4. **Snapshot "as-is"** — a faithful read of the project as it stands.
5. **Diagnose** — surfaces deltas with evidence, typed by the taxonomy.
6. **Grill + re-align** — for each delta, **you** decide deliberate vs. accidental:
   - deliberate → **evolution**: the skill re-documents the *new* intent (never reverts)
   - accidental → **drift**: the skill adds it to the re-alignment plan as a defect
7. **Output** — writes `RE-ALIGNMENT.md`, shaped so a fresh session can pick up and work without the drifted context.

## Install

```sh
ln -s "$PWD" ~/.claude/skills/architect-audit
```

(Requires a skill-aware Claude Code version.)

## Usage

Open a Claude Code session inside the drifted project and invoke the skill:

```
/architect-audit
```

## Files

- `SKILL.md` — the skill itself (frontmatter + 6-phase procedure)
- `templates/re-alignment.md` — the output template the skill writes from
