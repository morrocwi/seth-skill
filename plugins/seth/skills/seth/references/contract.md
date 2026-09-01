# MOCA AI calculation contract, failure codes, and algorithms

## QuantityResult — required output object (§10.1)

Every computed quantity is emitted as:

```
QuantityResult = {
  name: string,
  value: number | interval | set | "NI",
  unit: string | null,
  equation_id: string,                     # stable E-* id from equations.md
  time_index: "point" | [start, end],
  identification: "point" | "set" | "NI",
  assumptions: [id...],
  support_bundles: [[source_id...], ...],  # minimal jointly sufficient sets
  defeated_sources: [source_id...],
  tier: "model" | "standard-math" | "finite-diagnostic" | "NI/Open",
  notes: string
}
```

A bare number without this metadata is not a complete MOCA result.

## Table 1 — minimum input contract (rule if missing/ambiguous)

| Block | Required fields | Rule if missing or ambiguous |
|---|---|---|
| Time | t, T, δ (integer horizon, discount) | Ask for horizon or run declared scenarios; never infer a calendar unit silently |
| State | financial, capacity, trust, hazard, regime (Eq. 3) | Missing state is NI; scenario bounds only if declared |
| Topology | nodes, edges, governance rights | Do NOT collapse a multi-entity system into one firm if control/resource edges are load-bearing |
| Mission | loci b, constraints G_j, thresholds τ^auth, objective Ψ^M | Statements without a computable rule are declaration-only; binding may remain 0 / NI |
| Actions | candidate actions or continuous decision variables (records with V, mission score, cash effects) | No action set ⇒ no optimization claim allowed |
| Opportunity | Ω^exo, Ω^endo | Mission attribution is NI unless a support path from mission architecture to opportunity is declared |
| Binding | W_j, constitutive subset R*_j, assurance a_j | Missing constitutive requirement sets q_j = 0; missing assurance makes β̂_j NI |
| Evidence | readouts, provenance DAG, support bundles (+ source IDs, date/version) | Failing E, A, or D downgrades the claim to NI / Open / qualified |
| Uncertainty | scenarios, probabilities, or uncertainty set | Never use chance and robust constraints simultaneously unless explicitly specified |
| Policy support | instruments u_t, incentive rule, incidence matrix | Treat support as resource + incentive + institutional change, not cash only |

## Failure codes (§15 — use these exact states)

- `NI_INPUT` — required value not observed and no declared bound exists
- `INFEASIBLE` — F^SE = ∅ (report U_min + provenance; diagnosis = infeasibility, not drift)
- `NONBINDING` — mission declared but constitutive binding requirements fail
- `UNIDENTIFIED_COUNTERFACTUAL` — x⁰, x^Ω, or attribution is not identified
- `ZERO_CONFLICT_READOUT` — integrity denominator has no identifiable conflicts
- `SILENT_LIFT` — a claim depends on undeclared augmentation
- `SUPPORT_DEFEATED` — all minimal sufficient support bundles are undercut
- `LEAKED_PREDICTION` — outcome information entered before prediction freeze
- `PORTABILITY_NI` — ecosystem transfer cannot be evaluated from available evidence

Two absolute rules: **missing is not zero**, and **a model-generated counterfactual is never
relabeled as an observed fact**.

## Algorithm 1 — one-period diagnostic

```
function MOCA_DIAGNOSE(data, question_Q):
  validate_schema(data)
  R <- collect_readouts(data.evidence);  build_provenance_DAG(R)
  X <- assemble_state(data.state)
  O <- assemble_topology(data.organizations, data.edges, data.control_rights)
  b <- locate_mission_loci(data.mission, question_Q)
  for each locus j in active(b):
    W[j] <- evaluate_binding_components(j)
    q[j] <- product(W[j][r] for r in constitutive[j])
    beta_hat[j] <- q[j] * assurance[j]   # if assurance unknown -> NI
  Omega_exo  <- declared_external_opportunities()
  Omega_endo <- solve_or_bound_fixed_point(G_omega, b, W, X, Z, O)
  F_tilde <- union(F0, Omega_exo, Omega_endo)
  F_SE    <- {x in F_tilde : all mission constraints pass}
  if F_SE is empty:
    U_min <- solve_min_support_for_nonempty(F_SE)
    return INFEASIBLE with U_min and provenance
  x0 <- argmax_set(F0, V); xOmega <- argmax_set(F_tilde, V)
  xG <- argmax_set(F_SE, V); xSE <- argmax_set(F_SE, V + Psi_M)
  O_M <- V(xOmega)-V(x0); C_G <- V(xOmega)-V(xG); C_Psi <- V(xG)-V(xSE); C_M <- C_G+C_Psi
  phi <- shapley_attribution(coalitions) if coalition values available else NI
  integrity <- compute_integrity_only_if(conflicts_identified)
  readout_audit <- EAD_and_identification_audit(all_claims)
  return structured_results(X, O, b, W, F_SE, x0, xOmega, xG, xSE,
                            O_M, C_G, C_Psi, C_M, phi, integrity, readout_audit)
```

