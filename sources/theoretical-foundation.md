# Theoretical Foundation of the Sharealedger Conceptual Model

**Status:** Working note. Not a ratified standard or product commitment.

---

## Purpose

This note records the relationship between the Sharealedger conceptual model and the academic
monograph that provides its theoretical and empirical foundation. The conceptual model formalizes
the architecture for community use; the monograph provides the information-theoretic argument,
the production evidence, and the peer-review-quality grounding for why that architecture is correct.

---

## The Monograph

*The Architecture of Enterprise Financial Truth: Nine Studies in Data, Measurement, and System
Design* (Twitchell, forthcoming) is a nine-paper academic monograph currently in draft and
circulating for private comment among Sharealedger members.

The monograph makes three large claims:

**Tier 1 — The compression problem is formally characterized.**
Posting transactions to balance hierarchies is a lossy compression of business events in the
Shannon sense. The minimum cost architecture sits at an interior point on the
transaction/balance spectrum. The right-hand arm of the cost curve rises combinatorially
as balance key permutations scale as (1+v)^m. Two production natural experiments —
a major global bank's Arrangement Ledger and a major U.S. insurer's policy transaction
data store — prove the optimal architecture is feasible at enterprise scale.

**Tier 2 — The solution is known, production-proven at scale, and generalizable.**
The ARE (Accounting Rules Engine) / Instrument Ledger / Extract pipeline separates
accounting rules from ledger state, processes movements as primary facts, and derives
every downstream output — finance, risk, regulatory, management, AI training — from a
single source without reconciliation. Five institutions independently arrived at the
same architectural diagnosis. GenevaERS is the enabling engine.

**Tier 3 — The AI moment makes this historically invisible fact suddenly consequential.**
Pre-hierarchy event repositories are the only enterprise training corpora that have not
destroyed their information content through balance posting. No model can reconstruct
the mutual information destroyed by the posting process — the information bound is a
function of the data, not the algorithm.

---

## Mapping to the Conceptual Model

The conceptual model developed in this repository is the community formalization of the
architecture the monograph describes. The key correspondences:

| Monograph concept | Conceptual model concept |
|---|---|
| Pre-hierarchy event | Event / Movement |
| Arrangement Ledger | Instrument Ledger / Movement-based Position |
| Instrument ID as anchor key | Instrument (stable join key) |
| Contract Attributes Record (CAR) | Reference datum + Arrangement/Contract |
| ARE (Accounting Rules Engine) | Rule + Accounting projection |
| Switch / Recast / Reclass | Reference-data perspectives (same names) |
| Posting = lossy compression | Events as primary facts; Positions as derived |
| Shared ledger / counterparty reconciliation | Shared and private state |
| Minimum cost curve | Materialization frontier (conceptual model does not yet formalize this; monograph Paper 1 is the source) |

---

## Papers Circulating for Comment

Papers 00–02 are available to Sharealedger members in the private `sharealedger-org/members`
repository. They cover:

- **Paper 00** — Introduction and Master Framework: the 35-year argument arc, the JPEG/RAW
  analogy for information loss, and why this moment is when the argument becomes provable.
- **Paper 01** — The Minimum Cost Curve: formal information-theoretic grounding of the
  compression claim; the interior minimum; the Instrument Pivot Theorem (omnidirectional
  queryability at zero marginal cost per new reporting dimension).
- **Paper 02** — Pre-Hierarchy Event Repositories as AI Training Corpora: the AI consequence
  of Paper 01; the information ceiling imposed by posting; the proposed empirical test.

Papers 03–09 cover the full architecture, GenevaERS technology, enterprise transformation
patterns, reclassification, operational integrity, legacy conversion, and shared ledgers.

---

## Citation

These papers are pre-publication drafts. Do not cite without the author's permission.
When available, full citations will be added here.

Author contact: kip.twitchell@sharealedger.org
