---
docpipe: 1
phase: 7
title: Completion and Approvals
status: final
version: 2.0
upstream: ["01-prd.md", "02-conops.md", "03-opscon.md", "04-techspec.md", "05-requirements.md", "06-validation.md"]
upstream_hash: {"01-prd.md": "0e34202c06cdf092", "02-conops.md": "7fdb53fbc48fff39", "03-opscon.md": "98addfd786475290", "04-techspec.md": "4248dd6478ed6328", "05-requirements.md": "6d65c655a1ac2b42", "06-validation.md": "afcfede65dc2140a"}
finalised: 2026-10-15
---

# Completion and Approvals

Record that the Mākoha specification set is complete, consistent and approved for its intended purpose, with the approved versions pinned. Completion evidence is tool output from `docpipe status` and `docpipe build` on 25 Sep 2026 (cycle 1, v1.0) and on 15 Oct 2026 (revision 2, v2.0). Revised 15 Oct 2026: the v2.0 cycle is recorded beside the v1.0 cycle in every section; nothing from cycle 1 is removed. Identifiers minted here: APR- (approvals), CND- (conditions and follow-up actions).

## 1. Scope of approval (confirmed 25 Sep 2026)

What is approved: the seven phase documents at version 1.0 with the hashes in section 3, compiled as `docs/spec/PSD.md`, together with `docpipe.json` conventions and the Mākoha Design Compendium (25 Sep 2026) as the authoritative build specification they map to.

For what use: the build baseline for milestones M1 to M9 of the Tier 3 first release for telehealth and hospital in the home in New Zealand (PRD section 8.1), and the source of requirements, risks and verification evidence captured into Ketryx for the planned regulatory applications. This approval is not a regulatory submission, a clinical governance ratification of any fragment, or an ethics approval of any study; each of those remains with its named role.

Revision 2 (confirmed 15 Oct 2026): what is approved is the six phase documents at version 2.0 with the hashes in section 3, compiled as `docs/spec/PSD.md` on 15 Oct 2026, mapped to the Mākoha Design Compendium revision 2 (15 Oct 2026). The use is unchanged, with the first-release scope now including the revision 2 modules A6, A7, J4, J5, H4 and F5 under the front-office profile (PRD section 8.1, TechSpec DEC-08) and the remaining revision 2 modules built but not operated until a later release decision.


## 2. Completion checklist (answered from tool output)

| Item | Result | Evidence |
| --- | --- | --- |
| All phases 1 to 6 final and none stale | Met | `docpipe status` 25 Sep 2026: six rows final v1.0, stale = no |
| Zero open markers | Not met; carried as condition CND-01 | 25 markers remain across phases 1 to 5, every one recorded as deferred with its reason: 11 metric baselines captured at cut-over; 2 metric targets set in Ketryx; voice turn latency at M9; availability, RPO and RTO; web framework at M7; operating organisation; payer or funder; bill tracker; standards list; consumer identity provider; pharmacist-prescriber instrument; terminology release cadence; voice acceptance test |
| Every requirement covered by validation | Met | `docpipe check 6` clean: all 187 identifiers referenced; 176 entries, 11 withdrawn listed |
| All change requests closed | Not met; carried as condition CND-02 | CCR-01 to CCR-04 and OCR-01 to OCR-03 applied upstream; CR-01 (claim-type vocabulary, target the compendium Volume 4.2, amended by CCR-04) remains open because the compendium is outside this set |
| Residual risks accepted | Pending approver | Five residual risks in 06-validation.md section 6: inspection and analysis in place of test for 21 requirements; two deferred numbers; national sandbox access; voice model selection; synthetic practice |
| Requirement syntax and identifier checks | Met | `docpipe check 5` clean apart from the two deferred numbers |
| Traceability export | Met | `docs/spec/traceability.csv` built 25 Sep 2026 |

Revision 2 cycle, answered from tool output on 15 Oct 2026:

