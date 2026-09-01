# Changelog

## v0.2.0 — 2026-09-02

- **Advisory mode**: the skill now answers everyday social-enterprise questions
  (starting, structuring, pricing, funding, staffing, governing an SE; mission-vs-profit
  tensions) in plain-language advisory mode — MOCA as the silent lens, no input contract
  demanded, one or two targeted questions at most — and escalates to the full typed
  diagnostic when numbers are supplied with a request to calculate, or on an explicit
  "run the framework"; a high-stakes question with no data stays advisory with an offer
  to upgrade. The register adapts to the asker: everyday words for a
  first-time founder, technical vocabulary for an accountant/funder/researcher, replies in
  the user's own language, with precision preserved under simplification. Trigger
  description updated accordingly.

- **Thai SE law library** (`references/thai-se-law/`): 40 primary-source PDFs — the
  พ.ร.บ.ส่งเสริมวิสาหกิจเพื่อสังคม พ.ศ. 2562 and 39 subordinate instruments (2562–2567) —
  with a machine-readable knowledge graph (`kg.json`: verified titles, issuing bodies,
  Gazette citations, legal-basis edges, audience groups, Thai lookup keywords), a human
  catalog (`INDEX.md`), a relationship map (`KG.md`), and per-document verification notes
  (`catalog-raw.md`). Every field was read from the documents themselves. The skill now
  requires legal answers to cite the specific instrument + date and to carry a currency
  warning: verify against the latest version at ราชกิจจานุเบกษา / สวส. (OSEP) in parallel
  before acting.

## v0.1.0 — 2026-09-02

Initial public release.

- `seth` skill (SKILL.md + `references/equations.md` + `references/contract.md`) distilled from
  the MOCA Technical Preprint v0.2 (September 2026).
- MOCA paper PDF included under `paper/` (CC BY 4.0).
- Two worked example diagnostics (`examples/`) produced by an agent running the skill.
- Finite-diagnostic benchmark notes (`benchmarks/`, n = 2 cases, honest limitations stated).
- Claude Code plugin marketplace packaging (`.claude-plugin/`, `plugins/seth/`).
