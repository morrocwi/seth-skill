# Benchmark — agent-with-skill vs. agent-without-skill

**Status: finite-diagnostic only.** n = 2 synthetic cases, one run per configuration, same
model for both arms, no variance data. This is a worked demonstration of what the skill does
and does not add — it is **not** proof of effectiveness and must never be quoted as
"SETH improves analysis by X%".

Each case was graded against 6 pre-written assertions; grading was done against the produced
analysis files, not the agents' self-reports.

| Case | With skill | Without skill | Tokens (with / without) |
|---|---|---|---|
| Coffee shop (feasible; attribution + drift + impact-claim traps) | 6/6 | 4/6 | 75.8k / 55.2k |
| Bakery (infeasible; topology + obligation + leakage traps) | 6/6 | 6/6 in substance | 73.9k / 55.6k |

## Discriminating findings (where the skill changed the outcome)

- **Economic decomposition.** The unskilled baseline conflated MOCA's mission opportunity
  value O_M with the constraint sacrifice (reporting the V forgone to constraints as
  "opportunity value"), and merged binding cash expenditure C^bind into the counterfactual
  mission cost C_M — exactly the two separations MOCA's eq. 26 and eq. 35 exist to enforce.
  The skilled run computed the four benchmarks, the O_M − C_M identity (with check), and kept
  the categories separate.
- **Readout suspicion.** In the bakery case, the skilled run flagged that the tempting
  action's stated valuation did not visibly cost its own prepaid-obligation default and
  brand-license risk, downgrading it to set-identified. The baseline took the number at face
  value.
- **Formalization.** The skilled runs emitted typed `QuantityResult`s, failure codes, and an
  explicit `U_min` (minimum viability support) — auditable outputs rather than prose.

## Non-discriminating findings (honesty about what the base model already does)

On both cases, the unskilled baseline independently: refused to treat a post-hoc "prediction"
as confirmed (naming it postdiction/HARKing), refused an unsupported "+20% impact" claim,
refused to collapse two legal entities or divert a restricted grant, and refused to resolve an
empty feasible set by quietly breaking the softest constraint. A strong general model brings
this integrity layer without the skill; the skill's distinctive value is the calculation
architecture on top of it.

## Cost

The skill added roughly one third more tokens and ~50% more wall time per run in these two
cases.

## Reproducing

The two test-case prompts and the full assertion lists are in [`PROMPTS.md`](PROMPTS.md),
verbatim. Run them with and without `plugins/seth/skills/seth/` available to your agent and
grade the outputs against the assertions.
