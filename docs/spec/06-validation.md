---
docpipe: 1
phase: 6
title: Validation Activities
status: final
version: 2.0
upstream: ["05-requirements.md"]
upstream_hash: {"05-requirements.md": "6d65c655a1ac2b42"}
finalised: 2026-10-15
---

# Validation Activities

Plan and record of validating every requirement in 05-requirements.md (final v2.0). Revised 15 Oct 2026 against compendium revision 2: activities ACT-14 to ACT-16 and entries VAL-188 to VAL-259 added for the new requirement sections 14 to 19; existing entries unchanged; cycle 1 remains the planning cycle. Cycle 1 (25 Sep 2026) is the planning cycle: every requirement has one entry inheriting its verification method and acceptance criterion, grouped into activities; complete = no throughout; modification required = no unless stated. Later cycles record outcomes and raise change requests. Identifiers minted here: VAL-nnn (one entry per requirement, same number as the requirement), ACT- (grouped activities), VCR- (change requests raised by validation). Every REQ identifier of phase 5 appears below, including the withdrawn ones, which are listed as not validated.

## 1. Activities

Each activity covers many entries; each entry references exactly one requirement. Evidence location follows the convention in section 5, confirmed 25 Sep 2026.

| Id | Activity | Milestone gate | Environment | Blocker |
| --- | --- | --- | --- | --- |

| ACT-01 | Argument, evaluator and ledger suites (M1 to M3): compile-fail tests, evaluator check catalogue and single-gate negatives, ledger triggers, RLS and replay | M1, M2, M3 | CI | none |
| ACT-02 | Telehealth end-to-end scenario suite on the synthetic practice (M7, M9): pre-intake, brief, session, checks, drafting, delivery | M7, M9 | Staging with synthetic practice | synthetic practice; voice model (M9 items) |
| ACT-03 | HITH end-to-end scenario suite with simulated device streams (M7, M9): promotion, re-score, escalation, handover | M7, M9 | Staging with simulated devices | device simulators; risk engines validated |
| ACT-04 | Inbound pipeline and reconciliation suite (M5): secure messaging fixtures, matcher thresholds, discharge discrepancy episode | M5 | Staging with messaging fixtures | HealthLink test fixtures |
| ACT-05 | Scope-of-practice suite (M6): profile fragments, formulary holds, escalation chain | M6 | Staging | ratified scope fragments |
| ACT-06 | Governance and research suite (M8): sealed envelopes, enrolment with consent, revalidation, evaluation register | M8 | Staging | ethics classification process |
| ACT-07 | Operations drills (M5, M8): migration fixtures, drift retirement, 8 h outage drill, restore drill, attestation | M5, M8 | Staging and scratch restore node | second region; edge hardware |
| ACT-08 | Mode transition tests (M8): attestation, read-only restore, cohort opening, evaluation-zone role | M8 | Staging | none |
| ACT-09 | Interface conformance (M5, M7): Hira, HealthLink, NZePS and HL7 v2 sandboxes, gateway auth, sidecar schema, anchor, Ketryx export | M5, M7 | National sandboxes and vendor test endpoints | Hira, HealthLink, NZePS sandbox access; Ketryx credentials and MCP authorisation |
| ACT-10 | Performance suite on the 10,000-patient synthetic practice, every build (M5 onward); quarterly and monthly MeasureReports for the analysis items | M5 onward | CI performance rig; production for measures | synthetic practice before M5; production data for measures |
| ACT-11 | Security test and inspection (M8): MFA, audit, break-glass, consent, tenancy, seccomp, secrets, manifest, de-identification | M8 | CI and review session | hardware-backed key store |
| ACT-12 | Regulatory and knowledge inspection (M8): bundle verifier, obligations register, ratification gates, retention, terminology pin, configuration audit | M8 | Review session | sponsor appointed; standards list confirmed |
| ACT-13 | Voice sidecar demonstration and tests (M9): interruption, pinned weights, transcript spans, fallback, consent, bounded loop | M9 | Staging with GPU node | voice model selected; GPU hardware |
| ACT-14 | Front door and channels suite (M5, M7, M9; revision 2): lead register and clocks, conversion, omnichannel desk with rule routing and the PHI check (M5), front-office aperture, consoles and form designer (M7), intent classifier, follow-through drafts and campaign drafting (M9); E2E-14, E2E-15, E2E-17 | M5, M7, M9 | Staging with the synthetic lead set and provider fakes; provider sandboxes for the WhatsApp items | synthetic lead set; WhatsApp provider selected (D-14); intent taxonomy ratified (D-21) |
| ACT-15 | Voice line telephony suite (M5, M9; revision 2): IVR floor, identity confirmation, consent prompt, booking by keypad, message taking (M5); dialogue, hand-off cues, after-hours, check-in instruments (M9); E2E-16 | M5, M9 | Staging with a carrier sandbox and the scripted call and cue set; GPU node for M9 items | telephony carrier selected (D-15); voice model (M9 items) |
| ACT-16 | Document intake batch suite (M5, M9; revision 2): batch control, resume and idempotence, field review, unsolicited result trigger (M5); OCR, layout and handwriting engines at volume (M9); E2E-18 | M5, M9 | Staging with the synthetic archive and the reference machine | synthetic archive with handwriting; recognition models; reference machine |

