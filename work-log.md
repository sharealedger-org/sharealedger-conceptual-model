# Conceptual Model — Work Log

This file records open work items, session notes, and follow-on tasks at the
repo level. Project-specific work is tracked in each project's own `log.md`
and `todo.md`. Items here concern the framework layer, repo structure, and
cross-cutting concerns.

---

## Session: 2025 — Repo Restructure + Confidentiality Fixes

### Work completed this session

**conceptual-model repo:**
- Restructured into three-layer architecture: `sources/`, `framework/`, `projects/`
- All files moved, new project stubs created (ledger-lab), STARTUP.md added, README rewritten
- Committed: `restructure: sources / framework / projects three-layer architecture`

**members repo:**
- E205, E206, E210, E211, E220, E221 transcript titles renamed from HSBC to
  "Global Financial Institution POC" series
- Topical_Index.md committed (had been created last session but not committed)
- Committed in two commits: rename/add new files, then remove old HSBC files

**ledgerlearning repo:**
- README.md updated (CwK episode count 250+ → 330+, expanded description, CwK corpus section)
- **NOT YET COMMITTED** — Dropbox sync was interfering; commit manually:
  `git add README.md && git commit -m "README: update CwK episode count and description; add CwK corpus section"`

---

## Session: 2025 — Repo Restructure (sources / framework / projects)

### Work completed this session

**Repo restructured into three-layer architecture:**
- `framework/` — generalized shared-ledger principles (was `model/`)
- `projects/` — goal-directed work threads with README, todo, and log per project
- `sources/` — contributed materials with copyright retained by contributors

**Files moved:**
- `model/open-accounting-framework.md` → `framework/`
- `model/open-accounting-model-brief.md` → `framework/`
- `model/practical-implementation-roadmap.md` → `framework/`
- `model/examples/hospice-caregiver/README.md` → `projects/hospiceapp/README.md`
- `decisions/fhir-mapping.md` → `projects/hospiceapp/fhir-mapping.md`
- `decisions/shared-storage-infrastructure.md` → `projects/hospiceapp/shared-storage-infrastructure.md`
- `decisions/theoretical-foundation.md` → `sources/theoretical-foundation.md`
- `model/source/VA Data Samples and Specs.xlsx` → `sources/`
- `GenevaERS/` → `sources/GenevaERS/`
- `presentations/` → `sources/presentations/`

**New files created:**
- `STARTUP.md` — session startup checklist
- `projects/ledger-lab/README.md` — project stub
- `projects/hospiceapp/todo.md`, `projects/hospiceapp/log.md`
- `projects/ledger-lab/todo.md`, `projects/ledger-lab/log.md`
- `README.md` — fully rewritten to reflect new structure

**Also this session (members repo):**
- E205, E206, E210, E211, E220, E221 transcript titles renamed from HSBC to
  "Global Financial Institution POC" series; all file names, title lines, and
  cross-references updated across README, Sequential_Scan, XLSX_Correlation,
  and Topical_Index.

---

## Session: 2025 — Hospice Example, Infrastructure, and Corpus Infrastructure

### Work completed this session

**New files:**
- `model/examples/hospice-caregiver/README.md` — hospice family caregiver shared ledger
  example; full conceptual model mapping including medications (individual delivery model),
  medical equipment (DME), shared/private boundary, worked sequence, CKB access-path note
- `decisions/shared-storage-infrastructure.md` — infrastructure scope boundary, interface
  contract operations, candidate provider topologies (6 including blockchain), IBM Cloud
  as initial prototype target
- `decisions/fhir-mapping.md` — FHIR R4/R5 mapping stub; 20-row candidate mapping table;
  six identified gaps; three structural gaps; work required before interoperability claims
- `decisions/theoretical-foundation.md` — extended with CwK corpus reference section and
  13-episode blockchain position table

**Updated files:**
- `README.md` — registered new examples and decisions in the index
- `decisions/shared-storage-infrastructure.md` — added blockchain topology 6 with the
  five-gap analysis grounded in CwK episodes; expanded FHIR topology 4 with specific
  resource mappings and gap identification
- Members repo `E196` transcript — location field updated from specific institution name
  to "Global financial institution, Buffalo, NY"
- LedgerLearning `README.md` — added Conversations with Kip transcript corpus section
  with members repo pointer and access permissions statement
- Members repo `content/conversations-with-kip/Topical_Index.md` — new 14-section
  topical index bridging E-number corpus to conceptual model documents

---

## Open Work Items for Next Session(s)

### HIGH — Required before hospice prototype can be built

- [x] **E205/E206/E210/E211/E220 titles in members repo** — files were named using a specific
  institution name (HSBC). Renamed to "Global Financial Institution POC" series:
  - Transcript files renamed: `E305_`–`E309_` prefixed files in `Transcripts/`
  - Title lines updated inside each file
  - Cross-references updated in `README.md`, `Transcript_Sequential_Scan.md`,
    `Transcript_XLSX_Correlation_ByDate.md`, and `Topical_Index.md`
  - E221 (Kolkata Part 2, no file downloaded) title updated in index files
  - Note: the work log previously cited E305–E309 E-numbers; the actual E-numbers for
    these POC episodes are E205, E206, E210, E211, E220, E221

- [ ] **E271 transcript body** — contains a specific institution name in the body text
  (not just location metadata). Review and redact or generalize as appropriate.
  File: `members/content/conversations-with-kip/Transcripts/E271_Data_Quality_and_People_qTf886PKgkw.md`

