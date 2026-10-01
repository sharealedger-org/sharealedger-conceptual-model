# Sharealedger Vision

## An open model for economic state

**Status:** Working vision for community discussion. This document is not a ratified standard, implementation specification, or product commitment.

Sharealedger exists to make financial and other performance measurement more open, understandable, reusable, and verifiable. Its long-term vision is an open architecture for representing economic state that can be implemented by different systems, reviewed by different communities, and used by both people and machines.

The central proposition is:

> The durable source of financial meaning should be the governed record of economic events and instruments. Balances, charts of accounts, reports, classifications, and AI features should be derived views rather than the only surviving record.

## The problem

Most enterprise financial systems preserve conclusions about business events more reliably than they preserve the events themselves. Posting processes and pre-built hierarchies are useful for producing known reports, but they can discard temporal sequence, instrument context, counterparty relationships, contractual terms, and attributes that were not part of the original reporting design.

That creates several recurring costs:

- new reporting questions require new extracts, balances, and reconciliations;
- historical classification changes can require reposting or opaque restatement logic;
- finance, risk, management, and operational systems develop separate views of the same economic activity;
- organizations exchange statements and then reconcile independently maintained summaries;
- AI systems receive aggregated representations without the event history and metadata needed to explain or predict the underlying activity.

The historical design choices were often rational responses to the cost of storage and computation. The open question for current systems is whether those choices should remain the permanent definition of the data.

## The proposed architecture

Sharealedger's conceptual model separates business meaning from accounting projections and physical implementation.

### 1. Economic events

An economic event records a change involving resources, agents, arrangements, commitments, or positions. It should retain its identity, effective time, participants, quantities or amounts, causal relationships, source provenance, and lifecycle status.

An event is not defined by the report or account into which a particular participant later projects it.

### 2. Instruments and arrangements

An instrument or arrangement provides the stable context that connects events over time. Examples may include a contract, policy, loan, order, delivery obligation, deposit, claim, or other governed relationship.

A stable Instrument ID should connect the event history to the attributes and terms that explain it. This permits systems to analyze both what happened and what was expected to happen under the arrangement.

### 3. Movement-based instrument ledger

The Instrument Ledger is a durable movement-oriented book of record. It preserves instrument-level changes and derives positions from those movements according to explicit rules.

The ledger should support multiple projections without requiring every projection to become a separate permanently maintained balance store. A position may be calculated for a participant, date, currency, classification, reporting purpose, or other perspective while retaining a trace to the originating events.

### 4. Governed reference data

Reference data supplies the classifications and attributes used to interpret events and instruments. It may include:

- account and financial-statement concepts;
- industry classifications such as UN ISIC and national SIC variants;
- products, facilities, collateral, obligations, and counterparties;
- currencies, units, jurisdictions, and legal entities;
- taxonomies, reporting dimensions, and regulatory mappings.

Reference data must be versioned and effective-dated. A change in classification should not silently rewrite history. The model should support at least three explicit perspectives:

- **Switch:** history remains classified as recorded, with the new classification applying from its effective date;
- **Recast:** historical events are viewed under a selected current classification;
- **Reclass:** an explicit generated event records the transfer between classifications.

### 5. Declarative accounting rules

Accounting rules should be represented as governed policy rather than hidden only in procedural application code. A Finance-authorized rules layer can derive participant-specific accounting entries, classifications, allocations, and reports from shared events and private policy.

The rules layer must remain distinct from the technical transport and execution layer. This allows policy changes to be reviewed, versioned, tested, and applied without redefining the underlying event history.

### 6. Accounting perspectives

Different participants may have different legitimate accounting perspectives on the same event. A seller, buyer, lender, borrower, insurer, regulator, and management group may each derive different entries or reports while sharing selected facts.

The conceptual model therefore distinguishes:

- perspective-independent event facts;
- participant-private mappings, costs, margins, and controls;
- shared facts and commitments;
- derived accounting entries and positions.

A chart of accounts is an important projection, but it is not the universal semantic foundation. Multiple charts and reporting frameworks should be able to map to the same underlying concepts and events.

### 7. Verification and control

An open ledger model must be auditable as well as flexible. Verification should include:

- immutable event identifiers and provenance;
- referential-integrity and temporal-validity checks;
- duplicate, cycle, and overlap detection in reference data;
- balanced projections and control totals;
- contract- or instrument-anchored manual adjustments;
- traceability from a reported amount to its source events;
- explicit quarantine, correction, reversal, and supersession behavior;
- reproducible test cases for every published rule or dataset release.

A claim that a model or dataset is verified should identify the tests, evidence, version, reviewers, and scope of that verification.

## Reference-data registry

Sharealedger should provide a repository and release process for open reference data. Each dataset should have:

- a stable identifier and schema version;
- a source, license, steward, and provenance record;
- effective dates and publication dates;
- explicit deprecation and replacement relationships;
- machine-readable JSON or YAML and analyst-friendly CSV where appropriate;
- validation reports and checksums;
- signed or otherwise authenticated releases;
- documented crosswalks rather than flattened combinations of distinct classification systems.

Users should be able to pin an upstream release and add local overlays. Local use may extend or map the shared data without changing the canonical upstream history. A bot should be able to download a known release, verify it, and use it deterministically.

## AI and machine use

AI should be treated as a consumer and assistant of governed economic data, not as a substitute for the ledger's controls.

A machine-readable event and reference layer can support:

- retrieval by stable concept, instrument, event, and version identifiers;
- forward projections from structured contractual obligations;
- sequence analysis over event history;
- explanation of calculations and classifications;
- anomaly detection with traceable evidence;
- model training on event-native data rather than only posted balances;
- reproducible answers tied to a data and rules release.

The important distinction is between training on a static dump and operating against a live, versioned source. AI systems should be able to identify the exact event, reference-data version, accounting rule, and calculation used in an answer.

Claims that event-native data improves model performance remain empirical claims. Sharealedger should publish experiments, baselines, acceptance criteria, and limitations rather than treating the architectural hypothesis as already proven in every domain.

## Shared inter-enterprise state

When counterparties independently record and summarize the same economic event, they incur a reconciliation obligation. Selected sharing can reduce that duplication without requiring all private information to become public.

A shared partition may contain mutually authorized commitments, fulfillment facts, settlement events, and identifiers. Private partitions may contain internal cost allocations, margins, tax mappings, and management perspectives. The shared event can be authoritative for the facts the parties agreed to share while each participant retains its legitimate private accounting view.

This is not a requirement for a public or trustless blockchain. The appropriate sharing, authorization, cryptographic, and recovery model depends on the relationship between the participants.

## Adoption path

The vision is intentionally implementable in stages:

1. Publish the conceptual model and invariants.
2. Publish governed reference-data packages and worked examples.
3. Provide mappings and adapters for existing ERP and reporting systems.
4. Build a small instrument-ledger implementation and verification suite.
5. Demonstrate projections for finance, risk, management, and AI use cases.
6. Add selected sharing for trusted inter-enterprise relationships.
7. Support migration through parallel runs and reconciliation against existing certified outputs.

Existing ERP systems do not need to be replaced before the model is useful. A read-only event repository, reference-data registry, mapping layer, or shadow ledger can establish value and evidence before an organization changes its system of record.

## Repository responsibilities

The repositories should remain distinct:

- **Conceptual model:** business meaning, relationships, invariants, perspectives, and open decisions.
- **Community:** governance, policies, participation, public discussion, and website content.
- **Operational or prototype repositories:** executable engines, adapters, controls, and measured experiments.
- **LedgerLearning:** educational material, books, historical explanations, and long-lived learning resources.

No implementation, ERP product, or physical engine should silently redefine the conceptual model. Conversely, conceptual proposals should identify their logical representation, candidate physical realizations, worked examples, and falsifiable controls.

## Open questions

The following questions require community review:

- What is the minimum event and instrument vocabulary that remains useful across industries?
- Which attribute domains are canonical, and which belong to local or industry extensions?
- How should authorization, signatures, and release stewardship work for shared reference data?
- Which accounting projections must be demonstrated first?
- What evidence is sufficient to call a rule, dataset, or implementation verified?
- How should privacy, commercial confidentiality, and shared state interact?
- Which parts of the model should be normative, and which should remain alternative realizations?

This vision is a starting point for those decisions. It is not a declaration that they have already been settled.