## 2. Validation register

Columns: entry; requirement; activity; method (inherited); evidence location; complete; modification required; change request.


### Argument, gate and ledger invariants

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-001 | REQ-001 | ACT-01 | Test | `evidence/ACT-01/REQ-001/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-002 | REQ-002 | ACT-01 | Test | `evidence/ACT-01/REQ-002/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-003 | REQ-003 | ACT-01 | Test | `evidence/ACT-01/REQ-003/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-004 | REQ-004 | ACT-01 | Test | `evidence/ACT-01/REQ-004/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-005 | REQ-005 | ACT-01 | Test | `evidence/ACT-01/REQ-005/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-006 | REQ-006 | ACT-01 | Test | `evidence/ACT-01/REQ-006/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-007 | REQ-007 | ACT-01 | Test | `evidence/ACT-01/REQ-007/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-008 | REQ-008 | ACT-01 | Test | `evidence/ACT-01/REQ-008/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-009 | REQ-009 | ACT-01 | Test | `evidence/ACT-01/REQ-009/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-011 | REQ-011 | ACT-01 | Test | `evidence/ACT-01/REQ-011/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-012 | REQ-012 | ACT-01 | Test | `evidence/ACT-01/REQ-012/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-013 | REQ-013 | ACT-01 | Test | `evidence/ACT-01/REQ-013/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-014 | REQ-014 | ACT-01 | Inspection | Inspection record `evidence/ACT-01/REQ-014/` signed by the reviewer | no | no | none |
| VAL-015 | REQ-015 | ACT-01 | Inspection | Inspection record `evidence/ACT-01/REQ-015/` signed by the reviewer | no | no | none |
| VAL-016 | REQ-016 | ACT-01 | Inspection | Inspection record `evidence/ACT-01/REQ-016/` signed by the reviewer | no | no | none |
| VAL-017 | REQ-017 | ACT-01 | Test | `evidence/ACT-01/REQ-017/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-018 | REQ-018 | ACT-01 | Test | `evidence/ACT-01/REQ-018/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-020 | REQ-020 | ACT-01 | Test | `evidence/ACT-01/REQ-020/` under the build hash; mirrored to Ketryx | no | no | none |

### Telehealth consultation (SCN-01)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-021 | REQ-021 | ACT-02 | Test | `evidence/ACT-02/REQ-021/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-022 | REQ-022 | ACT-02 | Test | `evidence/ACT-02/REQ-022/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-023 | REQ-023 | ACT-02 | Test | `evidence/ACT-02/REQ-023/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-024 | REQ-024 | ACT-02 | Test | `evidence/ACT-02/REQ-024/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-025 | REQ-025 | ACT-02 | Test | `evidence/ACT-02/REQ-025/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-027 | REQ-027 | ACT-02 | Test | `evidence/ACT-02/REQ-027/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-028 | REQ-028 | ACT-02 | Test | `evidence/ACT-02/REQ-028/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-029 | REQ-029 | ACT-02 | Test | `evidence/ACT-02/REQ-029/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-030 | REQ-030 | ACT-02 | Test | `evidence/ACT-02/REQ-030/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-031 | REQ-031 | ACT-02 | Test | `evidence/ACT-02/REQ-031/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-032 | REQ-032 | ACT-02 | Test | `evidence/ACT-02/REQ-032/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-033 | REQ-033 | ACT-02 | Test | `evidence/ACT-02/REQ-033/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-034 | REQ-034 | ACT-02 | Test | `evidence/ACT-02/REQ-034/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-035 | REQ-035 | ACT-02 | Test | `evidence/ACT-02/REQ-035/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-036 | REQ-036 | ACT-02 | Test | `evidence/ACT-02/REQ-036/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-037 | REQ-037 | ACT-02 | Test | `evidence/ACT-02/REQ-037/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-039 | REQ-039 | ACT-02 | Test | `evidence/ACT-02/REQ-039/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-040 | REQ-040 | ACT-02 | Test | `evidence/ACT-02/REQ-040/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-041 | REQ-041 | ACT-02 | Test | `evidence/ACT-02/REQ-041/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-042 | REQ-042 | ACT-02 | Test | `evidence/ACT-02/REQ-042/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-043 | REQ-043 | ACT-02 | Test | `evidence/ACT-02/REQ-043/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-044 | REQ-044 | ACT-02 | Test | `evidence/ACT-02/REQ-044/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-045 | REQ-045 | ACT-02 | Test | `evidence/ACT-02/REQ-045/` under the build hash; mirrored to Ketryx | no | no | none |

