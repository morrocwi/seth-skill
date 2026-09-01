> **Note.** This is a complete worked diagnostic produced by an AI agent running the SETH skill
> on a synthetic test case ("Baan Kafae Jaidee", a fictional coffee shop). The case was designed
> to exercise: benchmark computation, attribution discipline, drift vs. hardship rules, and an
> impact-claim audit. Monetary figures are illustrative. Reproduced verbatim from the eval run.

# MOCA diagnostic — Baan Kafae Jaidee (quarterly epoch)

Framework: Mission Opportunity–Constraint Architecture (MOCA), Yaoharee Lahtee, Technical
Preprint v0.2 (Sep 2026), executed per the SETH skill (Algorithm 1, one-period diagnostic).
All social-domain quantities below are **model-tier** (conditional on declared inputs), not
Coq-certified, and all input records are readouts, not the latent enterprise state
(E-READOUT: `R_{a,t} != E_t`).

---

## 0. State, mission architecture, and binding evaluation

**State readouts (X_t, partial):** Liq_t = 250,000 THB; CF^op = 60,000; C^bind = 15,000
(sign-language training + social audit — binding expenditure, NOT counterfactual sacrifice,
per E-CASH eq. 35); DS = 10,000. Trust variables T^op, T^sym, hazard H_t: **NI_INPUT** (no
readouts supplied — missing is not zero; TTD dynamics are therefore not computed this epoch).

**Mission loci (b_{Q,t}):** Labour (deaf baristas) and Sourcing (fair-price floor,
tau^auth = 85 THB/kg with a pre-authorized state-contingent hardship clause:
tau = 75 THB/kg iff Liq_t < 100,000 THB).

**Binding evaluation (E-BIND, eq. 9), Appendix-B constitutive defaults:**

| Locus | Constitutive elements checked | q_j | Status |
|---|---|---|---|
| Labour | eligibility rule OK, employment record OK (deaf baristas on payroll); voice mechanism: NI | q_L = 1 on checked elements; assurance partially supported by the funded social audit | BINDING (qualified) |
| Sourcing | supplier rule OK (85 THB/kg floor, board-signed) — **traceability record FAIL (farm-purchase log not kept this year)** | **q_S = 0** | **NONBINDING** |

**Finding (failure code `NONBINDING`, Sourcing):** the mission is *declared* at the Sourcing
locus but a constitutive element (traceability record) fails, so q_S = 0. Operationally: this
year the enterprise **cannot demonstrate** that the 85 THB/kg floor was honored. This does not
mean the floor was violated (readout != reality — absence of record is absence of readout, not
evidence of breach), but every Sourcing-locus claim downstream (including the impact claim in
Q3) inherits this assurance hole, and Sourcing mission integrity I_S = **NI** (eq. 55–57: the
records cannot distinguish "conflict honored" from "conflict not detected"; NI, not 0 or 1).
Remediation: restore the purchase log (supplier, kg, price, date) as the constitutive record.

**Opportunity attribution (a2):** the founder states the CSR contract "came to us because of
our social mission". Under Rule 6 of the skill, a founder statement alone is not an adequate
support bundle for mission attribution of an opportunity — no client statement, no
counterfactual, nothing in the contract. The claim "a2 in Omega^M" is
**UNIDENTIFIED_COUNTERFACTUAL**: a2's membership is set-identified between {a2 in Omega^M}
and {a2 in F0}. Both branches are computed below; as it happens, the headline quantities are
**robust to the branch** (see Q1), so they come out point-identified anyway.

---

## Q1 — Benchmarks, O_M, and C_M

### Feasible sets

- Branch A (founder claim true, a2 in Omega^M): F0 = {a0, a1, a3}; F~ = F0 ∪ Omega^M = {a0, a1, a2, a3}.
- Branch B (a2 is an ordinary commercial opportunity, a2 in F0): F0 = F~ = {a0, a1, a2, a3}.
- F^SE (mission-admissible, both branches) = {a1, a2, a3} — a0 violates both hard constraints
  (Labour and Sourcing) and is excluded. F^SE nonempty => viability gate nu_t = 1, **not INFEASIBLE**.

### Four benchmarks (eq. 18–21; V in THB; J = V + Psi)

| Benchmark | Definition | Branch A | Branch B | V | Notes |
|---|---|---|---|---|---|
| x0 (mission-relaxed) | argmax_{F0} V | **a0** | **a0** | 180,000 | model counterfactual — never actually taken; never relabel as observed |
| xOmega (opportunity-expanded) | argmax_{F~} V | **a0** (180,000 > 170,000) | **a0** | 180,000 | a2 does not overtake a0 on V |
| xG (constraint-restricted) | argmax_{F^SE} V | **a2** | **a2** | 170,000 | |
| xSE (mission optimum) | argmax_{F^SE} V + Psi | **a2** (J = 200,000 > 180,000 [a1] = 180,000 [a3]) | **a2** | 170,000 | J: a1 = 180k; a2 = 200k; a3 = 180k |

