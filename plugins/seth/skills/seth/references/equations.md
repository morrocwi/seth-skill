# MOCA equation inventory (from Technical Preprint v0.2, Yaoharee Lahtee, Sep 2026)

Stable IDs (Table 2) are the durable reference, not printed equation numbers.
Tier legend: Th-coqc (generic structural, machine-checked in the Universal Solver repo) ·
standard-math · model (MOCA definitions conditional on declared inputs) · finite-diagnostic ·
NI/Open. The social-domain equations below are **model / standard-math tier — not Coq-certified**
(paper §18).

## E-READOUT — reality, readout, non-equivalence  (§2.1)

- (1) `R_{a,t} = K_a θ(E_t) + η^sel_{a,t} + η^map_{a,t} + η^self_{a,t}`
  (source/channel a; selection, mapping, self-report noise)
- (2) `R_{a,t} ≠ E_t` in general — the ONLY universal discipline used operationally.
  Accounting records, audit files, impact reports, interviews are typed as readouts.

## E-STATE — enterprise state  (§2.2)

- (3) `X_t = (Liq_t, AR_t, Inv_t, Debt_t, Cap^mgr_t, Cap^coord_t, T^op_t, T^sym_t, H_t, σ_t)`
  (liquidity, receivables, inventory, debt, managerial bandwidth, coordination capacity,
  operational trust, symbolic trust, hazard memory, regime)
- (4) `T^sym_t = (T^sym_customer, T^sym_worker, T^sym_supplier, T^sym_regulator, T^sym_funder,
  T^sym_investor, …)_t` — symbolic trust is stakeholder-specific.
- (5) `S_t = (X_t, Z_t, O_t, Ω^M_t, Q^M_t, W_t)` — complete management state
  (ecosystem, topology, mission-enabled opportunity set, mission-obligation stock, binding arch.)
- (6) `O_t = (N_t, E_t(edges), Γ_t)` — organizational topology graph: actors, resource/contract/
  control relations, governance rights. A mission rule may reside on a node OR an edge.

## Mission architecture  (§3)

- (7) `b_{Q,t} = (b_A, b_L, b_S, b_P, b_Pay, b_T, b_D, b_K, b_R, …)_t` — question-relative
  mission-binding vector over loci (Allocation, Labour, Sourcing, Product/Offering,
  Payment/Customer-Finance, Transaction, Data/Information, Capital/Governance,
  Process/Lifecycle). An audit coordinate, not an ontological claim.
- (8) `W_{j,t} = (Rule, Record, Rights, Voice, Control, Audit, Capital)_{j,t}` — binding
  architecture per locus.
- (9) E-BIND: `q_j = ∏_{r∈R*_j} b_{jr}`, `β̂_j = q_j a_j`, a_j ∈ [0,1] assurance/readout
  strength. Any constitutive element fails ⇒ q_j = 0. Unknown assurance ⇒ β̂_j = NI.
  Deliberately NOT a universal latent "binding score".
- (10) Master decomposition: `Mission = Opportunity Creation + Hard Constraint + Mission
  Objective` — representational, not an empirical claim that all three are nonzero.
- (11) E-OMEGA: `Ω^M_t = Ω^exo_t ∪ Ω^endo_t`
- (12) `Ω^endo_t = G(Ω^endo_t, b_t, W_t, X_t, Z_t, O_t)` — fixed point; multiple fixed points
  ⇒ Ω^endo and downstream economic values are SET-identified until an equilibrium-selection
  rule is independently justified.

## E-FEAS / E-ECON — static architecture  (§4)

- (13) `F̃_t = F⁰_t ∪ Ω^M_t` (mission-relaxed conventional feasible set ∪ mission opportunities)
- (14) hard constraint: `G_{j,t}(x, X_t, Z_t, O_t, H_t, ω_t) ≥ τ^auth_{j,t}`
- (15) `F^SE_t = {x ∈ F̃_t : G_{j,t}(x,…) ≥ τ^auth_{j,t} ∀j}`
- (16) viability gate `ν_t = 1[F^SE_t ≠ ∅]`; ν_t=0 ⇒ no optimum reported; diagnosis =
  mission INFEASIBILITY under current state, not drift.
- (17) mission decision objective `J_t(x) = V_t(x) + Ψ^M_t(x)`
- (18–21) four benchmarks (set-valued arg max intentional; existence/uniqueness are separate
  obligations):
  `x⁰ ∈ argmax_{x∈F⁰} V`, `x^Ω ∈ argmax_{x∈F̃} V`, `x^G ∈ argmax_{x∈F^SE} V`,
  `x^SE ∈ argmax_{x∈F^SE} [V + Ψ^M]`