### HITH supervision and deterioration (SCN-02, SCN-03)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-046 | REQ-046 | ACT-03 | Test | `evidence/ACT-03/REQ-046/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-047 | REQ-047 | ACT-03 | Test | `evidence/ACT-03/REQ-047/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-048 | REQ-048 | ACT-03 | Test | `evidence/ACT-03/REQ-048/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-049 | REQ-049 | ACT-03 | Test | `evidence/ACT-03/REQ-049/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-051 | REQ-051 | ACT-03 | Test | `evidence/ACT-03/REQ-051/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-052 | REQ-052 | ACT-03 | Test | `evidence/ACT-03/REQ-052/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-053 | REQ-053 | ACT-03 | Test | `evidence/ACT-03/REQ-053/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-054 | REQ-054 | ACT-03 | Test | `evidence/ACT-03/REQ-054/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-056 | REQ-056 | ACT-03 | Test | `evidence/ACT-03/REQ-056/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-057 | REQ-057 | ACT-03 | Test | `evidence/ACT-03/REQ-057/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-058 | REQ-058 | ACT-03 | Test | `evidence/ACT-03/REQ-058/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-059 | REQ-059 | ACT-03 | Test | `evidence/ACT-03/REQ-059/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-060 | REQ-060 | ACT-03 | Test | `evidence/ACT-03/REQ-060/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-061 | REQ-061 | ACT-03 | Test | `evidence/ACT-03/REQ-061/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-062 | REQ-062 | ACT-03 | Test | `evidence/ACT-03/REQ-062/` under the build hash; mirrored to Ketryx | no | no | none |

### Inbound documents and reconciliation (SCN-04, SCN-05)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-063 | REQ-063 | ACT-04 | Test | `evidence/ACT-04/REQ-063/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-064 | REQ-064 | ACT-04 | Test | `evidence/ACT-04/REQ-064/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-065 | REQ-065 | ACT-04 | Test | `evidence/ACT-04/REQ-065/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-066 | REQ-066 | ACT-04 | Test | `evidence/ACT-04/REQ-066/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-067 | REQ-067 | ACT-04 | Test | `evidence/ACT-04/REQ-067/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-068 | REQ-068 | ACT-04 | Test | `evidence/ACT-04/REQ-068/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-069 | REQ-069 | ACT-04 | Test | `evidence/ACT-04/REQ-069/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-070 | REQ-070 | ACT-04 | Test | `evidence/ACT-04/REQ-070/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-071 | REQ-071 | ACT-04 | Test | `evidence/ACT-04/REQ-071/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-072 | REQ-072 | ACT-04 | Test | `evidence/ACT-04/REQ-072/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-073 | REQ-073 | ACT-04 | Test | `evidence/ACT-04/REQ-073/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-074 | REQ-074 | ACT-04 | Test | `evidence/ACT-04/REQ-074/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-075 | REQ-075 | ACT-04 | Test | `evidence/ACT-04/REQ-075/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-076 | REQ-076 | ACT-04 | Test | `evidence/ACT-04/REQ-076/` under the build hash; mirrored to Ketryx | no | no | none |

### Scope of practice and escalation (SCN-06)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-077 | REQ-077 | ACT-05 | Test | `evidence/ACT-05/REQ-077/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-078 | REQ-078 | ACT-05 | Test | `evidence/ACT-05/REQ-078/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-079 | REQ-079 | ACT-05 | Test | `evidence/ACT-05/REQ-079/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-080 | REQ-080 | ACT-05 | Test | `evidence/ACT-05/REQ-080/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-081 | REQ-081 | ACT-05 | Test | `evidence/ACT-05/REQ-081/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-082 | REQ-082 | ACT-05 | Test | `evidence/ACT-05/REQ-082/` under the build hash; mirrored to Ketryx | no | no | none |

### Prospective studies and research (SCN-07)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-083 | REQ-083 | ACT-06 | Test | `evidence/ACT-06/REQ-083/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-084 | REQ-084 | ACT-06 | Test | `evidence/ACT-06/REQ-084/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-085 | REQ-085 | ACT-06 | Test | `evidence/ACT-06/REQ-085/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-086 | REQ-086 | ACT-06 | Test | `evidence/ACT-06/REQ-086/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-087 | REQ-087 | ACT-06 | Test | `evidence/ACT-06/REQ-087/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-088 | REQ-088 | ACT-06 | Test | `evidence/ACT-06/REQ-088/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-089 | REQ-089 | ACT-06 | Test | `evidence/ACT-06/REQ-089/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-090 | REQ-090 | ACT-06 | Test | `evidence/ACT-06/REQ-090/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-091 | REQ-091 | ACT-06 | Test | `evidence/ACT-06/REQ-091/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-092 | REQ-092 | ACT-06 | Test | `evidence/ACT-06/REQ-092/` under the build hash; mirrored to Ketryx | no | no | none |

