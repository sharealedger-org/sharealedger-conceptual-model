# Hospice App — Active Task List

Items are tracked here by priority. Move completed items to `log.md` when done.

---

## HIGH — Required before prototype can be built

- [ ] **FHIR mapping** (`fhir-mapping.md`) — current status is stub. Needs:
  1. Validation of each mapping row against FHIR R4/R5 specs
  2. FHIR profiles or extensions for the six gap event types
  3. Shared/private partition representation in FHIR consent/access control
  4. Three structural gap handling specifications
  5. Test against a reference FHIR server (HAPI FHIR) with synthetic hospice data
  6. Publication as a Sharealedger FHIR Implementation Guide

- [ ] **IBM Cloud prototype plan** — `shared-storage-infrastructure.md` names IBM Cloud
  as the prototype target and lists the six-component stack, but no implementation
  plan exists. Define: which component first, what synthetic dataset, what acceptance
  test, who operates the IBM Cloud account.

## MEDIUM

- [ ] **Conformance fixture data files** — plain JSON/CSV files representing parties,
  agreements, instruments, events, reference data, rules, and expected outputs.
  The hospice example is the candidate first fixture set.

- [ ] **Shared-storage interface contract** — formalize the eight required operations
  in OpenAPI or AsyncAPI. Decide: which format, where does the spec file live
  (this repo or ledger-lab)?

- [ ] **Provider registration model** — define a minimum viable manifest format
  for how an app finds the shared partition endpoint for a given Arrangement.
