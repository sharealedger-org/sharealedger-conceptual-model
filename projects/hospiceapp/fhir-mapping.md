# Decision: FHIR Mapping for Healthcare Domain Events

**Status:** Open question — stub for required work. Not a ratified decision or product commitment.

**Related documents:**
- [`model/examples/hospice-caregiver/README.md`](../model/examples/hospice-caregiver/README.md)
- [`decisions/shared-storage-infrastructure.md`](shared-storage-infrastructure.md)

---

## The question

HL7 FHIR R4/R5 is the dominant interoperability standard for healthcare data exchange. Existing
hospice EMR systems, pharmacy dispensing systems, and DME supplier platforms that speak FHIR are
the most likely integration points for any prototype of the hospice caregiver shared ledger
example. Sharealedger must define explicit mappings between its event types and FHIR resource
types in order to:

- exchange events with existing clinical systems that already produce or consume FHIR resources;
- provide a credible interoperability story to the healthcare IT community;
- avoid inventing a parallel vocabulary where a standard one already exists; and
- identify precisely where FHIR coverage is incomplete and Sharealedger extensions or profiles
  are required.

This decision record is a stub. The mappings must be worked out with reference to FHIR R4/R5
specifications and tested against at least one working FHIR server before this record can be
considered resolved.

---

## FHIR is a compatibility surface, not the conceptual foundation

The Sharealedger conceptual model defines event semantics independently of any wire format or
storage standard. FHIR mappings are a compatibility surface — a translation layer that allows
Sharealedger events to be exchanged with FHIR-capable systems. They do not redefine the
Sharealedger event model.

Specifically:

- A Sharealedger **Medication Order** event is not defined as a FHIR `MedicationRequest`; it is
  defined by the conceptual model. The FHIR mapping says how to represent a Medication Order
  event as a `MedicationRequest` for exchange with a clinical system.
- Where FHIR has no equivalent resource (e.g., home delivery confirmation, on-hand
  reconciliation), the Sharealedger event type is primary and a FHIR extension or profile must
  be defined, not the other way around.
- The Sharealedger shared/private partition boundary has no FHIR equivalent. FHIR access
  control (SMART on FHIR scopes, Consent resources) is the translation mechanism, but it does
  not replace the conceptual model's partition definition.

---

## Known mappings (preliminary, unvalidated)

The following table records initial candidate mappings from the hospice example event types to
FHIR R4/R5 resource types. All entries are preliminary and must be validated.

| Sharealedger event type | Candidate FHIR R4/R5 resource | Coverage notes |
|---|---|---|
| Medication Order | `MedicationRequest` | Good fit; order intent, dosage, route, prescriber, status |
| Medication Dispense | `MedicationDispense` | Good fit; quantity, lot number, dispenser, status |
| Delivery Confirmation | No standard resource | Candidate: `Observation` with custom code, or `MedicationDispense` with delivery extension; gap requires a profile |
| Medication Administration | `MedicationAdministration` | Good fit; medication, dosage, route, performer, effective time |
| Medication Waste | No standard resource | Candidate: `MedicationAdministration` with wasNotGiven + waste code, or custom extension; gap requires a profile |
| On-Hand Reconciliation | No standard resource | No FHIR equivalent; requires custom profile; candidate: `Observation` with structured component values |
| Medication Disposal | No standard resource | Candidate: `MedicationDispense` with status = `on-hold` or custom extension; gap requires a profile |
| Equipment Order | `DeviceRequest` | Reasonable fit; device type, quantity, requester, status |
| Equipment Delivery and Setup | `DeviceDelivery` (R5) / `Procedure` (R4 workaround) | `DeviceDelivery` added in R5; R4 requires a workaround |
| Equipment Malfunction | `DeviceAlert` (R5) / `Flag` or `Observation` (R4) | Gap in R4; R5 `DeviceAlert` is a closer fit |
| Equipment Swap | No standard resource | Candidate: two linked `DeviceDelivery` resources (one for retrieval, one for delivery); gap requires a profile |
| Equipment Retrieval | No standard resource | No FHIR equivalent; candidate: `DeviceDelivery` with direction = return, or custom profile |
| Symptom Observation | `Observation` | Good fit; code from LOINC/SNOMED, value, performer, effective time |
| Comfort Assessment | `Observation` | Good fit; structured using standard pain/dyspnea scales |
| Nurse Visit | `Encounter` | Good fit; episode of care, participants, period, class |
| Question Submitted | `Communication` | Reasonable fit; sender, recipient, payload, status |
| Question Answered | `Communication` (reply) | Reasonable fit; in-response-to link |
| Care Plan Amendment | `CarePlan` (revised version) | Good fit; CarePlan supports versioning through status transitions and revision history |
| Episode Transition | `EpisodeOfCare` (status change) | Good fit; EpisodeOfCare status lifecycle covers admission, active, finished |

**Coverage summary:**
- **Well-covered by existing FHIR resources:** medication order, dispense, administration;
  symptom/comfort observations; nurse visits; questions; care plan; episode lifecycle
- **Partially covered, R5 improves on R4:** equipment delivery, equipment alerts
- **Gaps requiring custom profiles or extensions:** delivery confirmation, medication waste,
  on-hand reconciliation, medication disposal, equipment swap, equipment retrieval

---

## What FHIR does not cover

Beyond specific missing resource types, three structural gaps between FHIR and the Sharealedger
model must be addressed in any integration design:

1. **Shared/private partition boundary.** FHIR has no concept of a fact that is jointly
   owned by multiple unaffiliated organizations with a declared shared boundary. FHIR access
   control governs who can read a resource on a given server; it does not express that a
   resource is a shared fact agreed upon by a nurse, a pharmacy, and a family caregiver.
   The mapping must define how the Sharealedger partition boundary is represented in FHIR
   consent and access control terms.

2. **Open Commitment as a first-class position.** FHIR `MedicationRequest` can have a status
   of `active` (not yet dispensed). But there is no standard FHIR query that returns "all
   medications ordered but not yet confirmed delivered to this patient" as a named position.
   That derivation lives in Sharealedger's position layer, not in FHIR.

3. **Administration-implies-delivery inference rule.** The Sharealedger rule that a
   `MedicationAdministration` event implicitly closes an open delivery-status position has
   no FHIR equivalent. This is a Sharealedger business rule that must be applied in the
   mapping layer, not a FHIR native behavior.

---

## Work required to resolve this record

1. Validate each candidate mapping in the table above against the FHIR R4/R5 specification.
2. Author FHIR profiles or extensions for the six gap event types.
3. Define the FHIR representation of the Sharealedger shared/private partition boundary.
4. Specify how the three structural gaps above are handled in the mapping layer.
5. Test the mappings against a reference FHIR server (e.g., HAPI FHIR) with synthetic data
   from the hospice example.
6. Publish the validated mappings as a Sharealedger FHIR Implementation Guide (IG) or
   equivalent artifact.

This work is a prerequisite for the hospice prototype to interoperate with existing clinical
systems. It does not need to be complete before the first prototype is built, but it must be
started before the prototype claims clinical system interoperability.