### Onboarding, drift and outage (SCN-08, SCN-09, SCN-10)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-093 | REQ-093 | ACT-07 | Test | `evidence/ACT-07/REQ-093/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-095 | REQ-095 | ACT-07 | Test | `evidence/ACT-07/REQ-095/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-096 | REQ-096 | ACT-07 | Test | `evidence/ACT-07/REQ-096/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-097 | REQ-097 | ACT-07 | Test | `evidence/ACT-07/REQ-097/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-098 | REQ-098 | ACT-07 | Test | `evidence/ACT-07/REQ-098/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-099 | REQ-099 | ACT-07 | Test | `evidence/ACT-07/REQ-099/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-100 | REQ-100 | ACT-07 | Demonstration | Demonstration record and recording `evidence/ACT-07/REQ-100/` | no | no | none |
| VAL-101 | REQ-101 | ACT-07 | Test | `evidence/ACT-07/REQ-101/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-102 | REQ-102 | ACT-07 | Test | `evidence/ACT-07/REQ-102/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-103 | REQ-103 | ACT-07 | Test | `evidence/ACT-07/REQ-103/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-104 | REQ-104 | ACT-07 | Inspection | Inspection record `evidence/ACT-07/REQ-104/` signed by the reviewer | no | no | none |
| VAL-105 | REQ-105 | ACT-07 | Test | `evidence/ACT-07/REQ-105/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-106 | REQ-106 | ACT-07 | Inspection | Inspection record `evidence/ACT-07/REQ-106/` signed by the reviewer | no | no | none |
| VAL-107 | REQ-107 | ACT-07 | Test | `evidence/ACT-07/REQ-107/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-108 | REQ-108 | ACT-07 | Test | `evidence/ACT-07/REQ-108/` under the build hash; mirrored to Ketryx | no | no | none |

### Modes of operation

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-109 | REQ-109 | ACT-08 | Test | `evidence/ACT-08/REQ-109/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-110 | REQ-110 | ACT-08 | Test | `evidence/ACT-08/REQ-110/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-111 | REQ-111 | ACT-08 | Test | `evidence/ACT-08/REQ-111/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-112 | REQ-112 | ACT-08 | Test | `evidence/ACT-08/REQ-112/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-113 | REQ-113 | ACT-08 | Test | `evidence/ACT-08/REQ-113/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-114 | REQ-114 | ACT-08 | Inspection | Inspection record `evidence/ACT-08/REQ-114/` signed by the reviewer | no | no | none |

