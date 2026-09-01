# SETH — Social-Enterprise Technical Handler

**An AI skill that executes MOCA — the Mission Opportunity–Constraint Architecture — so that
social-enterprise analysis becomes reproducible calculation instead of narrative.**

SETH is a [Claude Code skill](https://docs.claude.com/en/docs/claude-code) (plain-Markdown
instructions — portable to any LLM agent that can read files) implementing the framework of:

> Yaoharee Lahtee, *Mission Opportunity–Constraint Architecture (MOCA): an AI-executable
> technical management framework for social enterprises.* Technical Preprint v0.2, Open Civil
> Science Initiative, September 2026. CC BY 4.0. ORCID
> [0009-0005-3861-0626](https://orcid.org/0009-0005-3861-0626).
> The full paper is included in [`paper/`](paper/).

## Why

Social enterprises are usually discussed through labels ("hybrid", "impact-driven") and
unfalsifiable claims ("our mission earned us this contract", "we increased farmer income 20%").
MOCA's move is to stop treating mission as a *type* and represent it as a dynamic configuration
that (i) **creates** economic opportunities, (ii) **constrains** otherwise admissible choices,
and (iii) **re-ranks** admissible choices through a mission objective — and then to demand that
every computed quantity carry its provenance, identification status, and tier.

What the skill enforces, mechanically:

- **Readout ≠ reality.** Accounting records, audits, impact reports, and interviews are typed
  as *readouts* of a latent enterprise state, never the state itself.
- **Missing is not zero.** An unobserved required value is `NI` — never silently imputed.
- **The four benchmarks and the central identity.** x⁰ (mission-relaxed), x^Ω
  (opportunity-expanded), x^G (constraint-restricted), x^SE (mission optimum), with
  `V(x^SE) − V(x⁰) = O_M − C_M`: mission-created opportunity separated from mission-imposed
  sacrifice — and both separated from binding *cash* expenditure `C^bind` (no double counting).
- **Infeasibility is a diagnosis, not a failure to answer.** When no action satisfies the
  mission constraints, the output is `INFEASIBLE` plus the minimum support `U_min` that would
  restore feasibility — not a quiet recommendation to break the "softest" constraint.
- **Drift vs. authorized hardship.** Lowering a mission threshold under a pre-authorized
  state-contingent rule is *not* drift; lowering it because cash is tight is.
- **Attribution discipline.** A founder's statement that an opportunity "came from the mission"
  is not an adequate support bundle: the quantity is set-identified or `NI`, even when the
  arithmetic is internally correct.
- **Prediction-freeze falsification.** A "prediction" written after the outcome was seen is
  `LEAKED_PREDICTION` — excluded from scoring, never "confirmed".
- **Typed outputs.** Every quantity is a `QuantityResult` (equation id, identification status,
  tier, support bundles, assumptions). A bare number is not a complete result.

And it meets entrepreneurs where they are: casual questions ("should I take this deal?",
"how do I start a social enterprise?", "how do I price the subsidized line?") get
**advisory mode** — plain-language options, trade-offs, and next steps with MOCA as the silent
lens, the register matched to the asker (everyday words for a first-time founder, the technical
vocabulary for an accountant or funder, answers in the user's own language) — while supplied
numbers with a request to calculate, or an explicit "run the framework", get the full typed
diagnostic — a high-stakes question with no data stays advisory, with an explicit offer to
upgrade.

## Install

As a Claude Code plugin:

```
/plugin marketplace add morrocwi/seth-skill
/plugin install seth@yaoharee-lahtee-seth
```

Or manually: copy `plugins/seth/skills/seth/` into your agent's skills directory
(`~/.claude/skills/seth/` for Claude Code).

## What's inside

| Path | Contents |
|---|---|
| `plugins/seth/skills/seth/SKILL.md` | The skill: non-negotiable rules, the one-epoch diagnostic workflow, failure codes, numerical-method selection |
| `.../references/equations.md` | Full equation inventory (E-READOUT … E-FALSIFY, eqs. 1–85) with the dynamics, governance, inference, and falsification layers |
| `.../references/contract.md` | The AI calculation contract: `QuantityResult` schema, minimum-input Table 1, failure-code definitions, Algorithms 1–4 pseudocode, per-locus binding defaults |
| `.../references/thai-se-law/` | Thai SE law library: the พ.ร.บ.ส่งเสริมวิสาหกิจเพื่อสังคม พ.ศ. 2562 + 39 subordinate instruments as primary-source PDFs, with a verified machine-readable knowledge graph (`kg.json`), human catalog (`INDEX.md`), and relationship map (`KG.md`). Snapshot as gazetted (2562–2567) — every legal answer must be re-verified against the current version (ราชกิจจานุเบกษา / OSEP) before acting |
| `paper/` | The MOCA technical preprint (PDF, CC BY 4.0) |
| `examples/` | Two full worked diagnostics produced by an agent running this skill (a coffee shop and a two-entity bakery) |
| `benchmarks/` | Honest finite-diagnostic comparison of agent-with-skill vs. agent-without-skill on those two cases |

## Worked examples

- [`examples/coffee-shop-diagnostic.md`](examples/coffee-shop-diagnostic.md) — a feasible case:
  four benchmarks computed, O_M = 0 shown *robust* to an unresolved attribution question,
  C_M vs. C^bind kept separate, a drift verdict under a hardship rule that has not triggered,
  and an impact claim audited down to `NI`.
- [`examples/bakery-infeasibility.md`](examples/bakery-infeasibility.md) — an infeasible case:
  `INFEASIBLE` with `U_min` computed, a two-entity topology defended against "we're one
  organization anyway", an obligation-stock default surfaced inside a tempting valuation, and a
  leaked prediction excluded.

## Evidence status (read this before quoting numbers)

Everything here follows the paper's own tier discipline:

- The paper's stress tests (a 45-enterprise development harness; a later 40-case battery coded
  under a frozen v5 architecture — but, as the paper itself states, **not disjoint from the
  earlier development cases**, so not held-out testing) are **finite-diagnostic structural
  pressure testing — 30 PASS / 8 PRESSURE / 2 BOUNDARY / 0 structural FAIL is not an accuracy
  estimate, not population validation, and not a ranking of the organizations named**.
- The benchmark in [`benchmarks/`](benchmarks/README.md) is n = 2 cases, one run each, no
  variance data — it is a worked demonstration, not proof of effectiveness. Its most honest
  finding: a strong base model already refuses leaked predictions and unsupported impact claims
  without the skill; the skill's distinctive value concentrated in the **economic decomposition
  layer** (O_M / C_G / C_Ψ / C_M vs. C^bind — where the unaided baseline made real conceptual
  errors) and in **readout suspicion** (questioning a suspiciously clean valuation).
- The social-domain equations are **not** machine-verified; the paper's formal repository
  covers generic structural results only (paper §1.1, §18).

## License

- The MOCA paper (`paper/`) is © Yaoharee Lahtee, released under
  [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- The skill files, references, examples, and benchmark notes in this repository are likewise
  released under [CC BY 4.0](LICENSE).

## Citing

If you use SETH or MOCA, cite the technical preprint (see [`paper/`](paper/)) and this
repository:

```
Lahtee, Y. (2026). Mission Opportunity–Constraint Architecture (MOCA): an AI-executable
technical management framework for social enterprises. Technical Preprint v0.2,
Open Civil Science Initiative.

Lahtee, Y. (2026). SETH — Social-Enterprise Technical Handler (Claude skill).
https://github.com/morrocwi/seth-skill
```