| Item | Result | Evidence |
| --- | --- | --- |
| All phases 1 to 6 final and none stale | Met | `docpipe status` 15 Oct 2026: six rows final v2.0, stale = no |
| Zero open markers | Not met; carried as condition CND-01 | 28 markers across phases 1 to 5: the 25 of cycle 1 plus three metric baselines for MET-14, MET-15 and MET-17 captured at cut-over |
| Every requirement covered by validation | Met | `docpipe check 6` clean: all 259 REQ identifiers referenced; 248 entries, 11 withdrawn listed; 72 new entries VAL-188 to VAL-259 in activities ACT-10, ACT-11 and ACT-14 to ACT-16 |
| All change requests closed | Not met; carried as conditions CND-02 and CND-17 | CR-01 amended 15 Oct 2026 to add `projection`, still open against the compendium; CR-02 raised against compendium Volume 13.2 (the open item this revision discharges); no change request raised by phases 2 to 6 in this revision |
| Residual risks accepted | Pending approver | Ten residual risks in 06-validation.md section 6: the five of cycle 1 plus providers not selected, taxonomy not ratified, recognition inputs missing, deferred modules without entries, and the inspection and demonstration count now 24 |
| Requirement syntax and identifier checks | Met | `docpipe check 5` clean apart from the two deferred numbers; every new requirement EARS-shaped |
| Traceability export | Met | `docs/spec/traceability.csv` built 15 Oct 2026: 1,108 identifiers once this document's own APR and CND identifiers are counted (1,099 before them); REQ-188 to REQ-259 present with phase 6 references |

## 3. Document register at approval

Pasted from `docs/spec/PSD.md`, built 25 Sep 2026.

| # | Document | Status | Version | Finalised | Hash |
|---|---|---|---|---|---|
| 1 | Product Requirements Document | final | 1.0 | 2026-09-25 | 945319a42d20e0ce |
| 2 | Concept of Operations | final | 1.0 | 2026-09-25 | 978e178898dc37f9 |
| 3 | Operations Concept | final | 1.0 | 2026-09-25 | 2566aaa0e9b9bf55 |
| 4 | Technical Specifications | final | 1.0 | 2026-09-25 | a3e788961563417d |
| 5 | Specific Requirements | final | 1.0 | 2026-09-25 | 182f72a000933d5b |
| 6 | Validation Activities | final | 1.0 | 2026-09-25 | 5f7ecdaa17a52a10 |

Conventions: intended purpose as recorded in `docpipe.json`; identifier pattern `\b[A-Z][A-Z0-9]{0,4}-\d{2,3}\b`; requirement syntax EARS.

Register at revision 2, pasted from `docs/spec/PSD.md` built 15 Oct 2026:

| # | Document | Status | Version | Finalised | Hash |
|---|---|---|---|---|---|
| 1 | Product Requirements Document | final | 2.0 | 2026-10-15 | 0e34202c06cdf092 |
| 2 | Concept of Operations | final | 2.0 | 2026-10-15 | 7fdb53fbc48fff39 |
| 3 | Operations Concept | final | 2.0 | 2026-10-15 | 98addfd786475290 |
| 4 | Technical Specifications | final | 2.0 | 2026-10-15 | 4248dd6478ed6328 |
| 5 | Specific Requirements | final | 2.0 | 2026-10-15 | 6d65c655a1ac2b42 |
| 6 | Validation Activities | final | 2.0 | 2026-10-15 | afcfede65dc2140a |

## 4. Approvals

The product owner is the sole approver for this cycle (stated 25 Sep 2026). Clinical governance, compliance and architecture roles have no named holder yet; their acceptance of residual risks, standards list and deferred stack choices is carried as conditions CND-09 to CND-11.

| Id | Role | Name | Decision | Conditions | Date |
| --- | --- | --- | --- | --- | --- |
| APR-01 | Product owner | Ken Lee | Approve with conditions | CND-01 to CND-11 | 2026-09-25 |
| APR-02 | Product owner | Ken Lee | Approve with conditions (revision 2, v2.0) | CND-01 to CND-11 carried; CND-12 to CND-19 added | 2026-10-15 |

## 5. Release decision

Go: the set is approved with conditions as the build baseline for the Tier 3 New Zealand first release, authorising M1 to M4 to start immediately and M5 onward subject to CND-03 and CND-04 (decided by the product owner, 25 Sep 2026).

Revision 2 (decided by the product owner, 15 Oct 2026): Go stands for v2.0. M4 now includes the eleven new fragment classes; M5 now includes the revision 2 crates (TechSpec COMP-25 to COMP-29 operated, COMP-31 build-only) and is additionally subject to CND-12 and CND-19; M7 and M9 items of ACT-14 to ACT-16 are subject to CND-13.