### Technical interfaces

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-115 | REQ-115 | ACT-09 | Test | `evidence/ACT-09/REQ-115/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-116 | REQ-116 | ACT-09 | Test | `evidence/ACT-09/REQ-116/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-118 | REQ-118 | ACT-09 | Test | `evidence/ACT-09/REQ-118/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-119 | REQ-119 | ACT-09 | Test | `evidence/ACT-09/REQ-119/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-121 | REQ-121 | ACT-09 | Test | `evidence/ACT-09/REQ-121/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-122 | REQ-122 | ACT-09 | Test | `evidence/ACT-09/REQ-122/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-123 | REQ-123 | ACT-09 | Test | `evidence/ACT-09/REQ-123/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-124 | REQ-124 | ACT-09 | Test | `evidence/ACT-09/REQ-124/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-125 | REQ-125 | ACT-09 | Test | `evidence/ACT-09/REQ-125/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-126 | REQ-126 | ACT-09 | Test | `evidence/ACT-09/REQ-126/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-127 | REQ-127 | ACT-09 | Test | `evidence/ACT-09/REQ-127/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-128 | REQ-128 | ACT-09 | Test | `evidence/ACT-09/REQ-128/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-129 | REQ-129 | ACT-09 | Test | `evidence/ACT-09/REQ-129/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-130 | REQ-130 | ACT-09 | Test | `evidence/ACT-09/REQ-130/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-131 | REQ-131 | ACT-09 | Test | `evidence/ACT-09/REQ-131/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-132 | REQ-132 | ACT-09 | Test | `evidence/ACT-09/REQ-132/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-133 | REQ-133 | ACT-09 | Test | `evidence/ACT-09/REQ-133/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-134 | REQ-134 | ACT-09 | Demonstration | Demonstration record and recording `evidence/ACT-09/REQ-134/` | no | no | none |

### Performance and capacity

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-135 | REQ-135 | ACT-10 | Test | `evidence/ACT-10/REQ-135/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-136 | REQ-136 | ACT-10 | Test | `evidence/ACT-10/REQ-136/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-137 | REQ-137 | ACT-10 | Test | `evidence/ACT-10/REQ-137/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-138 | REQ-138 | ACT-10 | Test | `evidence/ACT-10/REQ-138/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-139 | REQ-139 | ACT-10 | Test | `evidence/ACT-10/REQ-139/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-140 | REQ-140 | ACT-10 | Test | `evidence/ACT-10/REQ-140/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-141 | REQ-141 | ACT-10 | Test | `evidence/ACT-10/REQ-141/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-142 | REQ-142 | ACT-10 | Test | `evidence/ACT-10/REQ-142/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-143 | REQ-143 | ACT-10 | Test | `evidence/ACT-10/REQ-143/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-144 | REQ-144 | ACT-10 | Inspection | Inspection record `evidence/ACT-10/REQ-144/` signed by the reviewer | no | no | none |
| VAL-145 | REQ-145 | ACT-10 | Analysis | MeasureReport lineage in the ledger; `evidence/ACT-10/REQ-145/` | no | no | none |
| VAL-146 | REQ-146 | ACT-10 | Test | `evidence/ACT-10/REQ-146/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-147 | REQ-147 | ACT-10 | Test | `evidence/ACT-10/REQ-147/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-148 | REQ-148 | ACT-10 | Test | `evidence/ACT-10/REQ-148/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-149 | REQ-149 | ACT-10 | Test | `evidence/ACT-10/REQ-149/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-150 | REQ-150 | ACT-10 | Analysis | MeasureReport lineage in the ledger; `evidence/ACT-10/REQ-150/` | no | no | none |
| VAL-151 | REQ-151 | ACT-10 | Analysis | MeasureReport lineage in the ledger; `evidence/ACT-10/REQ-151/` | no | no | none |
| VAL-152 | REQ-152 | ACT-10 | Test | `evidence/ACT-10/REQ-152/` under the build hash; mirrored to Ketryx | no | no | none |

### Security and privacy

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-153 | REQ-153 | ACT-11 | Test | `evidence/ACT-11/REQ-153/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-154 | REQ-154 | ACT-11 | Inspection | Inspection record `evidence/ACT-11/REQ-154/` signed by the reviewer | no | no | none |
| VAL-155 | REQ-155 | ACT-11 | Test | `evidence/ACT-11/REQ-155/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-156 | REQ-156 | ACT-11 | Test | `evidence/ACT-11/REQ-156/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-157 | REQ-157 | ACT-11 | Test | `evidence/ACT-11/REQ-157/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-158 | REQ-158 | ACT-11 | Test | `evidence/ACT-11/REQ-158/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-159 | REQ-159 | ACT-11 | Test | `evidence/ACT-11/REQ-159/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-160 | REQ-160 | ACT-11 | Test | `evidence/ACT-11/REQ-160/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-161 | REQ-161 | ACT-11 | Test | `evidence/ACT-11/REQ-161/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-162 | REQ-162 | ACT-11 | Inspection | Inspection record `evidence/ACT-11/REQ-162/` signed by the reviewer | no | no | none |
| VAL-163 | REQ-163 | ACT-11 | Inspection | Inspection record `evidence/ACT-11/REQ-163/` signed by the reviewer | no | no | none |
| VAL-164 | REQ-164 | ACT-11 | Test | `evidence/ACT-11/REQ-164/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-166 | REQ-166 | ACT-11 | Test | `evidence/ACT-11/REQ-166/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-167 | REQ-167 | ACT-11 | Test | `evidence/ACT-11/REQ-167/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-168 | REQ-168 | ACT-11 | Test | `evidence/ACT-11/REQ-168/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-169 | REQ-169 | ACT-11 | Test | `evidence/ACT-11/REQ-169/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-170 | REQ-170 | ACT-11 | Test | `evidence/ACT-11/REQ-170/` under the build hash; mirrored to Ketryx | no | no | none |

### Regulatory, knowledge and data

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-171 | REQ-171 | ACT-12 | Test | `evidence/ACT-12/REQ-171/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-172 | REQ-172 | ACT-12 | Inspection | Inspection record `evidence/ACT-12/REQ-172/` signed by the reviewer | no | no | none |
| VAL-173 | REQ-173 | ACT-12 | Test | `evidence/ACT-12/REQ-173/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-174 | REQ-174 | ACT-12 | Test | `evidence/ACT-12/REQ-174/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-175 | REQ-175 | ACT-12 | Test | `evidence/ACT-12/REQ-175/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-176 | REQ-176 | ACT-12 | Test | `evidence/ACT-12/REQ-176/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-178 | REQ-178 | ACT-12 | Inspection | Inspection record `evidence/ACT-12/REQ-178/` signed by the reviewer | no | no | none |
| VAL-179 | REQ-179 | ACT-12 | Inspection | Inspection record `evidence/ACT-12/REQ-179/` signed by the reviewer | no | no | none |
| VAL-180 | REQ-180 | ACT-12 | Inspection | Inspection record `evidence/ACT-12/REQ-180/` signed by the reviewer | no | no | none |