- (22) `O_M = V(x^Ω) − V(x⁰) ≥ 0` (mission opportunity value)
- (23) `C_G = V(x^Ω) − V(x^G) ≥ 0` (hard-constraint sacrifice)
- (24) `C_Ψ = V(x^G) − V(x^SE) ≥ 0` (mission-objective sacrifice)
- (25) `C_M = C_G + C_Ψ` (total mission-attributable private economic sacrifice)
- (26) central identity: `V(x^SE) − V(x⁰) = O_M − C_G − C_Ψ = O_M − C_M`
  (separates mission-created opportunity from mission-imposed sacrifice; NOT social welfare)
- (27) `RF_{j,t} = Rev^counterfactual − Rev^observed` (direct revenue forgone — operational readout)
- (28) `RF_{j,t} ≠ C_{G,j,t}` in general (refusal may create reputation/lower risk/open doors)

## E-SHAPLEY — constraint interaction  (§4.5–4.6)

- (29) `C(S) = V^Ω − V^S` for constraint subset S ⊆ J active
- (30) pairwise interaction `Γ_jk = C({j,k}) − C({j}) − C({k})`
- (31) Shapley `φ_j = Σ_{S⊆J\{j}} |S|!(|J|−|S|−1)!/|J|! × [C(S∪{j}) − C(S)]`;
  Σφ_j = C(J) when fully specified. Attribution is model-relative.
- (32–34) KKT: `L = V + Σ λ_j[g_j(x) − τ_j]`, complementary slackness
  `λ_j[g_j(x*) − τ_j] = 0`, local marginal value `−∂V*/∂τ_j = λ_j` — a LOCAL shadow price,
  not to be confused with global interaction-aware Shapley attribution.

## E-CASH / E-TTD — cost, accounting, TTD plug-in  (§5)

- (35) `C_M ≠ C^bind` — counterfactual sacrifice vs. binding expenditure (certification,
  impact evaluation, complaints systems, protected-party rights, audit, governance covenants).
- (36) ledger: `Liq_{t+1} − Liq_t = CF^op + U^cash − C^bind − I^MC − DS − ΔWC − Loss_t`
  (I^MC = mission-enabled market/capability-creation investment; DS debt service; ΔWC working
  capital). Counterfactual sacrifice C_M is NOT subtracted from cash flow (avoid double count).
- (37) audit residual `R^cash_T = (Liq_T − Liq_0) − Σ_{t<T}(Liq_{t+1} − Liq_t)` must be 0
  for an internally closed discrete ledger.
- (38) TTD scalar revenue: `Rev_t = r_0[0.6 + 0.8 tanh(T^op_t)] × (1 + βT^sym_t)(1 + σ_r ε_t)`
- (39) `G_t = max(0, T^sym_t − κ T^op_t)` (trust gap)
- (40) `p^haz_t = clip[h_0(1 + h_m H_t)e^{−h_p T^op} + φG_t, 0, 0.95]`
- (41) `Ovh_t = max(Ovh^floor, Ovh_0[1 − α_eff T^op_t]) + γ max(0, Liq_t − Liq^scale)`
- (42–43) decay `T^op_{t+1} = T^op_t(1−δ_op)`, `T^sym_{t+1} = T^sym_t(1−δ_sym)`
- (44) cash update `Liq_{t+1} = Liq_t + Rev_t − Ovh_t − hit_t + ΔLiq(a_t)`; action cash
  effects immediate, trust/hazard effects arrive after lag ℓ.
- (45) hard survival: `Liq_t ≥ Liq^min, T^op_t ≥ T^op_min, H_t ≤ H^max`
- (46) stakeholder expectation gap `G_{a,t} = max(0, T^sym_{a,t} − κ_a T^op_{a,t})`.
  Any projection of the trust vector to a scalar must declare weights (a model augmentation,
  not a direct readout).

## E-OBLIG / E-DYN — dynamics  (§6)

- (47) obligation stock `Q^M_{t+1} = (1−δ_Q)Q^M_t + q^M(x_t) − Fulfilled_t` — a firm can be
  profitable at t while accumulating mission obligations that destroy future viability.
- (48) ecosystem feedback `Z_{t+1} = 𝓩(Z_t, O_t, u_t, ε_t)` — not purely exogenous.
- (49) transition `S_{t+1} = 𝓣(S_t, x_t, u_t, Q^M_t, ε_t)`
- (50–51) dynamic viability `S_t ∈ 𝓥 ∀t ≤ T`; `P_surv(T) = P(S_t ∈ 𝓥 ∀t ≤ T)`
- (52) Bellman: `W^SE(S_t) = sup_{π∈Π^SE} E[Σ_{k=t}^T δ^{k−t}(V_k + Ψ^M_k + Ψ^u_k − C^bind_k
  − I^MC_k)]` — a disciplined representation of declared ranking and constraints, NOT a claim
  managers possess a true utility function. Ψ^u records policy-instrument incentive effects.
- (53) chance constraint `P[G_{j,t} ≥ 0 | 𝓘_t] ≥ 1 − α_j`; (54) robust `inf_{ω∈𝓤} G ≥ 0`.
  Tolerance α_j and uncertainty set 𝓤 are policy/model choices ⇒ belong in provenance.
  Never use chance and robust constraints simultaneously unless explicitly specified.

