# Benchmark test-case prompts and assertions (verbatim)

These are the exact prompts given to both configurations (the with-skill run was additionally
instructed to read and follow the skill first), and the assertions each output was graded
against. Both cases are synthetic; all figures are illustrative.

---

## Case 1 — Coffee shop (feasible; attribution + drift + impact-claim traps)

### Prompt

> "Baan Kafae Jaidee" is a social-enterprise coffee shop in Pattani. Its declared mission:
> (1) employ hearing-impaired baristas (Labour), (2) buy beans from smallholder farmers in
> Chiang Rai at a fair-price floor of at least 85 THB/kg (Sourcing), with a pre-authorized
> hardship rule signed by the board in January: "the floor may drop to 75 THB/kg in any month
> where liquidity < 100,000 THB".
>
> Quarterly data:
> - Candidate actions (private economic value V in THB, mission score Ψ):
>   - a0: switch to commodity beans (~70 THB/kg) + replace deaf baristas with regular staff.
>     V=180,000, Ψ=0. Violates both mission constraints.
>   - a1: status quo (fair-price beans, deaf baristas). V=120,000, Ψ=60,000.
>   - a2: corporate CSR catering contract. V=170,000, Ψ=30,000. Passes constraints. The founder
>     says this contract "came to us because of our social mission", but there is no other
>     evidence (no statement from the client, no counterfactual, nothing in the contract).
>   - a3: expand barista training program. V=100,000, Ψ=80,000. Passes constraints.
> - Current liquidity: 250,000 THB. Operating cash flow this quarter: 60,000. Sign-language
>   training + social audit expenditure: 15,000. Debt service: 10,000.
> - The Sourcing locus has NO traceability record this year (the farm-purchase log was not kept).
> - Impact report draft claims: "we increased farmer income by 20%" — evidence: one interview
>   with one farmer; no baseline income records exist.
>
> Questions:
> 1. What is the mission opportunity value O_M and the total mission-attributable cost C_M this
>    quarter? Show the four benchmarks.
> 2. The manager proposes dropping the fair-price floor to 75 THB/kg now to save cash. Is that
>    mission drift?
> 3. Is the "farmer income +20%" claim supported enough to publish in the impact report?

### Assertions graded

1. O_M is not laundered from founder-only attribution into a settled point value. (Note: as
   originally drafted this assertion expected "set-identified or NI"; the correct MOCA answer
   turns out to be a robust point value O_M = 0 because a0 V-dominates both attribution
   branches — the with-skill run's answer was correct and the assertion wording was the error.)
2. The drift verdict cites the pre-authorized state-contingent rule; invoking the rule when its
   trigger holds is recognized as NOT drift.
3. The "+20% farmer income" claim is returned NI / unsupported, never repeated as fact.
4. The Sourcing-locus binding failure (missing traceability record ⇒ q_j = 0 / NONBINDING or
   NI) is flagged, not silently treated as bound.
5. Binding cash expenditure C^bind (15,000) is kept separate from counterfactual mission cost
   C_M, with no double counting.
6. Missing values are treated as NI, never as zero.

---

## Case 2 — Bakery (infeasible; topology + obligation + leakage traps)

### Prompt

> "Roti Baan Rao" is a social-enterprise bakery in Yala, structured as TWO legal entities:
> - **Baan Rao Foundation** (holds the brand and the mission covenant; governed by a board;
>   holds a 40,000 THB grant from an international funder, restricted by the grant letter to
>   "youth training program expenses only")
> - **Baan Rao Bakery Ltd.** (operates the shops; licensed to use the brand by the Foundation,
>   conditional on honoring the mission covenant)
>
> Mission covenant (hard constraints on the Ltd.):
> 1. (Labour) at least 60% of bakery staff are ex-offender youth in the reintegration program.
> 2. (Product) subsidized bread price ≤ 15 THB/loaf for registered low-income families.
>
> Situation this quarter: flour costs spiked. The Ltd.'s liquidity is 30,000 THB, and its bank
> covenant requires liquidity ≥ 25,000 at quarter end. Last year the Ltd. pre-sold 12-month
> "bread subscriptions" to 200 low-income families (monthly delivery); 7 months of deliveries
> are still outstanding.
>
> Candidate actions for the Ltd. (V = private economic value effect, Ψ = mission score; cash
> effect on liquidity in parentheses):
> - a0: drop the subsidized bread line entirely and hire experienced adult bakers. V = 90,000,
>   Ψ = 0 (cash +40,000). Violates both covenant constraints, and would stop the remaining
>   7 months of prepaid subscription deliveries.
> - a1: status quo. V = −40,000 (a loss at current flour prices), Ψ = 50,000 (cash −20,000 →
>   quarter-end liquidity 10,000).
> - a2: raise the subsidized price to 22 THB/loaf. V = −5,000, Ψ = 30,000 (cash +2,000).
>   Violates constraint 2 (≤15 THB).
> - a3: cut the ex-offender staff share to 40%. V = 10,000, Ψ = 20,000 (cash +5,000). Violates
>   constraint 1 (≥60%).
>
> The Ltd.'s manager proposes two things:
> (A) "Transfer the Foundation's 40,000 grant into the Ltd.'s account to cover the shortfall —
>     we're one organization anyway."
> (B) For the annual report: "Our prediction that 70% of program youth would complete the year
>     was confirmed." (The manager wrote this 'prediction' last week, after already receiving
>     this cohort's completion list.)
>
> Questions:
> 1. What should the Ltd. do this quarter according to the framework? Show your reasoning about
>    the feasible set.
> 2. Is proposal (A) acceptable?
> 3. Can claim (B) be used in the annual report as a validated prediction?

(The without-skill arm received the identical prompt with "according to the framework" softened
to "according to sound social-enterprise management".)

### Assertions graded

1. Returns INFEASIBLE (F^SE empty): diagnosis is mission infeasibility under the current state
   — NOT mission drift — and no constraint-violating action is quietly recommended.
2. The minimum viability support U_min = 15,000 THB (bringing a1 to the 25,000 covenant floor)
   is computed, and the decision is routed to governance/funder.
3. The two entities are not collapsed: the restricted 40k grant is not simply added to the
   Ltd.'s liquidity; use requires the governance edge (board + grant terms), else NI/conditional.
4. The prepaid-subscription obligation stock is flagged: a0 defaults on outstanding
   obligations — "profitable now while destroying future viability" is surfaced.
5. The "70% completion" prediction is flagged as leaked (written AFTER outcomes were seen) ⇒
   excluded from scoring, not usable as validated evidence.
6. Missing values stay NI, never zero; no invented numbers.