### Voice interaction (CAP-20)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-181 | REQ-181 | ACT-13 | Demonstration | Demonstration record and recording `evidence/ACT-13/REQ-181/` | no | no | none |
| VAL-182 | REQ-182 | ACT-13 | Inspection | Inspection record `evidence/ACT-13/REQ-182/` signed by the reviewer | no | no | none |
| VAL-183 | REQ-183 | ACT-13 | Test | `evidence/ACT-13/REQ-183/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-184 | REQ-184 | ACT-13 | Test | `evidence/ACT-13/REQ-184/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-185 | REQ-185 | ACT-13 | Test | `evidence/ACT-13/REQ-185/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-186 | REQ-186 | ACT-13 | Test | `evidence/ACT-13/REQ-186/` under the build hash; mirrored to Ketryx | no | no | none |

### Coverage of upstream

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-187 | REQ-187 | ACT-01 | Test | `evidence/ACT-01/REQ-187/` under the build hash; mirrored to Ketryx | no | no | none |

### Front door and lead register (SCN-11)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-188 | REQ-188 | ACT-14 | Test | `evidence/ACT-14/REQ-188/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-189 | REQ-189 | ACT-14 | Test | `evidence/ACT-14/REQ-189/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-190 | REQ-190 | ACT-14 | Test | `evidence/ACT-14/REQ-190/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-191 | REQ-191 | ACT-14 | Test | `evidence/ACT-14/REQ-191/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-192 | REQ-192 | ACT-14 | Test | `evidence/ACT-14/REQ-192/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-193 | REQ-193 | ACT-14 | Test | `evidence/ACT-14/REQ-193/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-194 | REQ-194 | ACT-14 | Inspection | Inspection record `evidence/ACT-14/REQ-194/` signed by the reviewer | no | no | none |
| VAL-195 | REQ-195 | ACT-14 | Test | `evidence/ACT-14/REQ-195/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-196 | REQ-196 | ACT-14 | Test | `evidence/ACT-14/REQ-196/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-197 | REQ-197 | ACT-14 | Test | `evidence/ACT-14/REQ-197/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-198 | REQ-198 | ACT-14 | Test | `evidence/ACT-14/REQ-198/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-199 | REQ-199 | ACT-14 | Test | `evidence/ACT-14/REQ-199/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-200 | REQ-200 | ACT-14 | Test | `evidence/ACT-14/REQ-200/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-201 | REQ-201 | ACT-14 | Test | `evidence/ACT-14/REQ-201/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-202 | REQ-202 | ACT-14 | Test | `evidence/ACT-14/REQ-202/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-203 | REQ-203 | ACT-14 | Test | `evidence/ACT-14/REQ-203/` under the build hash; mirrored to Ketryx | no | no | none |

### Omnichannel desk (SCN-12)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-204 | REQ-204 | ACT-14 | Test | `evidence/ACT-14/REQ-204/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-205 | REQ-205 | ACT-14 | Test | `evidence/ACT-14/REQ-205/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-206 | REQ-206 | ACT-14 | Test | `evidence/ACT-14/REQ-206/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-207 | REQ-207 | ACT-14 | Test | `evidence/ACT-14/REQ-207/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-208 | REQ-208 | ACT-14 | Test | `evidence/ACT-14/REQ-208/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-209 | REQ-209 | ACT-14 | Test | `evidence/ACT-14/REQ-209/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-210 | REQ-210 | ACT-14 | Test | `evidence/ACT-14/REQ-210/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-211 | REQ-211 | ACT-14 | Test | `evidence/ACT-14/REQ-211/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-212 | REQ-212 | ACT-14 | Test | `evidence/ACT-14/REQ-212/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-213 | REQ-213 | ACT-14 | Test | `evidence/ACT-14/REQ-213/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-214 | REQ-214 | ACT-14 | Test | `evidence/ACT-14/REQ-214/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-215 | REQ-215 | ACT-14 | Test | `evidence/ACT-14/REQ-215/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-216 | REQ-216 | ACT-14 | Demonstration | Demonstration record and recording `evidence/ACT-14/REQ-216/` | no | no | none |

### Voice line (SCN-13)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-217 | REQ-217 | ACT-15 | Test | `evidence/ACT-15/REQ-217/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-218 | REQ-218 | ACT-15 | Test | `evidence/ACT-15/REQ-218/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-219 | REQ-219 | ACT-15 | Test | `evidence/ACT-15/REQ-219/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-220 | REQ-220 | ACT-15 | Test | `evidence/ACT-15/REQ-220/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-221 | REQ-221 | ACT-15 | Test | `evidence/ACT-15/REQ-221/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-222 | REQ-222 | ACT-15 | Test | `evidence/ACT-15/REQ-222/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-223 | REQ-223 | ACT-15 | Test | `evidence/ACT-15/REQ-223/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-224 | REQ-224 | ACT-15 | Test | `evidence/ACT-15/REQ-224/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-225 | REQ-225 | ACT-15 | Test | `evidence/ACT-15/REQ-225/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-226 | REQ-226 | ACT-15 | Test | `evidence/ACT-15/REQ-226/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-227 | REQ-227 | ACT-15 | Test | `evidence/ACT-15/REQ-227/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-228 | REQ-228 | ACT-15 | Test | `evidence/ACT-15/REQ-228/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-229 | REQ-229 | ACT-15 | Test | `evidence/ACT-15/REQ-229/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-230 | REQ-230 | ACT-15 | Test | `evidence/ACT-15/REQ-230/` under the build hash; mirrored to Ketryx | no | no | none |