- [ ] **Full corpus scan for confidential institution names** — a systematic grep across
  all transcript files in `members/content/conversations-with-kip/Transcripts/` for
  known institution names. The E196 fix and the E305–E309/E342 items were identified
  opportunistically; a full scan is needed to ensure completeness.

- [ ] **FHIR mapping decision record** (`decisions/fhir-mapping.md`) — current status is
  stub. Needs:
  1. Validation of each mapping row against FHIR R4/R5 specs
  2. FHIR profiles or extensions for the six gap event types
  3. Shared/private partition representation in FHIR consent/access control
  4. Three structural gap handling specifications
  5. Test against a reference FHIR server (HAPI FHIR) with synthetic hospice data
  6. Publication as a Sharealedger FHIR Implementation Guide

- [ ] **IBM Cloud prototype plan** — `decisions/shared-storage-infrastructure.md` names
  IBM Cloud as the prototype target and lists the six-component stack, but no implementation
  plan exists. A minimum viable prototype spec is needed: which component first, what
  synthetic data set, what acceptance test, who operates the IBM Cloud account.

### MEDIUM — Important for conceptual model completeness

- [ ] **First conformance example data files** — `model/practical-implementation-roadmap.md`
  calls for plain JSON/CSV fixture files representing parties, agreements, instruments,
  events, reference data, rules, and expected outputs. None exist yet. The hospice example
  is a candidate second fixture; the purchase/settlement example from the framework is
  the first. Ledger Lab owns execution; this repo owns the fixture definitions.

- [ ] **Decision records for open framework questions** — the framework
  (`model/open-accounting-framework.md`) names several unresolved questions in
  "Logical representation questions" (§ at end). Each should become a decision record stub:
  - Event / Movement / Position as separate record types vs. common lineage model
  - Global vs. scoped identifiers
  - Commitment reciprocity (buyer's and seller's commitments as one shared fact vs. two)
  - Amount / quantity / unit / currency / uncertainty representation
  - Late-arriving and corrected events affecting snapshots and period-close views
  - Rules declaring dependencies and producing auditable generated events
  - Minimum conformance suite definition

- [ ] **Corpus method for conceptual-model repo** — you asked about applying the corpus
  navigation method (topical index pointing to original materials) to the conceptual-model
  repo itself. The repo currently has a flat `decisions/` directory and a flat `model/`
  directory with no topic-first navigation layer. As the number of documents grows,
  a topical index or topic map analogous to `Topical_Index.md` in the members repo
  would help. Define the right structure before the document count grows further.

- [ ] **Shared-storage interface contract formalization** — `decisions/shared-storage-infrastructure.md`
  names eight required operations for the interface contract. These should be formalized
  in a machine-readable format (OpenAPI or AsyncAPI) before prototype implementation begins.
  Decision: which format, and where does the spec file live (this repo or Ledger Lab)?

- [ ] **Provider registration model** — `decisions/shared-storage-infrastructure.md` names
  the provider registration problem (how does an app find the shared partition endpoint
  for a given Arrangement?) as unresolved. A minimum viable manifest format needs to be
  defined before the prototype can be built.

### LOWER — Background / research tasks

- [ ] **Members repo README** — the members repo top-level `README.md` should be updated
  to register the new `Topical_Index.md` and explain the relationship between the
  corpus guide, the topical index, and the sequential scan documents.

- [ ] **CwK corpus guide update** — `Conversations_With_Kip_Corpus_Guide.md` was written
  for the older 057-episode numbering. The thematic taxonomy there is incomplete relative
  to the full E-number corpus. The new `Topical_Index.md` is the richer entry point, but
  the guide should be updated to point to it and note the relationship.

- [ ] **GenevaERS conceptual mapping** — `GenevaERS/ERP_DISCUSSION_STARTER.md` exists but
  has not been read or evaluated in this session. It should be read and assessed against
  the current conceptual model to determine what it adds, what it conflicts with, and
  whether it belongs in `decisions/` as a mapping record.

- [ ] **Monograph Papers 03–09** — Papers 00–02 are available in the members research
  directory and are referenced in `decisions/theoretical-foundation.md`. Papers 03–09
  cover the full architecture, GenevaERS, enterprise transformation, reclassification,
  operational integrity, legacy conversion, and shared ledgers. As each paper circulates,
  it should be registered in `theoretical-foundation.md` with its key correspondences
  to the conceptual model.

- [ ] **VA source workbook analysis** — `model/source/VA Data Samples and Specs.xlsx`
  is listed in the README as historical source material but has not been analyzed in
  this session. It likely contains the original VA Arrangement Ledger data that the
  monograph cites as one of its two production natural experiments. Reading and mapping
  its contents to the conceptual model would strengthen the empirical grounding.

---

## Confidentiality Notes

**Do not use specific institution names in this public repo.** Use generic descriptions:
- "global financial institution" or "major global bank" for large international banks
- "major U.S. insurer" for the insurance production natural experiment
- "major U.S. agency" for the VA / government context

Specific institution names found and already addressed:
- E196 transcript location (members repo) — fixed previous session
- E205, E206, E210, E211, E220, E221 transcript titles (members repo) — renamed to
  "Global Financial Institution POC" series; all file names, title lines, and
  cross-references updated

If you encounter any other institution names in any public repo file, fix immediately
and log here.