(Arg max singleton in every cell, both branches.)

### Economic identity (eq. 22–26)

- **O_M = V(xOmega) − V(x0) = 180,000 − 180,000 = 0 THB.**
  Point-identified **despite** the unresolved a2 attribution, because a0's V (180,000)
  dominates a2's V (170,000) in both branches — the mission-created-opportunity question never
  reaches the V-maximum. If a2's V had exceeded 180,000, O_M would instead have been
  set-identified {0, V(a2) − 180,000} pending real attribution evidence.
- **C_G = V(xOmega) − V(xG) = 180,000 − 170,000 = 10,000 THB** — hard-constraint sacrifice
  (what excluding a0 costs in private economic value).
- **C_Psi = V(xG) − V(xSE) = 170,000 − 170,000 = 0 THB** — the mission objective re-ranks onto
  the same action the constrained V-max picks (a2), so no additional objective-driven sacrifice.
- **C_M = C_G + C_Psi = 10,000 THB.**
- Identity check (eq. 26): V(xSE) − V(x0) = 170,000 − 180,000 = −10,000 = O_M − C_M = 0 − 10,000. Verified.

**Interpretation:** this quarter the mission generated no measurable opportunity premium at
the optimum (O_M = 0 — and the only candidate for a positive O_M, the founder's claim about
a2, is unsupported anyway) and imposes a mission-attributable counterfactual sacrifice of
10,000 THB, all from the hard constraints (refusing commodity beans + replacing the baristas),
none from the mission objective's re-ranking.

**Do not double count:** C_M (10,000) is a counterfactual quantity, NOT a cash outflow. The
cash mission spend is C^bind = 15,000 THB (training + audit), which sits in the ledger, not in
C_M (eq. 35–36):