### Form designer (SCN-14)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-231 | REQ-231 | ACT-14 | Test | `evidence/ACT-14/REQ-231/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-232 | REQ-232 | ACT-14 | Test | `evidence/ACT-14/REQ-232/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-233 | REQ-233 | ACT-14 | Test | `evidence/ACT-14/REQ-233/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-234 | REQ-234 | ACT-14 | Test | `evidence/ACT-14/REQ-234/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-235 | REQ-235 | ACT-14 | Test | `evidence/ACT-14/REQ-235/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-236 | REQ-236 | ACT-14 | Test | `evidence/ACT-14/REQ-236/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-237 | REQ-237 | ACT-14 | Inspection | Inspection record `evidence/ACT-14/REQ-237/` signed by the reviewer | no | no | none |
| VAL-238 | REQ-238 | ACT-14 | Test | `evidence/ACT-14/REQ-238/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-239 | REQ-239 | ACT-14 | Test | `evidence/ACT-14/REQ-239/` under the build hash; mirrored to Ketryx | no | no | none |

### Document intake at volume (SCN-15)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-240 | REQ-240 | ACT-16 | Test | `evidence/ACT-16/REQ-240/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-241 | REQ-241 | ACT-16 | Test | `evidence/ACT-16/REQ-241/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-242 | REQ-242 | ACT-16 | Test | `evidence/ACT-16/REQ-242/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-243 | REQ-243 | ACT-16 | Test | `evidence/ACT-16/REQ-243/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-244 | REQ-244 | ACT-16 | Test | `evidence/ACT-16/REQ-244/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-245 | REQ-245 | ACT-16 | Test | `evidence/ACT-16/REQ-245/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-246 | REQ-246 | ACT-16 | Inspection | Inspection record `evidence/ACT-16/REQ-246/` signed by the reviewer | no | no | none |
| VAL-247 | REQ-247 | ACT-16 | Test | `evidence/ACT-16/REQ-247/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-248 | REQ-248 | ACT-16 | Test | `evidence/ACT-16/REQ-248/` under the build hash; mirrored to Ketryx | no | no | none |

### Campaigns, follow-through and revision 2 cross-cutting rules (SCN-16)

