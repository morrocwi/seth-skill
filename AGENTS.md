# AGENTS.md - seth-skill

## What this repository is

SETH (Social-Enterprise Technical Handler) is an AI skill that executes MOCA - the Mission
Opportunity-Constraint Architecture - so that social-enterprise analysis becomes reproducible
calculation instead of narrative. It is a Claude Code skill (plain-Markdown instructions, portable
to any LLM agent that can read files) implementing the framework of the MOCA technical preprint
included in `paper/`.
Evidence status, as the README states it: the paper's stress tests are finite-diagnostic structural
pressure testing (the later case battery is not disjoint from the earlier development cases, so not
held-out testing) - not an accuracy estimate, not population validation, and not a ranking of the
organizations named. The benchmark in `benchmarks/` is n = 2 cases, one run each, no variance data: a
worked demonstration, not proof of effectiveness. The social-domain equations are not machine-verified.

## Read first

1. `README.md` - what the skill enforces, and "Evidence status (read this before quoting numbers)".
2. `plugins/seth/skills/seth/SKILL.md` - the skill: non-negotiable rules, workflow, failure codes.
3. `plugins/seth/skills/seth/references/contract.md` - the AI calculation contract.

## Rules

These are rules the README already states; this file adds none of its own.

- Readout is not reality: records, audits, impact reports and interviews are typed as readouts of
  a latent enterprise state, never the state itself.
- Missing is not zero: an unobserved required value is `NI`, never silently imputed.
- Every quantity is a `QuantityResult`; a bare number is not a complete result.
- A "prediction" written after the outcome was seen is `LEAKED_PREDICTION`: excluded from scoring,
  never "confirmed".
- The Thai SE law library is a snapshot; every legal answer from it must be re-verified against the
  current version before acting.

## Programme map

This repository is one node of the Human-AI Readout Programme. Which repository answers which kind of
question, what to read first and which gate applies is kept in one place, the routing hub:
<https://github.com/morrocwi/main.hub> (start at its `AGENTS.md`, then `ROUTES.md`).
The hub holds pointers and pinned links only. It is a readout of one moment: when the hub and this
repository disagree, this repository wins.