## 6. Conditions and follow-up actions

| Id | Condition or action | Owner | Due |
| --- | --- | --- | --- |
| CND-01 | Resolve the 25 deferred markers at the milestone each names (cut-over, M7, M9) or by decision of the named role; none blocks M1 to M4 | Deferred owner | Per marker |
| CND-02 | Close CR-01 by closing the claim-type vocabulary in the compendium Volume 4.2 as the union list | Product owner | Before M4 (compiler templates need the closed list) |
| CND-03 | Arrange national sandbox access (Hira, HealthLink, NZePS) and Ketryx MCP authorisation before ACT-09 | Deferred owner | Before M5 |
| CND-04 | Produce the 10,000-patient synthetic practice before M5 | Deferred owner | Before M5 |
| CND-05 | Select the voice model and GPU node, set REQ-146, before M9 | Deferred owner | Before M9 |
| CND-06 | Appoint the New Zealand sponsor and lodge the WAND notification before the first cohort opens | Compliance | Before MOD-05 for the first site |
| CND-07 | Ratify loss matrices for the ten first-release claim types before the Tier 3 release build | Clinical governance | Before M9 exit |
| CND-08 | Track the Medical Products Bill at every milestone exit | Deferred owner | Each milestone |
| CND-09 | Name a clinical governance holder who accepts or rejects the five residual risks in 06-validation.md section 6 and ratifies fragments | Product owner | Before M4 |
| CND-10 | Name a compliance holder who confirms the standards list, appoints the sponsor and lodges the WAND notification | Product owner | Before M5 |
| CND-11 | Name an architecture holder who takes the deferred stack choices (TechSpec section 5) | Product owner | Before M1 exit |
| CND-12 | Select the WhatsApp Business provider (coexistence mode) and the telephony carrier (warm transfer), record their terms in the obligations register (D-14, D-15; TechSpec DEC-09) | Platform operator | Before M5 |
| CND-13 | Ratify the intent taxonomy codebook, urgency bands, tone classes and the default routing rules (D-21) | Clinical governance | Before M7 |
| CND-14 | Decide tokenisation key custody and rotation cadence (D-16; TechSpec DEC-10) | Compliance with architecture | Before M8, or before the release that operates L2 if later |
| CND-15 | Confirm demand for the overlay posture before the incumbent snapshot path is built (D-13; TechSpec DEC-11) | Architecture | Before any overlay deployment is scheduled |
| CND-16 | Activate a deferred revision 2 module (B9, E3, G4, I3, J6, J7, L1, L2, L3, composer, body map, overlay) only after a requirements revision and validation cycle covering it (PRD section 8.1; TechSpec DEC-08) | Product owner | At each activation decision |
| CND-17 | Close CR-02 by ticking the compendium Volume 13.2 item and reflect the `projection` amendment to CR-01 in Volume 4.2 at the next compendium revision | Product owner | With CND-02, before M4 |
| CND-18 | Confirm the Unsolicited Electronic Messages Act 2007 reading (ConOps POL-20, TechSpec STD-17) | Compliance | Before the first campaign publication |
| CND-19 | Produce the synthetic lead set, the scripted call and cue set and the synthetic archive with handwriting beside the synthetic practice (CND-04) | Deferred owner | Before M5 |

## 7. Assumptions

| Assumption | Confidence | How it would be checked |
| --- | --- | --- |
| A sole product-owner approval is sufficient for the build baseline; role approvals are needed before the regulatory application | Medium | Reviewed when CND-09 to CND-11 are filled |
| The revision 2 scope ruling (six modules operated, nine deferred) can be revisited without re-baselining M1 to M4, because activation is a profile manifest change (TechSpec DEC-08) | High | Any activation goes through CND-16 |

## 8. Open questions

- [x] Scope of approval confirmed
- [x] Sole approver: product owner, approve with conditions, 2026-09-25
- [x] Release decision: go
- [ ] Owners for CND-01, CND-03 to CND-05, CND-08: deferred 25 Sep 2026
- [x] Revision 2 re-approval: product owner, approve with conditions, 2026-10-15 (APR-02); CND-12 to CND-19 added
- [ ] Owner for CND-19: deferred 15 Oct 2026
