# Hospice App — Session Log

Running log of work done on this project. Compress older entries to 3–5 bullets
when the log grows long. Each entry closes with a **State** line.

---

### Initial project artifacts created (session: repo restructure)

- `README.md` — full conceptual model mapping for hospice family caregiver shared
  ledger, including medications (individual delivery model), medical equipment (DME),
  shared/private boundary, worked sequence, CKB access-path note. Moved from
  `model/examples/hospice-caregiver/README.md`.
- `fhir-mapping.md` — FHIR R4/R5 mapping stub; 20-row candidate mapping table;
  six identified gaps; three structural gaps. Moved from `decisions/fhir-mapping.md`.
- `shared-storage-infrastructure.md` — infrastructure scope boundary, interface
  contract operations, six candidate provider topologies including blockchain,
  IBM Cloud as initial prototype target. Moved from
  `decisions/shared-storage-infrastructure.md`.

**State:** Conceptual model and infrastructure design exist as stubs. FHIR mapping
and IBM Cloud prototype plan are the two blocking items before any prototype work
can begin. See `todo.md`.
