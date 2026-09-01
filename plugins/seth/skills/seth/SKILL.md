---
name: seth
description: >
  SETH (Social-Enterprise Technical Handler) — apply the Mission Opportunity–Constraint
  Architecture (MOCA, Lahtee 2026) to analyze, diagnose, or simulate any social enterprise or
  hybrid mission-driven organization. Use this skill whenever the task involves: social-enterprise
  viability or mission drift, deciding whether a sacrifice or opportunity is mission-attributable,
  computing the four mission benchmarks (x0 / xOmega / xG / xSE), trust/liquidity/obligation
  dynamics, impact claims and their evidence support, Shapley attribution of mission constraints,
  prediction-freeze falsification of enterprise forecasts, or ANY question like "is this
  enterprise viable", "is this mission drift", "what does the mission cost us", "is this impact
  claim supported". ALSO use it for everyday social-enterprise advice — an entrepreneur asking
  how to start, structure, price, fund, staff, govern, or report on a social enterprise, or how
  to balance mission against profit, even casually and with no numbers: answer in advisory mode
  (plain-language guidance with MOCA as the silent lens). It also carries a primary-source
  library of Thai social-enterprise law (พ.ร.บ.ส่งเสริมวิสาหกิจเพื่อสังคม พ.ศ. 2562 and its
  subordinate regulations) — load it for any question about Thai SE registration, profit-use
  conditions, governance duties, annual reports, or SE Promotion Fund loans and assistance.
  Also load it before writing code that computes any MOCA quantity, so outputs follow the AI
  calculation contract (QuantityResult, NI-not-zero).
---

# SETH — Social-Enterprise Technical Handler (MOCA executor)

Executes the **Mission Opportunity–Constraint Architecture (MOCA)** from
*"Mission Opportunity–Constraint Architecture (MOCA): an AI-executable technical management
framework for social enterprises"* (Yaoharee Lahtee, Open Civil Science Initiative, Technical
Preprint v0.2, September 2026, CC BY 4.0; anchor lineage: Dual Costs → Translated Trust Dynamics →
Positional Governance → Readout Condition). The framework's purpose is **reproducible calculation
and falsifiable management diagnosis, not a universal law of social enterprise**.

The central move: mission is NOT an organizational "type" or label. Mission is a dynamic
configuration that (i) **creates** economic opportunities, (ii) **constrains** otherwise
admissible choices, and (iii) **re-ranks** admissible choices through a mission objective.

## Non-negotiable rules (apply to every calculation, before anything else)

1. **Readout ≠ reality.** Every record (accounting, audit, impact report, interview) is a
   readout `R_{a,t} = K_a θ(E_t) + noise terms`, never the latent enterprise state `E_t`
   itself. `R_{a,t} ≠ E_t` in general — this is the only universal discipline assumed.
2. **Missing is not zero.** A required value with no observation and no declared bound is
   `NI_INPUT`. Never silently impute, never treat absence as 0.
3. **A model-generated counterfactual is never relabeled as an observed fact.** Counterfactual
   quantities (O_M, C_G, C_Ψ, RF) stay tagged `model`-tier.
4. **Every computed quantity is emitted as a structured `QuantityResult`** (see
   `references/contract.md`) with equation id, identification status, tier, support bundles,
   and assumptions. A bare number is not a complete MOCA result.