| Entry | Requirement | Activity | Method | Evidence | Complete | Modification | Change request |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VAL-249 | REQ-249 | ACT-14 | Test | `evidence/ACT-14/REQ-249/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-250 | REQ-250 | ACT-14 | Test | `evidence/ACT-14/REQ-250/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-251 | REQ-251 | ACT-14 | Test | `evidence/ACT-14/REQ-251/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-252 | REQ-252 | ACT-14 | Test | `evidence/ACT-14/REQ-252/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-253 | REQ-253 | ACT-14 | Test | `evidence/ACT-14/REQ-253/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-254 | REQ-254 | ACT-14 | Test | `evidence/ACT-14/REQ-254/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-255 | REQ-255 | ACT-14 | Test | `evidence/ACT-14/REQ-255/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-256 | REQ-256 | ACT-14 | Test | `evidence/ACT-14/REQ-256/` under the build hash; mirrored to Ketryx | no | no | none |
| VAL-257 | REQ-257 | ACT-11 | Inspection | Inspection record `evidence/ACT-11/REQ-257/` signed by the reviewer | no | no | none |
| VAL-258 | REQ-258 | ACT-11 | Inspection | Inspection record `evidence/ACT-11/REQ-258/` signed by the reviewer | no | no | none |
| VAL-259 | REQ-259 | ACT-10 | Test | `evidence/ACT-10/REQ-259/` under the build hash; mirrored to Ketryx | no | no | none |

### Withdrawn requirements (not validated)

| Entry | Requirement | Status |
| --- | --- | --- |
| VAL-010 | REQ-010 | Withdrawn in phase 5; no activity |
| VAL-019 | REQ-019 | Withdrawn in phase 5; no activity |
| VAL-026 | REQ-026 | Withdrawn in phase 5; no activity |
| VAL-038 | REQ-038 | Withdrawn in phase 5; no activity |
| VAL-050 | REQ-050 | Withdrawn in phase 5; no activity |
| VAL-055 | REQ-055 | Withdrawn in phase 5; no activity |
| VAL-094 | REQ-094 | Withdrawn in phase 5; no activity |
| VAL-117 | REQ-117 | Withdrawn in phase 5; no activity |
| VAL-120 | REQ-120 | Withdrawn in phase 5; no activity |
| VAL-165 | REQ-165 | Withdrawn in phase 5; no activity |
| VAL-177 | REQ-177 | Withdrawn in phase 5; no activity |

## 3. Summary counts (cycle 1, counted)

| Count | Value |
| --- | --- |
| Requirements with an entry | 248 (176 at cycle 1 plus 72 at revision 2) |
| Withdrawn identifiers listed | 11 |
| Entries complete | 0 |
| Entries with modification required | 0 |
| Open change requests | 0 |
| Entries by method | Test 221, Inspection 20, Analysis 3, Demonstration 4 |
| Activities | 16 |

## 4. Change requests

None raised in cycle 1. Revision of 15 Oct 2026: none raised.

| Id | Raised by | Target document | Target item | Change | Status |
| --- | --- | --- | --- | --- | --- |

## 5. Evidence convention (confirmed)

Every activity writes its evidence under `evidence/<activity>/<requirement>/` keyed by the build hash of the manifest it ran against, and every record is mirrored into Ketryx through TIF-16 with the REQ identifier as the trace key. Test evidence is the CI artefact (log, result file, timing table). Inspection evidence is a signed inspection record naming the reviewer and the artefact inspected. Analysis evidence is the MeasureReport with lineage. Demonstration evidence is a written record plus a recording where consent allows. Confirmed 25 Sep 2026.

## 6. Residual risks and known limitations

| Risk or limitation | Bearing on validation |
| --- | --- |
| 20 requirements are validated by inspection, 3 by analysis and 4 by demonstration rather than test | Acceptable for structural and measure-based items; each names its artefact; to be reconfirmed with compliance for the regulatory application |
| REQ-145 (availability, RPO, RTO) and REQ-146 (voice turn latency) carry deferred numbers | Their entries cannot pass until the numbers are set |
| National sandbox access (Hira, HealthLink, NZePS) is not yet arranged | ACT-09 is blocked until onboarding |
| The voice model is not yet selected | ACT-13 and the voice items in ACT-02 are blocked until M9 |
| The synthetic practice is not yet produced | ACT-10 and every scenario suite are blocked until it exists (PRD open item) |
| WhatsApp and telephony providers are not yet selected (D-14, D-15; revision 2) | ACT-14 provider items and ACT-15 are blocked until selection before M5; fakes cover the rule and PHI-check items |
| The intent taxonomy codebook is not yet ratified (D-21; revision 2) | VAL-207 and the classifier items of ACT-14 cannot pass until ratification before M7 |
| Recognition models, the synthetic archive and the reference machine for ACT-16 do not yet exist (revision 2) | VAL-241 to VAL-246 are blocked until M9 inputs exist; batch-control items run on fixtures |
| Deferred revision 2 modules (PRD section 8.1) carry no requirement and no entry | Their activation needs a later requirements revision and validation cycle before operation |

## 7. Assumptions

| Assumption | Confidence | How it would be checked |
| --- | --- | --- |
| One activity per section is the right grouping; a milestone may split it | Medium | Revisited at each milestone exit |
| Ketryx MCP authorisation is available before M5 so evidence mirroring starts with the first suites | Medium | Connector authorised |

## 8. Open questions

- [x] Evidence convention confirmed (section 5)
- [ ] Blocker owners: deferred 25 Sep 2026
- [x] Revision 2 (15 Oct 2026): ACT-14 to ACT-16, VAL-188 to VAL-259 added
- [ ] Owners for the revision 2 blockers (providers, taxonomy, synthetic archive): platform operator for D-14 and D-15, clinical governance for D-21, otherwise deferred
