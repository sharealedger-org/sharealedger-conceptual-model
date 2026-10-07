# Hospice App — Session Log

Running log of work done on this project. Compress older entries to 3–5 bullets
when the log grows long. Each entry closes with a **State** line.

---

### Session: 2025 — FHIR analysis, prototype architecture, technology stack decisions

**Decisions made this session:**

- **FHIR as the field-level data model.** For the 13 event types well-covered by
  FHIR R4/R5 (MedicationRequest, MedicationDispense, MedicationAdministration,
  Observation, Encounter, CarePlan, EpisodeOfCare, etc.), FHIR resource fields
  *are* the hospice app field-level data model. We do not design a parallel schema.
  The 6 gap event types (Delivery Confirmation, Medication Waste, On-Hand
  Reconciliation, Medication Disposal, Equipment Swap, Equipment Retrieval) require
  purpose-designed field specs informed by FHIR extension patterns.

- **Prototype repo confirmed: `sharealedger-hospice`.** Architecture modeled on the
  RSC demo (VAPostAnalysisRSCDemo) — server holds all state and enforces all rules;
  clients are role-specific thin interfaces; storage is server-side only. RSC's
  named-pipe transport is replaced by HTTPS REST; RSC's terminal UI is replaced by
  a PWA served from the same server.

- **Technology stack:**
  - Server: **Node.js + Express** — event-driven I/O matches concurrent participant
    sessions; JSON native; Dropbox SDK available; ecosystem directly relevant.
  - Client: **Progressive Web App (PWA)** — no app install required; works on any
    smartphone browser via URL or QR code; realistic for family caregivers, nurses,
    pharmacy, and DME staff.
  - Storage: **Dropbox API v2** (server-side only, synthetic data) as first prototype
    instance; OneDrive as second candidate. Storage layer is pluggable — swapping
    providers should require only a config change.
  - Terminal simulation mode: stdin/stdout on same server, for development and
    reproducible demos. Preserves RSC lineage.
  - Dependencies kept minimal: `express`, `dropbox`, `dotenv` only to start.

- **SMS design thread deferred.** SMS as a client transport was evaluated and
  rejected for the hospice prototype (developed-world users have smartphones; SMS
  reliability, cost, and 160-char limits are real constraints). The thin-client
  *principle* is preserved — the PWA is the minimum realistic UI. SMS / USSD /
  WhatsApp Business API as a transport for financial inclusion use cases (different
  from hospice) is recorded as a separate design thread; it shares the same
  server architecture but is not part of the hospice prototype scope.

- **Onboarding model:** Care coordinator (authorizer role) provisions a phone number
  or email into the server. Participant receives a URL by SMS or email. One tap opens
  the role-specific PWA in the browser. No app store, no install, no OAuth complexity
  for the prototype. Preserves the RSC authorizer/instrument provisioning pattern.

- **IBM Cloud no longer the primary prototype target.** Dropbox and OneDrive are
  sufficient for a synthetic-data prototype and demonstrate the portability claim
  more directly. IBM Cloud remains relevant if a HIPAA-eligible deployment is needed.

**New documents needed (next sessions):**
- `projects/hospiceapp/data-model.md` — field-level spec for all entities
- `projects/hospiceapp/sms-protocol.md` — deferred; separate design thread
- `projects/shared-storage/interface-contract.md` — OpenAPI or AsyncAPI spec

**State:** Architecture and stack decided. Three documents needed before prototype
coding begins: data model (hospiceapp), storage interface contract (shared-storage),
and prototype repo scaffold. Next session: data model.

---

### Initial project artifacts created (session: repo restructure)

- `README.md` — full conceptual model mapping, medications, DME, shared/private
  boundary, worked sequence, CKB access-path note.
- `fhir-mapping.md` — FHIR R4/R5 mapping stub; 20-row candidate mapping table;
  six identified gaps; three structural gaps.
- Infrastructure design moved to `projects/shared-storage/`.

**State:** Conceptual model and infrastructure design exist as stubs. See above
session for architecture decisions that supersede the IBM Cloud prototype assumption.