## E-INTEGRITY / E-DRIFT / E-INCIDENCE — governance  (§7)

- (55–57) `χ_{j,k} = 1[identifiable conflict]`, `h_{j,k} = 1[mission honored]`;
  `I_j = Σ χh / Σ χ` ONLY if ID(χ)=1. Denominator zero, or records cannot distinguish
  "no conflict" from "conflict not detected" ⇒ I_j = NI (not 0 or 1). A gate that never
  fails may be a non-readout.
- (58–59) `τ^auth_{j,t} = τ_j(S_t; γ_j)` pre-authorized state-contingent rule;
  `Drift = 1[τ^obs < τ^auth(S_t)] χ` — invoking a declared hardship rule ≠ drift.
- (60) stakeholder ledger `ΔV_{g,t} = O_{G,t} − C_{G,g,t} − C_{Ψ,g,t} − C^bind_{g,t} + U_{g,t}`
- (61–62) social outcome vector `Y^soc_t`; any aggregation `W^soc = Σ ω_g Y_g` must DISCLOSE
  normative weights ω_g. Mission integrity / social outcome / social welfare are distinct objects.
- (63–65) minimum support `U^min_t = inf{U ≥ 0 : F^SE(U) ≠ ∅}` (static),
  `U^min_{0:T}` (dynamic); portability `Port(M; Z_A→Z_B) = P[ν_B = 1 ∧ I_B ≥ I_min]`.

## E-READOUTAUDIT — readout-bounded inference  (§8)

- (66–67) identified set `𝓘_q(r; A_k) = {q(e′) : e′ ∈ Γ_k(r)}`; point identification iff
  |𝓘_q| = 1; else output set/interval/scenario family/NI (Manski partial identification).
- (68–69) minimal sufficient support bundles 𝓢(d; y, κ) — antichain of minimal jointly
  sufficient support sets under declared audit context; a represented basis B is
  attribution-adequate only if ∃S ∈ 𝓢 with S ⊆ B.
- (70) Readout Condition `RC(d) = E(d) ∧ A(d) ∧ D(d)` (provenance Existence, licensed
  Attribution, Disclosure/recoverability of material augmentation).
- (71–72) defeat: surviving supports `𝓢_Δ(d) = {S : S∩Δ = ∅}`; vulnerability
  `v_d(Δ) = 1[𝓢_Δ ≠ ∅]`. All adequate bundles defeated ⇒ downgrade or retract.
- (73–74) Goodhart: `R_t = R(M*_t, a^game_t, η_t)`; `R_t ↑ ⇏ M*_t ↑`.

## E-FALSIFY — prediction provenance  (§9)

- (75) `Pred(d) = (ŷ_d, 𝓢_pre(d), t_freeze, Leak_d)` — freeze prediction rules BEFORE
  outcome retrieval; retrospective case fit is weak evidence.
- (76) `Testable(d) = 1[Leak_d = 0] · 1[𝓢_out(d) ≠ ∅]`
- (77–78) `Hit = Testable · 1[Ŷ_d ∩ Y^out_d ≠ ∅]`; `Refute = Testable · 1[∩ = ∅]`.
  An outcome with inadequate support is NI, not a win.

## Collapse consistency  (§17)

- (84) `Ω^M → ∅, G_j → always true, Ψ^M → 0, C^bind → 0` ⇒
- (85) `F^SE → F⁰, x^SE → x⁰, O_M, C_G, C_Ψ → 0` — MOCA must reduce to ordinary economic
  optimization when mission-specific architecture disappears.

Falsifiable at multiple levels: inter-rater reliability of mission-locus coding; binding
architecture failing to predict behavior under identifiable conflict; opportunity attribution
inseparable from generic market growth; dynamic viability adding nothing over ordinary
financial ratios; portability adding no information; readout layer never changing a verdict;
held-out predictions systematically refuted.

## Worked numerical example  (§13, synthetic, illustrative only)

Actions: a0 premium market (V=120, Ψ=0, fails constraints), a1 low-income direct (95, 40,
pass), a2 institutional contract (132, 25, pass — exists via mission credibility),
a3 supplier-upgrading (110, 50, pass). F⁰={a0,a1,a3}.
x⁰=a0, x^Ω=a2, x^G=a2, x^SE=a3 ⇒ O_M = 132−120 = 12; C_G = 0; C_Ψ = 132−110 = 22;
ΔV^SE = 12−0−22 = −10 = V(a3)−V(a0), verifying (26).
Ledger: Liq 300 +110 op CF +20 support −8 C^bind −12 I^MC −5 DS −15 ΔWC = 390; C_M=22 NOT
subtracted again. **If the claim "a2 exists because of mission" rests only on a founder
statement (no contract/counterfactual/independent buyer evidence), O_M must be returned as
set-identified or NI even though the arithmetic is internally correct.**
