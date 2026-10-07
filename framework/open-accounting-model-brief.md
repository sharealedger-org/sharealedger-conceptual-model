# Open Accounting Model Brief

**Status:** Working brief for conceptual-model development. This is not a ratified standard, implementation plan, or product commitment.

## Purpose

Sharealedger is exploring an open, verifiable model for economic state: a model that preserves economic events and instruments, supports participant-specific accounting perspectives, governs the reference data used to interpret them, and can be implemented by different ledger or ERP systems.

The work should make the conceptual foundation precise before it makes a claim about a universal ledger, an ERP product, or an AI advantage.

## The starting proposition

Sharealedger should recover and extend the intelligence embedded in bookkeeping by making financial data accurate, understandable, updateable, secure, accessible, and controlled by the people and institutions whose economic lives it represents.

The technical implication is that events and instrument relationships should remain durable facts. Balances, charts of accounts, classifications, reports, and AI features should be reproducible projections of those facts rather than the only surviving record.

## Branches of the framework

### 1. Economic ontology

Define the minimum concepts that must be shared across implementations:

- Agents and roles;
- Resources and measures;
- Arrangements and contracts;
- Instruments and stable identifiers;
- Commitments and expected future events;
- Economic Events and their causal relationships;
- Movements and derived Positions;
- Evidence, authorization, and provenance.

**Question:** What is the smallest vocabulary that remains useful across finance, insurance, banking, commerce, and other performance-measurement domains?

### 2. Event and instrument history

Define how an Instrument lifecycle is represented through creation, amendment, fulfillment, settlement, cancellation, correction, reversal, novation, split, merge, and replacement.

**Question:** Which facts are immutable, which are superseding facts, and which are derived interpretations?

### 3. Reference-data registry

Define how shared and local reference data is identified, versioned, authorized, released, and consumed by applications. Initial candidate domains include industry classifications, accounts, products, currencies, units, jurisdictions, counterparties, obligations, taxonomies, and reporting dimensions.

Reference data must support valid time, publication time, deprecation, crosswalks, provenance, licensing, and local overlays.

**Question:** Which domains are canonical Sharealedger data, and which should remain external datasets with documented mappings?

### 4. Accounting rules and projections

Define how participants derive accounting entries, balances, allocations, valuations, and reports from shared or private facts. Keep business policy separate from transport and execution.

**Question:** What should a declarative rule contain so that it can be reviewed by Finance, executed by a runtime, and traced to its outputs?

### 5. Perspectives and time

Define the source cutoff, effective time, recorded time, publication time, perspective date, classification generation, and measurement basis for every reproducible view.

Preserve the distinction among:

- **Switch:** classify each event according to its effective-time reference;
- **Recast:** view history under a selected later reference generation;
- **Reclass:** generate explicit events that transfer a prior classification.

**Question:** What evidence and controls distinguish a changed view from a changed accounting fact?

### 6. Verification and control

Define conformance tests for identity, lineage, temporal validity, authorization, balance, conservation, completeness, correction, and reproducibility.

**Question:** What does “verified” mean for a model, dataset, rule, release, or implementation, and who is authorized to make that claim?

### 7. Shared and private state

Define what counterparties may share as a common fact while retaining private mappings, margins, costs, taxes, and management perspectives.

**Question:** What minimum shared event and authorization protocol removes reconciliation without requiring full disclosure?

### 8. AI and machine use

Define machine-readable access to events, instruments, reference data, rules, evidence, and derived positions. AI may retrieve, plan, explain, and propose; deterministic ledger services should calculate and verify financial results.

**Question:** Which claims about event-native data and AI should be treated as hypotheses until measured by public experiments?

### 9. Implementation and adoption

Map the conceptual model to logical schemas, small reference-data packages, adapters, a prototype Instrument Ledger, and migration or shadow-ledger patterns.

**Question:** What is the smallest useful implementation that proves the concepts without committing Sharealedger to one ERP or engine?

## First conformance example

The first shared example should contain:

- two Agents, one buyer and one seller;
- one Arrangement and one Instrument;
- one Contract and its reciprocal Commitment(s);
- one authorized Commitment;
- one Group Event, Subgroup Event, and Event Distribution hierarchy;
- fulfillment and settlement Events;
- a small reference-data generation;
- a later reference-data change;
- Switch, Recast, and Reclass views;
- participant-specific accounting projections;
- Contract Position and Resource Position outputs, including whether they coincide in the example;
- one shared fact and at least one private mapping; and
- one Shared Participant identity containing both participant IDs and the selected shared-data boundary;
- independent participant translations from shared values into local charts and Rules; and
- a balance control evaluated across each participant's shared and private books together; and
- a complete trace from reported amounts to Events, Reference Data, Rules, and evidence.

The first implementation should also document the physical access path used for Contract and
Resource processing and identify whether it resorts, duplicates, or indexes the relevant files.

The example should be representable in plain tables and machine-readable files before any runtime is selected.

## Work products

The conceptual-model repository should develop these artifacts in order:

1. Core vocabulary and invariants.
2. The first conformance example.
3. Plain example data and logical schemas for events, instruments, reference data, rules, and projections.
4. A deterministic calculator with lineage and control totals.
5. A reference-data release manifest and validation convention.
6. Decision records for unresolved alternatives.
7. Candidate mappings to GenevaERS, existing ERP structures, XBRL/Global Ledger, and other relevant standards.
8. A prototype conformance suite and measured implementation experiments.

## Repository boundaries

- `SHAREALEDGER-VISION.md` explains the purpose and long-term direction.
- `model/open-accounting-framework.md` defines the working conceptual vocabulary and invariants.
- This brief organizes the next research and design work.
- `model/practical-implementation-roadmap.md` keeps the next steps focused on data, code, and tests.
- `examples/` should hold worked scenarios and perspective comparisons.
- `decisions/` should hold alternatives, rationale, and accepted choices.
- Operational repositories should hold executable engines, adapters, controls, and benchmarks.
- The community repository should hold governance, participation, and website content.

## Non-goals for the first phase

The first phase should not attempt to:

- replace every ERP function;
- publish a universal chart of accounts;
- make all reference data legally authoritative;
- require blockchain or public consensus;
- expose private participant mappings;
- claim that AI performance improvements are already proven; or
- select GenevaERS as the only valid physical implementation.

## Success condition

The first phase succeeds when an independent reader can take the conformance example, identify the shared economic facts, apply a declared reference-data generation and rule set, produce more than one valid accounting perspective, and trace every result back to its inputs without relying on an undocumented application convention.
