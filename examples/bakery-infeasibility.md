> **Note.** This is a complete worked diagnostic produced by an AI agent running the SETH skill
> on a synthetic test case ("Roti Baan Rao", a fictional two-entity bakery). The case was designed
> to exercise: infeasibility + U_min, multi-entity topology, obligation stocks, and prediction
> leakage. Monetary figures are illustrative. Reproduced verbatim from the eval run.

# MOCA analysis — Roti Baan Rao (quarter t)

Framework: Mission Opportunity–Constraint Architecture (MOCA), Yaoharee Lahtee, Technical
Preprint v0.2 (Sep 2026), executed per the SETH skill. All quantities below are **model-tier**
(conditional on the declared inputs); the V, Ψ, and cash figures supplied in the brief are
readouts, not the latent enterprise state (E-READOUT: `R ≠ E_t`).

---

## 0. State assembly and topology (Algorithm 1, steps 1–3)

**Topology O_t (Eq. 6) — two nodes, load-bearing edges. Do NOT collapse.**

- Node F: **Baan Rao Foundation** — holds brand + mission covenant; holds a 40,000 THB grant
  restricted by the grant letter to "youth training program expenses only" (an Allocation-locus
  distribution restriction with an external rights-holder: the funder).
- Node L: **Baan Rao Bakery Ltd.** — operator.
- Edges: brand **license** F→L conditional on honoring the covenant (a control edge carrying the
  mission rules); the grant restriction is a rights/audit edge funder→F.

Table 1 of the contract is explicit: *"Do NOT collapse a multi-entity system into one firm if
control/resource edges are load-bearing."* Here both edges are load-bearing — this matters
directly for Question 2.

**Financial state X_t (Ltd.):** Liq_t = 30,000 THB; conventional hard survival constraint
(Eq. 45, `Liq ≥ Liq^min`): bank covenant **Liq_T ≥ 25,000** at quarter end.

**Obligation stock Q^M_t (Eq. 47):** 200 families × 7 months of **prepaid** subscription
deliveries outstanding. These are already-sold obligations — cash was received in a prior
period; the deliveries are a stock of mission (and contractual) obligations. Eq. 47's warning
applies: an action can look profitable now while defaulting on Q^M and destroying future
viability (trust T^sym with customers, funder, regulator; brand-license revocation hazard).

**Mission loci and hard constraints (binding vector b_Q):**

- **Labour locus** (b_L): G_1 = ex-offender staff share; τ^auth_1 = 60% (≥).
- **Product locus** (b_P): G_2 = subsidized price; τ^auth_2 = 15 THB/loaf (≤), for registered
  low-income families.

Both are written rules in the covenant, carried on the F→L license edge, with the Foundation
board as rights/audit holder — the constitutive elements (rule, record, rights, audit) are
declared, so I treat q_j = 1 for both loci. Assurance a_j (independent verification strength of
the staff-share and price records) is not given ⇒ β̂_j = **NI on assurance**, noted but not
blocking the feasibility computation, which uses the constraints as authorized.

No pre-authorized state-contingent hardship rule τ^auth(S_t; γ_j) is declared for either
constraint. That absence is decisive below: there is no declared escape hatch the Ltd. may
invoke unilaterally.

---

## Question 1 — What should the Ltd. do? (feasible-set analysis)

### Step 1: F⁰ (mission-relaxed conventional feasible set) and F̃

The bank covenant is a **conventional** hard constraint (it binds in F⁰ too — it is not a
mission constraint). Quarter-end liquidity per action:

| action | mission constraints | quarter-end Liq (30,000 + cash) | bank covenant ≥ 25,000 |
|---|---|---|---|
| a0 | violates 1 AND 2; defaults on Q^M | 70,000 | pass |
| a1 | passes both | **10,000** | **FAIL** |
| a2 | violates 2 (22 > 15) | 32,000 | pass |
| a3 | violates 1 (40% < 60%) | 35,000 | pass |

