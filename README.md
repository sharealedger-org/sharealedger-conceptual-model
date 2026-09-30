# Sharealedger Conceptual Model

This repository is the conceptual home for Sharealedger's model of perspective-independent shared bookkeeping. It describes the business concepts, relationships, invariants, and accounting perspectives that implementations should preserve. It is intentionally separate from any one ledger engine, ERP product, or physical data layout.

**Status:** Foundational concepts and historical source material are collected here for community discussion. This is not yet a ratified standard, implementation specification, or product commitment.

## Why This Repository

Sharealedger's vision is to improve financial and other forms of performance measurement through community-led innovation, a library of concepts and software for shared bookkeeping, and adoption at lower cost and higher scale. A stable conceptual model can help the community discuss what is shared, what remains private to each participant, how events relate to resources and agents, and how different accounting perspectives are produced before those ideas are encoded in a particular system.

The model should be useful independently of its implementation. GenevaERS, Universal Ledger, and other systems can be compared as physical realizations of the concepts; implementation constraints should be recorded without silently redefining the concepts themselves.

## Model Scope

The conceptual work may cover:

- **Business ontology:** Involved Parties, Contracts/Arrangements, Commitments, Resources, Positions, and economic Events.
- **Event semantics:** perspective-independent event definitions, event duality, provenance, and the relationship between source events and generated accounting entries.
- **Financial perspectives:** participant-specific chart of accounts, balance views, Switch/Recast/Reclass semantics, and reconciliation obligations.
- **Shared and private state:** which event facts and relationships are shared, which remain participant-private, and how shared identifiers connect participant partitions without collapsing their books.
- **Model invariants:** identity, effective time, amount/sign conventions, balancing, lifecycle, and rules for correcting, reversing, or superseding events.

This repository is not the home for a production ledger engine, an ERP application, or a single mandated physical schema. CKB groups, sorting, buffering, and storage layouts are physical realization topics and must be labeled as such.

## Conceptual Layers

Keep these views distinct and explicitly connected:

1. **Conceptual model:** business meaning and invariants, independent of a particular application or report.
2. **Logical model:** records, identifiers, relationships, temporal rules, and constraints that represent the concepts.
3. **Accounting projection:** participant-specific journal entries, chartfields, balances, and reports derived from shared or private events.
4. **Physical realization:** files, database structures, CKB groups, streams, generated code, and recovery processes used by a runtime.

A proposal should say which layer it changes and show the mapping to adjacent layers. A physical optimization must not silently become a new business definition; a participant-specific account mapping must not be mistaken for the shared event ontology.

## Historical Starting Point

[presentations/MSU%20edu%20KMT%20Guest%20Lecture%20Slides%20Apr%202020.pdf](presentations/MSU%20edu%20KMT%20Guest%20Lecture%20Slides%20Apr%202020.pdf) is a historical starting point for the model discussion. The April 2020 guest lecture connects REA, FTP/Universal Ledger prototypes, event duality, Contract/Commitment/Resource concepts, CKB-oriented physical groupings, and shared/private ledger partitioning. It is source material for discussion, not a current approved model specification.

The deck was created by Kip Twitchell for a guest lecture to Dr. William E. McCarthy's students at Michigan State University and contributed to Sharealedger with IBM authorization. Original slide attributions and notices remain in the deck. The accompanying conceptual materials in this repository follow Sharealedger's business-content licensing policy.

## Context and Related Work

- [Sharealedger.org](https://sharealedger.org/) states the community vision and mission.
- [LedgerLearning white papers](https://ledgerlearning.com/whitepapers/) provide related research on financial data maintenance, event-based systems, REA, shared ledgers, and system renewal.
- The [Sharealedger community repository](https://github.com/sharealedger-org/community) remains the home for community governance, discussion starters, and meeting records.
- [Ledger Lab](https://github.com/sharealedger-org/ledger-lab) is a separate research workbench for executable prototypes, controls, and measured evidence. A passing prototype does not by itself ratify this conceptual model.

## How to Contribute

Start proposals as questions or alternatives, not assumed facts. For a substantive change, include:

- the concept or invariant being clarified;
- a worked business example and the participating perspectives;
- valid-time and event-lifecycle implications;
- the logical representation and any competing choices;
- mappings to accounting projections and candidate physical realizations;
- controls or falsifiable examples that could distinguish the alternatives.

Record unresolved choices and rationale in version-controlled decision notes. Do not present a proposal as adopted until the Sharealedger community's review and governance process has accepted it.

## Repository Layout

- `presentations/` — attributed historical talks and source material.
- `model/` — conceptual entities, relationships, invariants, and diagrams to be developed.
- `examples/` — worked business scenarios and perspective comparisons.
- `decisions/` — open questions, alternatives, and accepted model decisions.

The initial repository starts with this README and the 2020 lecture deck. The model, examples, and decisions directories will be added as community work is ready; their absence is not a claim that the content is complete.

## Licensing

- Executable code is licensed under [Apache License 2.0](LICENSE-Apache.md).
- Business and conceptual content is licensed under [Creative Commons Attribution 4.0 International](LICENSE-CC4.0.md), subject to the attribution and notices accompanying each work.
- The lecture deck retains its original slide-level attributions and notices; see the source-material note above.
