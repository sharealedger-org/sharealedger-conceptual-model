# Ledger Lab — Active Task List

Items are tracked here by priority. Move completed items to `log.md` when done.

---

## HIGH — Project scoping (do first)

- [ ] **Define minimum viable first milestone** — what does ledger-lab implement
  first? Which framework concepts does the first milestone target?

- [ ] **Synthetic dataset** — what dataset drives the initial conformance fixtures?
  The purchase/settlement example from the framework is the candidate first fixture.
  Ledger Lab owns execution; this repo owns the fixture definitions.

- [ ] **Acceptance criteria** — what tests must pass for the first milestone to be
  declared complete?

- [ ] **Environment** — who operates the implementation environment? What platform?

## MEDIUM

- [ ] **Conformance fixture data files** — plain JSON/CSV files representing parties,
  agreements, instruments, events, reference data, rules, and expected outputs.
  This repo defines the fixtures; ledger-lab implements against them.

- [ ] **Decision records for open framework questions** — the framework
  (`framework/open-accounting-framework.md`) names several unresolved questions.
  Each should become a scoped item here or in the framework layer:
  - Event / Movement / Position as separate record types vs. common lineage model
  - Global vs. scoped identifiers
  - Commitment reciprocity
  - Amount / quantity / unit / currency / uncertainty representation
  - Late-arriving and corrected events
  - Rules declaring dependencies and producing auditable generated events
  - Minimum conformance suite definition
