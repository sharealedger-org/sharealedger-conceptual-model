# Sharealedger and an Open ERP: Discussion Starter

**Status:** Working thought for community discussion. This is not an approved project plan,
architecture, or product commitment.

## The Question

Could an enterprise financial system be assembled from open, reusable business definitions and
configuration, executed by a high-throughput ledger engine, instead of having its accounting
semantics and reporting rules inseparably embedded in one application?

This is a possible next step in Sharealedger's existing mission, not a replacement for it. The
2022 vision discussions called for testing whether shared ledgers can improve data quality and
cost, developing methods and open-source components, and building a library that can support
adoption. An open ERP financial foundation could make those goals concrete enough to explore.
See the [March 24, 2022 vision discussion](https://github.com/sharealedger-org/community/blob/master/meetings/WorkMeetings/2022-03-24Meeting_Minutes.md).

## Initial Idea

Sharealedger could curate an open configuration package for financial processes used by ERP
systems. The package would describe business meaning and processing choices, while a separate
runtime would execute them. The initial scope would be a configurable financial core, not an
attempt to replace every ERP application or business function.

The configuration might eventually cover:

- business events and their transformation into balanced journal entries;
- instruments, ledger balances, and effective-dated business attributes;
- accounting and calculation rules that can generate additional journal entries;
- reporting perspectives and the controls used to reconcile them; and
- named workloads that make behavior and evidence reproducible.

The architectural hypothesis is that generated entries and updated ledger state can remain in one
ordered processing flow and feed later calculations and perspectives. The right processing
contracts, data model, and boundaries still need to be demonstrated rather than assumed.

## Possible Roles

- **Sharealedger:** Community home for open business definitions, configuration conventions, and
  discussion of reusable ERP financial processes.
- **GenevaERS:** A candidate execution platform. Its Java Performance Engine work is intended to
  replace the assembler MR95 engine, and its existing YAML and FreeMarker generators may offer a
  foundation to build on. The relationship and extension points are questions for discussion,
  not commitments by either project.
- **Ledger Lab:** A separate research workbench for small workloads, controls, and measured
  evidence. It can test claims about configurations without becoming the ERP runtime or the home
  for the general-purpose package.

This separation could let business configuration outlive a particular execution implementation,
while still testing it against a real engine. It should not create a second engine or duplicate a
generator that already fits the need.

## Longer-Term Hypothesis: Geneva as a View Service

A started GenevaERS task could eventually act as a streaming view service. Source events would be
offered to the active views whose declared predicates and dimensions qualify. An AI-facing
interaction layer could translate a user's question into a constrained view request, but Geneva
would remain responsible for deterministic record selection, effective-dated lookup, aggregation,
controls, and output. The model would plan and explain queries, not calculate financial totals.

The view request would identify its source snapshot, hierarchy version, perspective semantics,
selection and grouping rules, requested measures, and lifecycle:

- **Snapshot view:** answer against a fixed set of committed source partitions. A request captures
  a high-water mark and a reader position. If the reader is already partway through an append-only
  source, it can consume the remainder through the high-water mark, wrap to the beginning, and
  finish at its saved boundary. The boundary record must be included exactly once. Later-appended
  partitions belong to a later snapshot unless explicitly requested.
- **Live view:** subscribe to qualifying events from a declared starting point and continue across
  committed partitions until canceled or closed by policy.
- **Period-close view:** an ordered end-of-day marker closes the period's extract-time buffers,
  emits the view outputs, and records a checkpoint. Late-arriving events need an explicit policy,
  such as reopening/reissuing the affected generation or recording a later-period adjustment.

Classification changes would remain explicit choices rather than an implicit side effect of
updating a master file. Effective-dated reference history can support a **Switch View** (resolve at
event time) or a **Recast View** (resolve at a selected perspective date). A **Reclass View** is
different: it requires balanced, traceable negating/opening business events. Replaying history to
rebuild a report projection must not silently create or alter accounting entries.

An overnight hierarchy update could therefore publish a new effective-dated reference generation;
startup would replay the immutable event history through a captured high-water mark to regenerate
the requested historical report generation, reconcile it, and then attach to live events. Prior
report generations remain identifiable by their hierarchy version and source cutoff. This replay,
the started-task lifecycle, and its buffering, restart, and scale behavior are hypotheses to test;
they are not claims about current GenevaERS capabilities or commitments by Sharealedger or
GenevaERS.

## Working Design Questions

These are hypotheses to evaluate, not settled requirements:

- Could declarative business definitions feed GenevaERS' existing Java code-generation and
  metadata-generation approach?
- Would generated Bash provide an inspectable, editable way to run an ordered workload without
  making JCL the orchestration interface? Existing GenevaERS test tooling may continue to use JCL
  where that is appropriate to its environment.
- For a complete ordered run, should recovery restart the whole attempt from the same immutable
  inputs rather than preserve intermediate checkpoints? Failed outputs would remain private while
  useful failure evidence is retained.
- What is the smallest useful financial workload that would test the configuration boundary,
  ledger behavior, controls, and reporting end to end?
- Which project should own each schema, template, generated artifact, and compatibility promise?

## A Possible First Exploration

Start with one deliberately small financial workload: define a source event, transform it into a
balanced journal entry, update an instrument-level balance, apply one calculation, and produce one
reconciled perspective. Use it to test whether the business configuration can be understood and
reviewed independently of the engine, whether the runtime can execute it in the intended order, and
whether its outputs and controls can be reproduced.

The first outcome need not be software. A shared configuration sketch, a clear ownership map, and
agreement on one falsifiable workload would establish whether this direction is worth pursuing.

## Questions for the Community

1. Is an open, configurable ERP financial foundation a useful expression of Sharealedger's shared-
   ledger mission?
2. Should the initial boundary focus on financial processing and configuration rather than a full
   ERP application?
3. Does the proposed separation among Sharealedger, GenevaERS, and Ledger Lab make sense, and
   where are the ownership boundaries unclear?
4. What existing community work, standards, or prospective users should shape the first workload?
5. What evidence would make the first exploration valuable to adopters rather than only to its
   implementers?