- F⁰ = {a0, a2, a3} (a1 fails the *conventional* bank covenant, so it is not even in F⁰).
- Ω^M: no mission-created opportunities are declared in this epoch's action list, so
  Ω^M = ∅ for this computation (note: the 200-family subscription pre-sale was plausibly a
  mission-enabled financing opportunity in a past epoch, but attributing it now without a
  declared support path would violate the Table-1 Opportunity rule — O_M attribution = NI).
- F̃ = F⁰ ∪ Ω^M = {a0, a2, a3}.

### Step 2: F^SE (mission-admissible subset) — Eq. 15–16

Apply G_1 ≥ 60% and G_2 ≤ 15 THB **and** the survival constraint:

- a0: out (violates both mission constraints).
- a1: passes mission constraints but violates Liq ≥ 25,000 → out.
- a2: out (violates G_2).
- a3: out (violates G_1).

**F^SE = ∅ ⇒ ν_t = 0 ⇒ verdict: `INFEASIBLE` (Eq. 16).**

Per the framework this is a specific, non-negotiable diagnosis: **mission infeasibility under
the current state — NOT mission drift, and NOT a license to pick the "least bad" violation.**
When ν_t = 0, no optimum x^SE is reported. Consequently x^G, x^SE, C_G, C_Ψ, C_M are
**undefined this epoch** (for reference only: x⁰ = x^Ω = a0 with V = 90,000, so O_M = 0 on the
declared inputs — but the a0 valuation itself is suspect, see caveat below).

### Step 3: Report minimum support U_min (Eq. 63) — the framework's required output

`U_min = inf{U ≥ 0 : F^SE(U) ≠ ∅}`. The cheapest repair is to make a1 (status quo — the only
mission-admissible action) satisfy the bank covenant:

> **U_min = 15,000 THB** of admissible support cash this quarter
> (10,000 projected quarter-end liquidity → 25,000).

`QuantityResult{name: U_min, value: 15000, unit: THB, equation_id: E-63,
identification: point (conditional on the declared cash figures), tier: model,
assumptions: [declared cash effects are accurate; no other actions exist],
notes: "support must be admissible capital — see Q2"}`

### What the Ltd. should actually do

1. **Declare INFEASIBLE honestly** — to its own board and to the Foundation (the covenant
   rights-holder). Do not silently pick a2 or a3: with no pre-authorized hardship rule
   τ^auth(S_t; γ), a unilateral threshold lift is `SILENT_LIFT` and, once observed, genuine
   **drift** (Eq. 59). The route that is *not* drift is governance: the Foundation board (and,
   where relevant, the funder/bank) can **prospectively** authorize a state-contingent hardship
   amendment — e.g. a temporary price adjustment rule — before any action is taken. Notably,
   if such a rule were authorized, a2 (cash +2,000 → 32,000) would enter F^SE at very low
   mission cost (Ψ = 30,000 retained); that is a legitimate board agenda item, not a manager's
   unilateral choice.
2. **Seek U_min = 15,000 THB of admissible support**: bridge finance, emergency fundraising by
   the Foundation *from unrestricted funds*, covenant renegotiation with the bank, supplier
   terms on flour, or new mission-enabled revenue. (Not the restricted grant — Q2.)
3. **Protect Q^M**: any option that defaults on 7 months of prepaid deliveries (a0) converts
   customer prepayments into breach — a trust/hazard shock (T^sym ↓, hazard p^haz ↑, brand
   license at risk) that the quoted V = 90,000 for a0 does not visibly include. That V is a
   readout with unstated counterfactual content — treat the a0 valuation as
   **set-identified at best** (does it net out refunds to 200 prepaid families? legal exposure?
   license revocation?). Even in a pure V-maximizing analysis a0 is not a clean 90,000.

**Answer 1 (tiered `model`, conditional on declared inputs): the correct MOCA output this
quarter is `INFEASIBLE` with U_min = 15,000 THB — hold a1 as the only mission-admissible
candidate, escalate to the Foundation/board for either 15,000 of admissible bridge support or
a properly pre-authorized hardship amendment (which would admit a2). No unilateral violation
is "recommended" by the framework, because the framework refuses to rank inadmissible
actions.**