Ledger (eq. 36, before the chosen action's own cash effect):
`Liq_{t+1} = 250,000 + 60,000 (CF^op) − 15,000 (C^bind) − 10,000 (DS) = 285,000 THB` — nowhere
near the 100,000 THB hardship trigger (relevant to Q2).

### QuantityResults

```
{ name: "O_M", value: 0, unit: "THB/quarter", equation_id: "E-ECON eq.22",
  time_index: "point (this quarter)", identification: "point",
  assumptions: ["declared V,Psi accepted as readouts", "action set complete",
                "a2 mission-attribution unresolved but non-load-bearing (a0 V-dominates both branches)"],
  support_bundles: [["candidate-action table"]],
  defeated_sources: ["founder statement on a2 origin (inadequate for attribution; here moot)"],
  tier: "model",
  notes: "Robust to the UNIDENTIFIED_COUNTERFACTUAL on a2 membership." }

{ name: "C_G", value: 10000, unit: "THB/quarter", equation_id: "E-ECON eq.23",
  identification: "point", tier: "model",
  notes: "Counterfactual sacrifice from excluding a0; x0 and xOmega are model constructs, never observed." }

{ name: "C_Psi", value: 0, unit: "THB/quarter", equation_id: "E-ECON eq.24",
  identification: "point", tier: "model", notes: "xG = xSE = a2." }

{ name: "C_M", value: 10000, unit: "THB/quarter", equation_id: "E-ECON eq.25",
  identification: "point", tier: "model",
  notes: "Distinct from C^bind = 15,000 THB cash (training+audit); never add the two into one 'mission cost' line." }
```

Caveat carried on all four: the V and Psi figures are unaudited internal readouts
(selection/mapping/self-report noise uncharacterized); results are conditional on accepting them.

---

## Q2 — Is dropping the floor to 75 THB/kg mission drift? **YES.**

E-DRIFT (eq. 58–59): the pre-authorized state-contingent rule is
`tau^auth_S(S_t) = 75 THB/kg iff Liq_t < 100,000 THB, else 85 THB/kg`.

- Observed state: Liq_t = 250,000 THB (ledger projects ~285,000 next period).
  250,000 >= 100,000 => hardship condition NOT met => tau^auth(S_t) = **85 THB/kg**.
- Proposed: tau^obs = 75 < 85 = tau^auth(S_t) => **Drift = 1**.

This is exactly the distinction MOCA is built to make: *invoking a declared hardship rule when
its trigger holds is NOT drift* — if liquidity actually fell below 100,000 THB, a 75 THB/kg
floor would be the pre-authorized rule operating as designed. But invoking it at Liq = 250,000
"to save cash" is an unauthorized threshold reduction — mission drift, and if enacted without
board re-authorization and disclosure it would additionally be a **SILENT_LIFT**. It is also
not an INFEASIBLE situation that could excuse relaxation: F^SE is non-empty and contains a
positive-cash action (a2, V = 170,000), so there is no viability pressure to point to.

Aggravating context: with q_Sourcing = 0 (no traceability record), a quiet drop of the floor
would likely be **undetectable in the records** — a gate that cannot fail is a non-readout
(Goodhart warning, Rule 7). Restoring the purchase log is therefore also the drift *detection*
mechanism, not just paperwork.

Legitimate path if the manager wants a lower floor: take it to the board as an explicit
amendment of tau^auth (a governance change, disclosed and recorded) — a mission-redefinition
decision, not an operational cash measure the manager can execute alone.

```
{ name: "Drift(Sourcing floor 75 proposal)", value: 1, unit: null,
  equation_id: "E-DRIFT eq.59", identification: "point", tier: "model",
  support_bundles: [["board hardship rule (Jan)", "liquidity readout 250,000", "manager proposal"]],
  notes: "tau_obs 75 < tau_auth(S_t) 85; hardship trigger (Liq<100k) not met at Liq=250k." }
```

---

## Q3 — Is "we increased farmer income by 20%" publishable? **NO — status NI; do not publish as stated.**

Audit per Algorithm 3 / E-READOUTAUDIT:

1. **Support bundle adequacy:** this is a *change* claim (delta income = +20%) plus a *causal
   attribution* claim (increased *by us*). A minimal sufficient support bundle needs at least
   (a) a baseline income readout, (b) a current income readout, (c) a licensed attribution
   path from the enterprise's purchasing to the change. Available evidence: one interview with
   one farmer, **no baseline income records**. Element (a) does not exist => the family of
   minimal sufficient support bundles is **empty** => Algorithm 3 returns **NI("no adequate
   support bundle")**. The identified set for the income change is unbounded, not "20% +/- x".
2. **Readout typing (eq. 1):** a single self-reported interview is one channel with
   uncharacterized selection noise (why this farmer?), mapping noise (income recall), and
   self-report noise (interviewee speaking to their own buyer). n = 1, eta^self uncontrolled.
3. **Compounding failure:** the Sourcing locus is NONBINDING this year (no purchase log), so
   the enterprise cannot even document *how much it bought, from whom, at what price* — the
   mechanism the income claim rides on fails provenance Existence (E in RC(d) = E∧A∧D).
4. **Missing is not zero — in both directions:** this verdict does NOT say farmer income did
   not rise, and must not be reported as "no impact". Honest status: **NI**.

**Publishable alternative (qualified, readout-faithful):** "One partner farmer reported in an
interview that their income has improved since selling to us; we do not yet have baseline
income records to quantify this." Plus a forward fix serving E-FALSIFY discipline: collect
baseline income and purchase-log data now, **freeze** a prediction rule (e.g. "partner
farmers' median coffee income next crop year >= X") *before* outcome retrieval, so next year's
report carries a testable, non-leaked claim instead of a retrospective anecdote.

```
{ name: "farmer income change attributable to enterprise", value: "NI", unit: "% change",
  equation_id: "E-READOUTAUDIT eq.66-70", identification: "NI",
  assumptions: [], support_bundles: [],
  defeated_sources: ["single farmer interview (n=1, self-report, no baseline)"],
  tier: "NI/Open",
  notes: "Failure codes: NI_INPUT (no baseline), UNIDENTIFIED_COUNTERFACTUAL (no comparison).
          Sourcing NONBINDING status independently breaks the attribution chain." }
```

---

## Summary of failure codes raised this epoch

| Code | Where |
|---|---|
| `NONBINDING` | Sourcing locus (traceability record missing; q_S = 0) |
| `UNIDENTIFIED_COUNTERFACTUAL` | a2 mission-attribution (founder statement only; non-load-bearing for O_M this quarter) |
| `NI_INPUT` | trust/hazard state variables; farmer baseline income |
| Drift = 1 | proposed 75 THB/kg floor at Liq = 250,000 (would be `SILENT_LIFT` if enacted undisclosed) |
| I_Sourcing = NI | integrity denominator unidentifiable without purchase records |

Recommended immediate actions: (1) reinstate the farm-purchase log (restores q_S, drift
detectability, and the impact claim's provenance base); (2) reject the floor-drop proposal or
route it to the board as an explicit tau^auth amendment; (3) rewrite the impact-report
sentence to the qualified form and start baseline data collection with a frozen prediction
for next year.