## Algorithm 2 — dynamic management simulation

```
function MOCA_SIMULATE(initial_state, policy_pi, horizon_T):
  S <- initial_state; path <- []
  for t in 0..T-1:
    if S not in viability_region: return FAILURE(path, cause="viability exit")
    actions <- feasible_actions(S)
    x <- policy_pi(S, actions);  verify_mission_constraints(x, S)
    cash <- cash_ledger_update(S, x)
    trust_hazard <- TTD_update_with_lag(S, x)
    Q_M <- obligation_stock_update(S, Q_M, x)
    Z_next <- ecosystem_update(S, Z, x, policy_support)
    S_next <- transition(S, x, cash, trust_hazard, Q_M, Z_next)
    path.append(audit_record(t, S, x, S_next));  S <- S_next
  return PATH_RESULT(path, survival=true,
                     discounted_value=Bellman_sum(path),
                     integrity=path_integrity(path),
                     provenance=path_provenance(path))
```

## Algorithm 3 — readout and claim audit

```
function AUDIT_CLAIM(claim_d, evidence_graph, assumptions):
  Gamma <- construct_identified_alternatives(evidence_graph, assumptions)
  I_q   <- evaluate_quantity_over(Gamma)
  support_family <- minimal_jointly_sufficient_supports(claim_d)
  if support_family is empty:               return NI("no adequate support bundle")
  if represented_basis_contains_no_bundle(): return FAIL_ATTRIBUTION
  if material_augmentation_not_disclosed():  return SILENT_LIFT
  if cardinality(I_q) == 1: return POINT_IDENTIFIED(only_element(I_q))
  else:                     return SET_IDENTIFIED(I_q)
```

## Algorithm 4 — prediction-falsification protocol

```
function SCORE_PREDICTION(prediction, outcome_evidence):
  if prediction.leak == 1: return EXCLUDED("leakage before freeze")
  S_out <- adequate_outcome_supports(outcome_evidence)
  if S_out is empty: return NI("outcome not identified")
  Y_out <- identified_outcome_set(outcome_evidence)
  if intersection(prediction.Y_hat, Y_out) is empty: return REFUTED
  else: return NOT_REFUTED
```

## Appendix B — default mission-locus binding requirements (starting points, not natural laws)

| Locus | Candidate constitutive requirements |
|---|---|
| Allocation | rule, accounting record, distribution restriction, audit |
| Labour | eligibility rule, employment record, worker rights, voice/complaint mechanism |
| Sourcing | supplier rule, traceability record, supplier rights/voice where mission-relevant, audit |
| Product | price/quality/access threshold, beneficiary definition, transaction record |
| Payment | financing rule, fee/interest ceiling, receivables record, affordability test |
| Transaction | non-completion objective, protected-party rights, separate condition record, conflicts disclosure, audit, admissible capital |
| Data | collection/use rule, consent/rights, access log, audit, model documentation |
| Capital | control-right lock, return/horizon rule, transfer/exit restriction, disclosure |
| Lifecycle | service/take-back/warranty rule, obligation record, funding reserve, completion audit |

## Development-stage evidence status (§16 — quote honestly)

45-enterprise retrospective harness forced major architecture additions; a later 40-case
battery (Grameen Shakti, KickStart, Revolution Foods, d.light, M-KOPA, TOMS,
The Big Issue, BRAC/Aarong Dairy, Grameen Bank, …), coded under a frozen v5 architecture but
— per the paper itself — **not disjoint from the earlier development cases** (not held-out),
coded 30 PASS / 8 PRESSURE / 2 BOUNDARY / 0 direct structural FAIL. **These counts are
finite-diagnostic — structural pressure testing,
not accuracy estimates, not population validation, not a ranking of those organizations.**
A quasi-blind pilot froze directional prediction rules before outcome retrieval; among
adjudicable predictions no observed disconfirmation, several outcomes NI — methodological
demonstration only. Future validation needs preregistered coding rules, held-out enterprises,
independent coders, declared failure conditions.