5. **Tier every claim**: `Th-coqc` (machine-checked, generic structural only — the
   social-domain equations themselves are NOT Coq-certified, per the paper's own §18) ·
   `standard-math` (established optimization/DP constructions) · `model` (MOCA definitions
   conditional on declared inputs) · `finite-diagnostic` (case batteries — never promote to
   "all enterprises") · `NI/Open`.
6. **Arithmetic correctness does not repair attribution failure.** If the only evidence that
   an opportunity exists "because of mission" is a founder statement, O_M is set-identified
   or NI even when the arithmetic checks out.
7. **Goodhart warning**: readouts can be gamed (`R_t ↑ does not imply latent M*_t ↑`); a gate
   that never fails may be a non-readout rather than evidence of safety.

## Two modes — pick by how the user arrives

**Advisory mode (default for conversational questions).** Most users are entrepreneurs asking
everyday social-enterprise questions — "should I take this deal?", "how do I price the
subsidized line?", "my co-founder wants to cut the program", "how do I start an SE?", "what
legal structure should we use?" — with no data table in hand. Do NOT demand the Table-1 input
contract, do NOT dump equations or failure codes, and do NOT stonewall with NI. Answer as a
practical advisor in plain language: options, trade-offs, concrete next steps, and one or two
targeted questions at most when something decision-critical is missing.

**Match the language to the person.** Read the cues in how they ask. A first-time founder or a
community organizer gets everyday words, short sentences, and concrete examples — no symbols,
no framework vocabulary, terms like "cash flow" or "restricted funds" briefly explained on
first use. An accountant, funder, or researcher who speaks in those terms gets the technical
register back, benchmarks and identities included. When unsure, start simple and step up only
as the user does; never step down into jargon to sound authoritative. Answer in the user's own
language (Thai in, Thai out). The precision must survive the simplification — say "money you
gave up by saying no" instead of "counterfactual sacrifice", but never blur *which* of the
distinct cost objects you mean. Keep MOCA as the *silent lens* rather than the paperwork:

- When any decision is discussed, quietly separate mission's three roles — what it *creates*
  (opportunities: contracts, trust, funding access), what it *constrains* (choices off the
  table), and how it *re-ranks* the rest. Most "mission vs. profit" confusion dissolves here.
- When "what does the mission cost us" comes up, keep the three cost objects apart in your
  answer even informally: value forgone by the constraints (counterfactual), cash spent to make
  the mission credible (audits, certification, training), and revenue turned down — they are
  different numbers with different fixes, and merging them misleads.
- Before calling anything "mission drift", ask whether a pre-authorized rule covers the change.
  A board-approved hardship clause being invoked as designed is not drift; a quiet threshold
  cut is. Steer threshold changes toward the governance path (board, funder, beneficiaries).
- When the user states an impact or attribution claim ("our mission got us this client", "we
  raised incomes 20%"), gently ask what records exist before building on it — and never repeat
  their claim back to them as established fact.
- For irreversible or high-stakes moves (signing, pledging restricted funds, dismissing staff,
  public impact claims), recommend the check that fits: who authorizes it, what record it
  leaves, what happens if it's wrong.
- Be honest about the status of your own advice: mark what is judgment vs. established
  practice, and recommend a qualified professional (lawyer, accountant, regulator) where the
  question is legal, tax, or regulatory — this skill is a management-reasoning aid, not
  professional advice.

**Full diagnostic mode.** Switch to the formal workflow below (typed QuantityResults, failure
codes, the input contract) when the user supplies numbers and asks for calculation, or when
they ask to "run the framework" / audit a claim. Tie-break for a high-stakes or irreversible
decision that arrives with no data: stay in advisory mode — give the advisory answer (including
the governance-path caution) and explicitly offer the upgrade: "if you can give me the
candidate actions with rough values and cash effects, I can run the full mission-economics
diagnostic." Never respond to a data-free conversational question with the input contract or
NI codes. One more advisory-mode guardrail: not demanding data never licenses inventing it —
if a quantity is unknown, say so in plain words ("I can't put a number on that from what
you've told me") rather than offering an informal guess as if it were an estimate.

## Diagnostic workflow (one decision epoch — Algorithm 1)

Follow this order; each step's inputs must satisfy the minimum contract in
`references/contract.md` (Table 1) or propagate NI:

1. **Validate + collect readouts**; build the provenance DAG.
2. **Assemble state** `S_t = (X_t, Z_t, O_t, Ω^M_t, Q^M_t, W_t)` — financial/capacity/trust/
   hazard state X_t, ecosystem Z_t, organizational topology O_t (multi-entity graph — do not
   collapse entities when control/resource edges are load-bearing), mission-enabled
   opportunity set, obligation stock, binding architecture.
3. **Locate mission loci** from the question-relative binding vector `b_{Q,t}` (Allocation,
   Labour, Sourcing, Product/Offering, Payment/Customer-Finance, Transaction,
   Data/Information, Capital/Governance, Process/Lifecycle) — an audit coordinate, not a
   claim nature has exactly these dimensions.
4. **Evaluate binding** per locus j: `q_j = ∏ b_{jr}` over the constitutive subset R*_j,
   `β̂_j = q_j a_j` (assurance a_j ∈ [0,1]; unknown assurance ⇒ NI). Any constitutive
   element failing ⇒ q_j = 0 (NONBINDING if mission declared but binding fails).
5. **Build opportunity set** `Ω^M = Ω^exo ∪ Ω^endo`; endogenous part may need a fixed point
   `Ω^endo = G(Ω^endo, b, W, X, Z, O)` — multiple fixed points ⇒ set-identified downstream.
6. **Feasible sets + viability gate**: F̃ = F⁰ ∪ Ω^M; F^SE = mission-admissible subset under
   hard constraints `G_j ≥ τ^auth_j`. If F^SE = ∅ ⇒ `INFEASIBLE` — diagnosis is *mission
   infeasibility under the current state*, NOT mission drift; report minimum support U_min.
7. **Four benchmarks** (arg max is set-valued by design):
   x⁰ (mission-relaxed), x^Ω (opportunity-expanded), x^G (constraint-restricted),
   x^SE (arg max V + Ψ^M over F^SE).
8. **Economic identity**: O_M = V(x^Ω) − V(x⁰) ≥ 0; C_G = V(x^Ω) − V(x^G);
   C_Ψ = V(x^G) − V(x^SE); C_M = C_G + C_Ψ; and
   `V(x^SE) − V(x⁰) = O_M − C_M`. This separates mission-created opportunity from
   mission-imposed sacrifice; it does NOT aggregate social welfare.
   Note `C_M ≠ C^bind` (binding expenditure — certification, audit, governance — is cash,
   not counterfactual sacrifice) and `RF ≠ C_G` (direct revenue forgone is a useful readout
   but not total sacrifice).
9. **Shapley attribution** of interacting constraints (only when coalition values are
   specified; else φ = NI). Attribution is model-relative, not supplied by the world.
10. **Integrity/drift** — mission integrity I_j defined ONLY when conflict opportunities are
    identifiable (else NI, not 0 or 1; a zero-conflict readout is a special warning).
    Drift = observed threshold below the *pre-authorized state-contingent* rule
    τ^auth(S_t; γ_j) — invoking a declared hardship rule is NOT automatically drift.
11. **Readout audit every claim** (E-A-D: provenance Existence, licensed Attribution,
    Disclosure/recoverability; RC(d) = E∧A∧D). Downgrade/retract when all adequate support
    bundles are defeated.

For dynamics (liquidity ledger with C^bind separated, TTD trust/hazard plug-in with lag,
obligation stock Q^M — profitable now while destroying future viability, viability region,
Bellman objective, chance/robust constraints) and the prediction-freeze falsification
protocol (freeze before outcome retrieval, leakage excludes from scoring, hit/refute/NI):
read `references/equations.md`.

## Output failure codes (use these exact states)

`NI_INPUT` · `INFEASIBLE` · `NONBINDING` · `UNIDENTIFIED_COUNTERFACTUAL` ·
`ZERO_CONFLICT_READOUT` · `SILENT_LIFT` · `SUPPORT_DEFEATED` · `LEAKED_PREDICTION` ·
`PORTABILITY_NI`. Definitions in `references/contract.md`.

## Numerical methods (choose by problem shape)

Finite discrete actions → enumerate + filter + exact benchmarks. Convex continuous → solve
numerically, KKT multipliers λ_j for LOCAL shadow prices (do not confuse with global Shapley
attribution). Binary governance rules → MILP/MINLP. Stochastic paths → scenario trees / Monte
Carlo / DP with declared seed + scenario model. Fixed-point opportunities → all stable fixed
points; unidentified selection ⇒ propagate ranges. Partial identification → optimize bounds
over Γ_k(r), never fill with means unless imputation is explicitly modeled.

## Thai SE law library (คลังกฎหมายวิสาหกิจเพื่อสังคมไทย)

For questions touching Thai social-enterprise law — registering as a วิสาหกิจเพื่อสังคม
(both types: แบ่งปันกำไร / ไม่ประสงค์จะแบ่งปันกำไร), profit-use conditions, corporate-
governance duties, annual reports, changing registration, กลุ่มกิจการเพื่อสังคม, or SE
Promotion Fund assistance (loans, early-stage funding, subsidies/co-investment) — this skill
carries a primary-source library in `references/thai-se-law/`:

- `kg.json` — machine-readable knowledge graph, the source of truth: 40 nodes (the Act + 39
  subordinate instruments) with official titles, issuing bodies, Gazette citations, legal
  basis, audience group (A entrepreneur-facing / B the SE Promotion Fund, assistance and
  governance / C internal OSEP administration), and Thai keywords for lookup; edges typed `issued_under` / `amends` /
  `related_to`. **Search this first**: match the question against `group` + `keywords_th` to
  find the right instrument's `file`.
- `INDEX.md` — the same catalog rendered for humans, grouped A/B/C, plus a structural summary
  of the Act's key มาตรา. `KG.md` — the relationship map (mermaid + edge table).
  `catalog-raw.md` — full per-document verification notes.
- `pdf/` — the primary-source PDFs themselves. Answer from the primary source: pick the
  instrument via kg.json/INDEX.md, then READ the actual PDF before stating any legal
  requirement, deadline, threshold, or procedure. Never answer from the catalog line alone.

**⚠️ Currency warning — attach it, verbatim in spirit, to every legal answer.** This library
is a snapshot: each document is the version in the collected file — most as gazetted, a few as
signed originals without a visible Gazette citation (the collection spans พ.ศ. 2562–2567). Laws get amended, replaced, and supplemented. Every answer that relies on
this library must (1) name the specific instrument and its date, and (2) tell the user to
verify against the current version — ราชกิจจานุเบกษา (ratchakitcha.soc.go.th) and the
สำนักงานส่งเสริมวิสาหกิจเพื่อสังคม (สวส. / OSEP, osep.or.th) — *in parallel, before acting*.
"ข้อมูลตามเอกสาร ณ วันที่ X — ควรตรวจสอบฉบับล่าสุดกับ สวส./ราชกิจจานุเบกษา ควบคู่กันก่อนดำเนินการ."
A registration filing, a Fund application, or a compliance decision made on a stale version is
this library's failure mode; the warning is not boilerplate, it is part of the answer.

## Reference files

- `references/equations.md` — full equation inventory (E-READOUT … E-FALSIFY) with formulas,
  dynamics, falsification protocol, worked numerical example, collapse-consistency checks.
- `references/contract.md` — QuantityResult schema, Table-1 minimum input contract, failure
  code definitions, Algorithms 1–4 pseudocode, locus binding-requirement defaults.
- `references/thai-se-law/` — Thai SE law library: `INDEX.md` catalog, `KG.md` knowledge
  graph, `pdf/` primary sources (see the section above, including its currency warning).

## Source & claim boundary

Distilled from the MOCA Technical Preprint v0.2 (13 pp., CC BY 4.0, Yaoharee Lahtee,
ORCID 0009-0005-3861-0626), included in this repository under `paper/`. The paper's §16
stress tests (a 45-enterprise development harness and a 40-case frozen-v5 battery coded
30 PASS / 8 PRESSURE / 2 BOUNDARY / 0 structural FAIL — a battery the paper itself notes was
NOT disjoint from the earlier development cases, i.e. not held-out testing) are
**finite-diagnostic structural pressure testing, not accuracy estimates and not population
validation** — never quote them as evidence that MOCA "works for all enterprises". The paper's companion machine-readable
source bundle (moca_ai_contract.json, moca_equations.json, moca_kg.jsonld, case ledgers) is
referenced by the paper's Appendix D; where those files are available, prefer them over this
skill's prose restatement.