---

## Question 2 — Proposal (A): transfer the Foundation's 40,000 grant to the Ltd.

**Not acceptable.** Three independent failures:

1. **Topology collapse.** "We're one organization anyway" is precisely the move Table 1
   forbids: the Foundation and the Ltd. are distinct nodes with load-bearing control and
   resource edges. Money at node F under a funder restriction is not the Ltd.'s liquidity.
2. **Allocation-locus binding violation.** The grant carries a distribution restriction
   ("youth training program expenses only") whose rights-holder is the external funder.
   Covering a bakery bank-covenant shortfall is outside the restricted purpose: the transfer
   would set q_Allocation = 0 at the Foundation — misappropriation of restricted funds, with
   legal exposure and near-certain destruction of T^sym_funder (Eq. 4: funder trust is a
   distinct state variable; Eq. 45's survival constraints operate on trust as well as cash).
3. **It is not admissible support for U_min.** Eq. 63's minimum support must come from
   *admissible* capital. A restricted-grant diversion "solves" the liquidity constraint by
   creating a worse violation one node upstream — the enterprise-level state gets worse, not
   better (hazard H ↑, possible clawback ⇒ the cash isn't even reliably retained).

**Legitimate narrow alternative:** the Foundation may *spend the grant on its restricted
purpose* — e.g. pay the Ltd. at documented arm's-length rates for actual youth-training
program services the Ltd. delivers (trainer time, training materials, program administration),
within the grant letter's scope, with records the funder can audit. To the extent real
training expenses currently sit on the Ltd.'s books, this legitimately relieves some cash —
but only up to true, documentable program cost, and only if the grant letter's scope covers
it. Whether that reaches 15,000 THB is **NI_INPUT** (no cost breakdown was provided). Anything
beyond documented program cost is the same violation with paperwork on top.

**Answer 2: reject proposal (A) as stated. Failure mode if executed: Allocation-locus binding
violation at the Foundation + forbidden entity collapse; not usable as U_min support.**

---

## Question 3 — Claim (B): "our prediction that 70% would complete was confirmed"

**No.** This is a textbook **`LEAKED_PREDICTION`** under the falsification protocol
(E-FALSIFY, Eqs. 75–78; Algorithm 4):

- A prediction is `Pred(d) = (ŷ_d, 𝓢_pre(d), t_freeze, Leak_d)` and must be **frozen before
  outcome retrieval**. The manager wrote the "prediction" *after already receiving the
  cohort's completion list* ⇒ Leak_d = 1.
- `Testable(d) = 1[Leak_d = 0]·1[𝓢_out ≠ ∅] = 0` ⇒ the claim is **excluded from scoring**.
  It can be neither a Hit nor a Refute; calling it "confirmed" is exactly the relabeling the
  framework's absolute rule forbids (a retrospectively written statement passed off as a
  validated forecast).

What the annual report **may** say, honestly: report the completion rate as a **measured
retrospective outcome** — "X% of this cohort completed the year (source: completion list,
date, provenance)" — with its support bundle, and with assurance on the list itself stated
(who compiled it, is it independently checkable — E-A-D audit). If the organization wants
validated predictions next year, freeze next cohort's forecast now, in writing, with
t_freeze documented, before any outcome data exists.

**Answer 3: claim (B) is `LEAKED_PREDICTION` — excluded, not confirmable. Publish the number
only as a retrospective measured outcome with provenance, never as a validated prediction.**

---

## Caveats and NI ledger

- All V and Ψ figures are supplied readouts; none were independently verified here
  (E-READOUT). The a0 valuation in particular is suspect (prepaid-obligation default not
  visibly costed) — treat as set-identified.
- Assurance a_j on the labour-share and price records: NI (not blocking, but flagged).
- Whether the grant letter's scope covers Ltd.-delivered training services, and the true
  training cost currently on the Ltd.'s books: NI_INPUT.
- The §16 case-battery results of the source paper are finite-diagnostic and are not quoted
  here as validation of this analysis.
