---
docpipe: 1
phase: 1
title: Product Requirements Document
status: final
version: 2.0
upstream: ["00-idea.md"]
upstream_hash: {"00-idea.md": "0e9f1f8a3d5668f2"}
finalised: 2026-10-15
---

# Product Requirements Document

Revised 25 Sep 2026 after finalisation on approval of change requests CCR-01 to CCR-04 raised in 02-conops.md and OCR-01 to OCR-03 raised in 03-opscon.md (FDA as possible third regulator; Ketryx and billing questions closed): first release moved to Tier 3, pre-intake agent placed in Tier 3, New Zealand regulatory wording corrected, voice capability added. Structure unchanged.

Revised 15 Oct 2026 on compendium revision 2 (15 Oct 2026), which folds the Care Execution Platform teardown into the compendium in situ: two user rows added (section 3), four metrics minted (MET-14 to MET-17), capabilities CAP-21 to CAP-28 minted from Volume 1A.2 rows 21 to 28, operations 18 to 24 placed in section 8.2, the first-release module set from revision 2 stated (section 8.1), constraints CST-14 to CST-18 minted, decisions D-12 to D-21 carried into section 10, CR-01 amended with `projection` and CR-02 raised. Scope rulings stated by Ken Lee on 15 Oct 2026. Structure unchanged.

Source of record for every derived statement below: the Mākoha Design Compendium (25 Sep 2026, revision 2 of 15 Oct 2026, Ken Lee), `docs/ref/makoha-design-compendium.md`, cited by volume and section. Identifiers minted here: G- (goals), NG- (non-goals), CAP- (capabilities), MET- (success metrics), CST- (constraints). Identifiers of the form D-nn and the acceptance-test ids (for example NER-01, LED-03) are the compendium's own and are carried unchanged.

## 1. Intended purpose and conventions of this set

Confirmed 25 Sep 2026 and recorded in `docpipe.json`.

| Convention | Value |
| --- | --- |
| Intended purpose | A build-ready specification set that a delivery team or coding agents with no access to the source repositories can build Mākoha from, tier by tier, and that can be exported as the regulator bundle for each tier. (Confirmed unchanged 25 Sep 2026; the launch strategy in section 8.1 is detail under this intent, not a change to it.) |
| Project name / system name | Mākoha / Mākoha platform |
| Identifier pattern | `\b[A-Z][A-Z0-9]{0,4}-\d{2,3}\b`; compendium families (D-, E2E-, LED-, ARG-, REN-, ADV-, ENG-, KP-, PUR-, and the capability and operation test ids) adopted unchanged; PRD families listed above |
| Requirement syntax (phase 5) | EARS: keyword start (The / When / While / If / Where), exactly one "shall" per requirement |

Identifiers are minted once and never renumbered; a withdrawn item is kept with a reason.

## 2. Problem statement

Derived from Volume 1.1.

Primary care produces most of its knowledge as free text: consultation notes, referral letters, discharge summaries, pathology comments, patient messages. Current systems store this text but cannot reason over it, so the clinician re-reads it every visit, safety checks fire on coded fields only, and audit means sampling paper. Learned models can now read that text well, but with unstated error rates and no way to state their certainty in a form a safety case can use.

Two gaps, closed together: (a) language becomes structured facts with provenance to the span they came from; (b) every machine proposal carries a machine-checkable statement of its own uncertainty, and a fixed arithmetic procedure decides whether it may be shown, must be flagged, or must be withheld. The same procedure runs identically years later against the same pinned inputs, which is what makes the system auditable rather than merely logged.

## 3. Users and settings

Derived from Volume 1.4 and Volume 1A.4. Each row becomes a role and a setting profile in phase 3.

| Setting / user | Primary gain | What they do today instead | Governed by |
| --- | --- | --- | --- |
| General practice (GP) | Consult-prep brief within a reading budget; safety checks on free text as well as codes; coding proposals with span-level evidence | Re-read the record each visit; coded-field-only alerts; manual coding | Volumes 9, 12 |
| Nurse and pharmacist prescribers | Scope-of-practice profile applied at evaluation time; every prescribing argument carries the guideline fragment and its version | Phone the GP; paper protocols | Volumes 5, 6 |
| Telehealth clinicians and locums | Agentic pre-intake (typed, or by voice for patients slow at or unable to text) produces structured grounds before the call; the pre-intake summary is itself an argument, rejectable line by line | Unprepared sessions with unfamiliar patients | Volumes 4, 9 |
| Hospital in the home (HITH) teams | Orders sent straight to patients with a state machine surfacing overdue and unacknowledged items; inbound results reconcile to the originating order | Ward-style supervision without ward tooling | Volume 3 |
| Practice governance and regulators | Sentinel events, prospective studies and audits are queries over the ledger; a regulator bundle is a signed export of a time window | Audit by sampling paper; studies as projects | Volumes 8, 10 |
| Patients | Engagement loops driven by released arguments only; never sees a held or flagged item; sees a released one only after sign-off | Plan communicated verbally or not at all | Volumes 2, 9 |
| Study owners and clinical researchers (through the governance face) | Prospective studies registered as sealed envelopes, cohorts by phenotype, enrolment on match with consent scope, endpoints as validated Measures, consented de-identified extracts | Studies as separate projects outside the record | Volumes 2A, 3A.10, 10.4 |
| Front office and practice growth (revision 2; front-office profile, 1A.4; restricted clinician aperture, 2A.0) | A lead register with response clocks, an omnichannel desk, a voice line and a form designer that all write to the same record; outreach that is itself a released argument; nothing clinical signable | Reception handsets, spreadsheets of enquiries, paper forms, a separate CRM | Volumes 1A, 3A groups A, H, J; 9.8 |
| Partners and integrators (revision 2; deferred from the first release, section 8.1) | Tenancy with brand packs, a developer platform with a sandbox and typed SDKs, engines admitted only under the purity contract | Bespoke integrations | Volumes 11.8, 12.4, 12.5, 3A.12b |

First adopters (stated 25 Sep 2026): telehealth and hospital-in-the-home services whose workforce is general practitioners together with nurse and pharmacist prescribers, on the Tier 3 general-purpose-assistant profile so that real-time voice interaction ships from day one (CCR-02). General practice as a standalone setting, and patients as a face, follow after the first release. Front-office staff of those two services operate the front-office profile from the first release (stated 15 Oct 2026). See section 8.

## 4. Goals and non-goals

Goals derived from Volume 1.1 and the horizon statements of Volume 1A.8; non-goals verbatim from Volume 1.3.

| Id | Goal | Horizon statement (1A.8) |
| --- | --- | --- |
| G-01 | Structured, span-provenanced facts from all free text in the record | No fact written in prose is lost |
| G-02 | Every recommendation reaches a person only as a gated argument with typed uncertainty | Only arithmetic releases (Law 4) |
| G-03 | Every decision replayable byte for byte from pinned inputs | Deterioration detected as one reconstructable trajectory; evidence loop closed |
| G-04 | Clinician prepared before every session within an attention budget | No clinician opens a consultation unprepared |
| G-05 | Every prescription checked against the whole reconciled medication story | Every prescription checked against the whole medication story |
| G-06 | Inbound results, letters and messages triaged and routed before a human sees them | Every result, letter and message read and actioned before a human sees it |
| G-07 | Advanced-practice prescribers at top of scope with a full-context escalation packet | Context, not calls |
| G-08 | Patients receive their signed plan in their own words | Patients receive their plan in their own words |
| G-09 | Primary care as a complete, consent-respecting, de-identified longitudinal dataset | Primary care as a complete longitudinal dataset |
| G-10 | Prospective clinical studies run concurrently with operations from the first launch: they validate the system, support iterative development cycles and allow user-group feedback, so safety and efficacy evidence accrues in the ledger alongside use (stated 25 Sep 2026) | Guidelines measured against practice, practice against outcomes, evidence loop closed |

| Id | Non-goal (Volume 1.3) |
| --- | --- |
| NG-01 | Autonomous prescribing, or acting on an order without a signing clinician |
| NG-02 | Online learning in production |
| NG-03 | Fusing probabilities from different engines into a single score |
| NG-04 | Presenting a base model's opinion of its own output as a control (it may only feed a human-review queue) |
| NG-05 | Ranking patients or clinicians by any composite; risk registers list evidence-backed suspects, each with its own argument |

## 5. Governing principles

Derived from Volume 1.2 and 1.6. These ten laws bind every downstream document; each has a conformance test (Volume 10) and a code-level enforcement point.

| Law | Statement | Enforcement point | Proof |
| --- | --- | --- | --- |
| 1 | One record, three faces: a single append-only ledger; patient, clinician and governance portals are authorised views, never copies | Ledger DDL, RLS policies (8.1, 8.3) | LED-03, LED-04 |
| 2 | The argument is the unit of decision: claim, grounds, warrant, backing, qualifier, rebuttals; nothing reaches a face that is not an argument | Orchestrator accepts only `ArgumentDraft`; faces read only `actual_argument` | ENG-02, single-gate negatives (5.6) |
| 3 | Uncertainty is typed and non-coercible: six signals (posterior, coverage, membership, reliability, fit, ignorance) as fixed-point values in separate types; no averaging or cross-kind comparison | `Fixed6` and signal types (4.3, 4.7) | ARG-01..03 compile-fail |
| 4 | Only arithmetic releases: a pure evaluator with five fixed stages assigns one of three verdicts (released, flagged, held); models propose, never release | Evaluator crate; verdict-class cap (5.4) | V-00..V-04, C-17 |
| 5 | Every input is pinned: eight pin classes by content hash on every attempt; replay reproduces the verdict byte for byte | `attempt.pins` NOT NULL; completeness check | LED-06, LED-07 |
| 6 | The compiler is the only door for knowledge: signed, versioned fragments admitted through eleven gates; hand edits impossible by construction | `GRANT INSERT ON pin_registry, generic_argument TO compiler` only | Gate fixtures (6.3) |
| 7 | Engines are pure functions of pinned inputs: no I/O, clock, or randomness; two-process purity harness | seccomp profile; harness | PUR-01..06, ENG-03 |
| 8 | Rendering cannot change meaning: three registers (clinician, patient, regulator); no register omits, adds or reorders a rebuttal or qualifier signal | Render-invariance property (9.3); class-U compiler gate | REN-01, REN-02 |
| 9 | Attention is budgeted, not begged: fixed number of interruptive items per encounter under a versioned suppression policy; suppressed items remain reachable and counted | Brief algorithm and suppression record (9.5, 9.6) | REN-05, REN-07 |
| 10 | Evaluation is adversarial and firewalled: continuous corruption engine; no test case, sealed envelope or feedback signal reaches training or knowledge except through the compiler | Zone label; compiler gate 1 | ADV-02 |

Four set-wide conventions also hold (compendium, "How to read"): every behaviour-governing number is a configured, versioned, signed value, never a code literal; released, flagged and held are the only states of decision support and only the evaluator assigns them; every learned-model output is a proposal until gated; every volume ends in a numbered acceptance-test table that is the contract with the delivery milestones.

## 6. Success metrics

Derived from Volume 1A.6 (instrumented benefits) and 1A.8 (horizon thresholds). Each is a Measure resource computed from ledger events, replayable (same period, same pins → identical MeasureReport hash, RPT-03). The compendium fixes how each baseline is captured but no baseline values exist yet; they are captured at cut-over.

| Id | Metric | Definition (numerator / denominator, source events) | Target (1A.8) | Baseline | Cadence |
| --- | --- | --- | --- | --- | --- |
| MET-01 | Coverage gap | Facts existing only in narrative / all facts, per fact type (1A.1) | ≤ 2% for problems, medications, allergies, results-follow-ups | Audit sample at cut-over {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-02 | Documentation time | Minutes from encounter finish to note-sign act / encounters; after-hours sign acts / all sign acts | Derived and captured through the Ketryx integration (the Ketryx interface in 03-opscon.md; OCR-02) {{TBD: value, set in Ketryx}} | Migration month {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Weekly |
| MET-03 | Missed follow-ups | Open-loop rate: orders past expected window without result act / orders; median time from result event to action act | Zero unrouted items > 24 h; unactioned age p95 < configured | Migration month {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Weekly |
| MET-04 | Prescribing safety | Held and flagged prescribing attempts with override / all; adverse-reaction facts detected per 1,000 prescriptions; prescriptions signed with unresolved discrepancy | Unresolved-discrepancy signs = 0; discrepancy median age < 24 h | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-05 | Deterioration lead time | First flagged deterioration attempt to escalation act; unplanned admissions per episode | Re-score latency p95 < 10 s; trajectory replay identical | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-06 | Register completeness | Narrative-plus-code members / manual-audit sample members | Derived and captured through the Ketryx integration (the Ketryx interface in 03-opscon.md; OCR-02) {{TBD: value, set in Ketryx}} | Audit sample at cut-over {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-07 | Advanced-practice scope use | Encounters completed within scope / encounters in prescriber settings; escalation packets with full context / escalations | Escalations with packet = 100% | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-08 | Grounded telehealth | Brief delivered before session join / sessions; re-contact within 72 h / sessions; clinician-rated preparedness | Brief-before-session ≥ 99% over a quarter | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-09 | Patient plan delivery | Patient-register summaries delivered within 24 h of sign-off / signed | ≥ 95% | {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Monthly |
| MET-10 | Dataset completeness | Exported fact count / ledger fact count for consented patients; identifier residuals on audit sample | ≥ 99%; zero residuals | {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Quarterly |
| MET-11 | Inbound triage | Triage latency; queue order by urgency | p95 under 5 s | {{TBD: baseline, captured at cut-over at the first site (deferred 25 Sep 2026)}} | Weekly |
| MET-12 | Equity visibility | Outcome measures stratified by SDOH fact presence, with imprecise-Dirichlet intervals | Published per quarter | First quarter | Quarterly |
| MET-13 | Evidence loop | Release-capable fragments with an adherence MeasureReport per quarter / all; attempts carrying the feedback-overlay pin / all | 100%; 100% | n/a | Quarterly |
| MET-14 | Front-door conversion and responsiveness (revision 2, 1A.6) | Leads reaching Converted / leads, by source and channel; response-clock breaches / leads; cost per acquired patient = entered campaign spend / conversions | Published per month; no target stated | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 15 Oct 2026)}} | Monthly |
| MET-15 | Non-attendance (revision 2, 1A.6) | No-show appointments / booked; no-shows rebooked within 7 d / no-shows | Published per week; the teardown's "up to 40%" reduction is a vendor claim, not a target (CST-18) | Migration month {{TBD: baseline, captured at cut-over at the first site (deferred 15 Oct 2026)}} | Weekly |
| MET-16 | Outreach closure (revision 2, 1A.6; measured once E3 operates, section 8.1) | Threads closed with a confirmed reply within the SLA / threads; unverified threads / breached threads | Published per month | Deferred with E3 | Monthly |
| MET-17 | Document intake accuracy (revision 2, 1A.6) | Fields accepted unchanged at review / fields reviewed, by document type; pages per hour | Published per month; 1,000 pages per hour sustained (1A.3 op 22) | First quarter {{TBD: baseline, captured at cut-over at the first site (deferred 15 Oct 2026)}} | Monthly |

## 7. Capabilities, prioritised

Derived from Volume 1A.2 (eighteen capability services) and 1A.8 / 11.5 (milestones). Verdict class fixes the ceiling of each output: class 1 deterministic may be released; class 2 (frozen model with declared error) reaches a person only as flagged or via a queue; class 3 (self-judgement, bounded generative loop) only via a queue. Pass/fail is the compendium's acceptance test. Priority: the first release is the Tier 3 profile (section 8.1), so class-1, class-2 and class-3 capabilities are all in scope for it; class-3 outputs reach a person only through a review queue. Build order remains M1 to M9 (11.5).

| Id | Capability | Service / class | Tier | Pass/fail (acceptance test) | Serves |
| --- | --- | --- | --- | --- | --- |
| CAP-01 | Clinical entity recognition | `lang-ner` (2) | 2 | NER-01 F1 ≥ declared on held-out practice notes by document type; per-subgroup report in pin | G-01 |
| CAP-02 | Assertion status | `lang-assert` (2) | 2 | AST-01 "no chest pain" → Absent; "mother had breast cancer" → FamilyMember; both excluded from present-problem queries | G-01 |
| CAP-03 | Relation extraction | `lang-rel` (2) | 2 | REL-01 "metformin 500 mg bd" → three relations; structured dose equals parser output | G-01 |
| CAP-04 | Terminology mapping and entity resolution | `lang-map` (2) + `terminology` (1) | 1 (terminology), 2 (mapping) | MAP-01 tier-3 binding caps draft at flagged; MAP-02 two documents' mentions resolve to one subject id | G-01 |
| CAP-05 | Temporal extraction | `lang-time` (2) | 2 | TIME-01 "for the past 3 weeks" on a note dated D → onset D−21d ± declared tolerance | G-01 |
| CAP-06 | Document classification and routing | `lang-classify` (2) + routing rules (1) | 1 (rules), 2 (classifier) | CLS-01 discharge summary classified and routed to reconciliation queue; low reliability → human classification queue | G-06 |
| CAP-07 | Clinical phenotyping | `phenotype` (1) | 1 | PHE-01 definition using an Absent fact never matches; PHE-02 membership replayable | G-03, G-09 |
| CAP-08 | Risk stratification | `risk-*` (2, conformal-wrapped) | 2 | RISK-01 output never exceeds flagged; RISK-02 evidence list equals facts consumed | G-02 |
| CAP-09 | Adverse-event and safety-signal detection | `lang-ae` (2) | 2 | AE-01 detected reaction becomes flagged ground on next prescribing check of that class | G-05 |
| CAP-10 | Social determinants extraction | `lang-sdoh` (2) | 2 | SDOH-01 fact shown "from note" until confirmed; excluded from measures below floor | MET-12 |
| CAP-11 | Patient-voice and sentiment | `lang-voice` (2) | 2 | VOICE-01 output routes to triage lane only; cannot create a condition fact | G-06 |
| CAP-12 | Summarisation | `gen-summary` (3, bounded loop) | 3 | SUM-01 sentence without a fact citation fails the fidelity tester; SUM-02 three failures → no draft | G-04 |
| CAP-13 | Question answering over the record | `gen-qa` (3) + `facts` search (1) | 3 | QA-01 answer cites facts only; QA-02 "last eGFR" returns the observation version and span | G-04 |
| CAP-14 | De-identification | `deid` (2 text, 1 structured) | 1 (structured), 2 (text) | DEID-01 export type cannot hold identifier fields; DEID-02 residual identifier rate on adjudicated set below declared | G-09 |
| CAP-15 | Trial and pathway matching | `match` (1) | 1 | MATCH-01 unknown criterion → Fit Unknown → flagged, never released | G-02 |
| CAP-16 | Multimodal ingestion | `inbound` OCR/layout (2), waveform promotion (1) | 1 (rules), 2 (OCR) | MM-01 OCR block below reliability floor excluded from facts; MM-02 promotion rule replayable | G-01, G-06 |
| CAP-17 | Domain packs | Configuration of CAP-01..16 by locale/specialty fragments | 1 | PACK-01 switching pack changes only pins K/I; engine pins unchanged | G-03 |
| CAP-18 | Workflow embedding | `orchestrator` + faces | 1 | WF-01 every rendered item has an argument id and attempt id in its response headers | G-02, G-04 |
| CAP-20 | Real-time voice-to-voice patient interaction for pre-intake, check-ins and messages, using a self-hosted voice model whose weights are content-hash pinned (examples stated: Fish Audio); runs under the Volume 7.5 bounded loop and writes only questionnaire responses and communications with dialogue spans (minted here, stated 25 Sep 2026; CCR-02) | `voice` sidecar (3) | 3 | Scope test as for the typed pre-intake agent (Volume 3A.11): cannot write anything but QuestionnaireResponse; no recording without a consent resource (Volume 3A.11 telehealth tests); {{TBD: acceptance test for turn latency and transcript fidelity, phase 4}} | G-04, G-08; risk 9 in 02-conops.md |
| CAP-19 | Prospective study machinery: StudyDefinition, prospective enrolment on phenotype match with consent scope, sealed envelopes, evaluation register, measure validation, findings-to-change flow (minted here from Volumes 2A, 3A.10 and 10.4) | `reporting::studies` (1), sealed envelopes (1) | 1 | ST-01 enrolment occurs on match event and is refused without consent scope; ST-02 interim reads cannot alter the sealed plan; ST-03 pin change creates a revalidation task; RE-01 fragment without evaluation-register entry refused; RE-02 every ratified change links to a prior MeasureReport and a follow-up study; ADV-03 | G-10 |
| CAP-21 | Lead and engagement rules: response-clock state, stage transitions, follow-through step due, per-factor contributions as separate typed outputs, never a summed score (revision 2; Volume 1A.2 row 21; 3A.2 A6, A7; D-12) | `engage` (1) | 1 | LEAD-01 clinical risk tier absent from every engagement rule input; LEAD-02 two leads with identical factors yield identical outputs; LEAD-03 breached clock creates a Task and a signal row; LEAD-05 no score column or composite field; LEAD-06 opt-out on one channel blocks every channel; LEAD-07 conversion carries responses with source lead-intake; LEAD-08 import dry run reports duplicates; CAMP-01, CAMP-02, CAMP-03, CAMP-04, CAMP-05 (A7) | MET-14, MET-15 |
| CAP-22 | Conversation intent, urgency and tone from the ratified taxonomy (D-21), each with reliability; routing target from a rule fragment; outbound PHI check (revision 2; 1A.2 row 22; 3A.11 J4; 9.8) | `lang-intent` (2) + routing rules (1) | 1 (rules, PHI check), 2 (classifier) | OMNI-01 possible-emergency intent routes to the critical lane under 100 ms; OMNI-02 distressed and negative tone distinguished on the sealed set; OMNI-03 free-form WhatsApp outside 24 h refused; OMNI-04 record number blocks the send with no override; OMNI-05 partial match goes to reconciliation and no Patient is created; OMNI-06 unknown sender's mention becomes a provisional fact with span; OMNI-07 class-1 red-flag floor fires when the classifier says low; OMNI-08, OMNI-09, OMNI-10 (2A.1 transports); REN-08, REN-09, REN-10, REN-11 (9.8) | G-06, MET-11 |
| CAP-23 | Telephony voice line: inbound and outbound calls, IVR floor, booking through class-1 scheduling, designed check-ins, after-hours answering, message taking, hand-off (revision 2; 1A.2 row 23; 3A.11 J5; extends CAP-20) | `voiceline` sidecar (ASR 2, dialogue 3, synthesis 2) + scheduling rules (1) | 1 (IVR, booking), 2 (ASR, synthesis), 3 (dialogue) | VOX-01 a call writes nothing clinical beyond patient-reported Observation, QuestionnaireResponse, Communication and Appointment transitions; VOX-02 hand-off cue reaches a person within one turn; VOX-03 a clinical question is never answered and an emergency keyword speaks the guidance fragment; VOX-04 no accepted consent prompt means no audio stored; VOX-05 identity confirmation precedes any patient-specific action; VOX-06 a spoken statement about a result traces to a released, signed argument | G-04, G-08, MET-15 |
| CAP-24 | Form definition and FHIR binding: typed fields, fifteen conditional operators, fixed-point formulas, every item bound to a FHIRPath target, versioned publication through the compiler (revision 2; 1A.2 row 24; 3A.9 H4) | `forms` (1) | 1 | FRM-01 every field in a shipped form has a binding; FRM-02 a formula field equals the calculator fragment output; FRM-03 rule outcome identical client and server; FRM-04 submit yields one transaction Bundle with provenance and spans; FRM-05 a binding to a non-existent FHIRPath fails compile gate 1; FRM-06 a response renders against its original pin after republication | G-01, G-08 |
| CAP-25 | Document intake at volume: archives, fax streams, handwriting, per-block and per-field reliability, review queue for low-reliability fields, resumable idempotent batches (revision 2; 1A.2 row 25; 3A.7 F5; extends CAP-16) | `docai` (OCR, layout, handwriting 2; batch orchestration 1) | 1 (batch control), 2 (recognition) | DAI-01 a field below floor never becomes a fact without a review act; DAI-02 a 1,000-page batch is resumable and idempotent; DAI-03 handwriting engine registered with its own benchmark and pin; DAI-04 an extracted critical laboratory value fires the critical lane; DAI-05 split reliability below floor sends the item to a manual split queue | G-01, G-06, MET-17 |
| CAP-26 | Tokenisation: deterministic HMAC tokens per identifier class with keys in a customer-owned vault; re-identification only through the vault under a recorded authority act (revision 2; 1A.2 row 26; 3A.12b L2; 12.4; D-16; deferred from the first release, section 8.1) | `tokenise` (1) | 1 | DPG-01 same identifier and key yield the same token across two exports; DPG-02 no token reverses without the vault; DPG-03 re-identification without an authority act returns 403 and writes an audit row; DPG-04 zero identifiers in logs on the synthetic run; DPG-05 analytics export holds only tokens; DPG-06 old tokens resolve after key rotation | G-09 |
| CAP-27 | Plain-language analytics query: a drafted query over declarative views shown verbatim with its term mappings, executed only after a confirming act (revision 2; 1A.2 row 27; 3A.10 I3; 12.6; deferred from the first release) | `gen-sql` (3) + view engine (1) | 1 (views), 3 (drafter) | ANA-01 a generated query never executes without an act; ANA-02 result rows carry lineage; ANA-03 a tile bound to an unpublished query is refused; ANA-04 the term mapping is shown and pinned; ANA-05 governance drill returns aggregates without break-glass | G-09 |
| CAP-28 | Cost and margin attribution with leakage flags and pre-submission claim check (revision 2; 1A.2 row 28; 3A.8 G4; deferred from the first release) | `cost` (1) | 1 | MRG-01 margin recomputed identically on replay; MRG-02 every leakage flag names its rule pin; MRG-03 the pre-check blocks a line whose note is unsigned; MRG-04 the margin view returns 403 to clinician and patient roles | NG-05 (no composite); MET-02 |

The twenty-four runtime operations (Volume 1A.3; operations 18 to 24 folded in at revision 2), the six setting profiles (1A.4; the front-office profile added at revision 2) and the layer-to-crate map (1A.5, with the ten crates added at revision 2 in 3A.1) are the phase-3 and phase-4 derivations of this table and are not restated here. Revision 2 also augments existing capabilities without new identifiers: the ambient capture review surface, five note types and co-sign (2A.2, 3A.3 B1; AMB-01, AMB-02, AMB-03, AMB-04, AMB-05) under CAP-12 and CAP-18; public booking and no-show recovery (3A.2 A4) and remote-monitoring programme fragments (3A.11 J3) under CAP-18; record search (3A.3 B9), panel worklist (2A.3, 3A.6 E3), surveys (J6), the HITH census board (J7), the composer (12.7) and the body map (12.8) are modules listed in section 8.1.

## 8. Release boundary

Derived from Volume 11.2 (tier manifests) and 11.5 (delivery plan). The compendium fixes the build order and the tier contents but does not name the first version a real user adopts.

| Tier | Contents | Excluded at build | Regulatory posture |
| --- | --- | --- | --- |
| Tier 1 — Record and workflow | Spine, ledger, faces, terminology, orders, inbound, deterministic rule engine (class 1 only) | All class-2 and class-3 engines; conformal wrapper; generative loop | Clinical information system; no diagnostic claim |
| Tier 2 — Decision support | Tier 1 plus class-2 engines under conformal wrapper, fit engine, attention layer, corruption engine, regulator bundle | Generative loop | Software as a medical device, decision-support class; flagged-only for class 2 |
| Tier 3 — General-purpose assistant | Tier 2 plus bounded generative loop and class-3 queues | Nothing; permitted-prompt whitelist is signed configuration (D-06) | Highest class; class-3 never a control |

Fold-in placement at revision 2 (D-20, Volume 11.2): the fifteen revision 2 modules A6, A7, B9, E3 (rules), F5 (batch control), G4, H4, I3 (dashboards), J4 (queue and routing), J5 (IVR floor), J6, J7, L1, L2 and L3 ship in Tier 1; the intent classifier, OCR at volume and the remote-monitoring risk programmes are class 2 and ship in Tier 2; voice-line dialogue, drafted outreach text, campaign copy and analytics query drafting are class 3 and ship only in Tier 3. The first release is Tier 3, so the build contains all of them; which are operated at the first release is stated in section 8.1.

Build order: M1 argument and fixed-point crates → M2 evaluator → M3 ledger → M4 compiler and registry → M5 spine functions → M6 Tier 1 engines → M7 faces and rendering → M8 governance → M9 Tier 2 and 3 engines. M5 is complete only when every Volume 3A module ships and parity suite E2E-01 to E2E-12 passes. Fold-in milestones (revision 2, Volume 11.5): M4 adds the eleven fragment classes of 6.9 (engagement loop, profile, phenotype definition, form definition, routing rule, channel template, pattern set, tokenisation policy, brand pack, cost schedule, contract) with a rejecting fixture each; M5 adds the Tier 1 modules and the parity scenarios E2E-14, E2E-15 (IVR path), E2E-17, E2E-18 (review path), E2E-20 and E2E-21; M7 adds the front-office aperture, the desk and voice-line consoles, the form designer, the dashboard designer and the body map; M8 adds the tokenisation gateway, the synthetic cohort generator and E2E-19; M9 adds the class-2 classifiers and the class-3 dialogue, drafting and query drafting, completing E2E-16.

### 8.1 First adoptable version (stated 25 Sep 2026)

| Item | Decision |
| --- | --- |
| Settings | Telehealth and hospital in the home |
| Workforce | General practitioners, nurse prescribers and pharmacist prescribers operating those two settings, each under their scope-of-practice profile (1A.4) |
| Tier | Tier 3 — general-purpose assistant (ruled 25 Sep 2026 on CCR-02, superseding the earlier Tier 2 and Tier 1 options, so that voice interaction ships from day one; the loss-matrix ratification of D-05 and the New Zealand sponsor and WAND obligations of CST-03 are first-release gates; the D-06 permitted-prompt whitelist is first-release signed configuration) |
| Site | Site agnostic; no reference site named |
| Jurisdictions | New Zealand (Medsafe) first, Australia (TGA) second, possibly the United States (FDA) third (OCR-01, 25 Sep 2026) |
| Launch shape (strategy, stated 25 Sep 2026) | Small launch. Prospective studies (CAP-19) run concurrently with operations from day one. Reasoning: a prospective study validates the system, supports iterative development cycles, and allows user-group feedback, so a body of research evolves alongside the demonstration of safety and efficacy (G-10) |
| Jurisdiction order | New Zealand under Medsafe first, as a first approval before new legislation closes the current regulatory window (CST-12); Australia under the TGA second |
| Explicit exclusions | None stated; the Tier 3 manifest excludes nothing at build (11.2) |
| Revision 2 modules operated at the first release (stated 15 Oct 2026) | In: A6 intake pipeline and lead register, A7 campaigns and follow-through, J4 omnichannel desk, J5 voice line, H4 form designer, F5 document intake at volume, together with the front-office setting profile (1A.4), the front-office aperture (2A.0), the two front-door engagement loops (2A.1), channel templates and the outbound PHI check (9.8), the ambient capture review surface (2A.2) and public booking and no-show recovery (3A.2 A4). Deferred from first-release operation, built per D-20 and present in the Tier 3 build: B9 record search, E3 panel worklist and outreach SLA, G4 cost and margin, I3 analytics studio, J6 surveys, J7 HITH census board, L1 tenancy and brand packs, L2 tokenisation gateway, L3 developer platform, the composer (12.7), the body map and projection arguments (12.8) and the overlay deployment posture (11.6; the first release is the system of record). Deferred modules take no operating role, staffing or baseline at the first release; they are activated by a later release decision |

### 8.2 What Tier 3 leaves in for those settings (derived)

Derived by applying the Tier 3 manifest (11.2), which excludes nothing at build, to the operations each setting weights (1A.4) and the engine class of each operation (1A.3). Class-1 outputs may be released; class-2 outputs reach a person only as flagged, under the conformal wrapper, with a validation report in the engine pin; class-3 outputs (bounded generative loop, Volume 7.5) reach a person only through a review queue and are never a control. The pre-intake conversational agent and the voice agent (CAP-20) are class 3 (CCR-01, CCR-02).

| Operation (1A.3) | Telehealth | HITH | In the first release | Class ceiling |
| --- | --- | --- | --- | --- |
| 1 Record pre-read and brief | yes | yes | Brief assembler; `gen-summary` summary draft as a queued item | Brief released; summary queue |
| 2 Ambient transcription and live extraction | yes | yes | ASR and language services 1 to 5; session facts excluded from grounds until note signed | Facts only |
| 3 Working differential and next-best-question | yes | no | Bayesian differential and EIG question ordering, flagged "consider" with rebuttals (D-09) | Flagged |
| 6 Inline record Q&A | yes | no | `facts` search and `gen-qa` answers citing facts | Queue |
| 7 Note, orders, letters, patient summary drafting | no | yes | Order builder from signed facts; `gen-summary` drafts, unsigned | Queue; sign-off act per item |
| 9 Follow-up task generation | no | yes | Whole operation | Released |
| 10 Inbound document triage | no | yes | Classifier, routing rules, summary | Summary queue; routing released |
| 12 Message triage | yes | no | `lang-voice` urgency and distress, red-flag rules, suggested response draft | Lane released; response queue |
| 13 Continuous risk re-scoring | yes | yes | `risk-*` engines under conformal wrapper; HITH deterioration, sepsis and readmission engines; daily trajectory | Flagged |
| 16 Quality and safety analytics | no | yes | Whole operation | Reports |
| Pre-intake (Volume 2A.1) | yes | yes | Conversational agent, typed or by voice (CAP-20), writing questionnaire responses with dialogue spans; pre-intake summary as a queued argument | Queue |
| 18 Lead intake and follow-through (revision 2; front-office profile) | yes | yes | `engage` rules (CAP-21); drafted outreach text as a queue item; Communication on send | Rule outputs released; drafted text queue-only |
| 19 Omnichannel conversation triage (revision 2; front-office profile) | yes | yes | `lang-intent`, routing rules and red-flag rules (CAP-22); one queue over WhatsApp, SMS, email and call records | Lane released; classification strip flagged |
| 20 Voice line call handling (revision 2; front-office profile) | yes | yes | `voiceline` (CAP-23): IVR, booking, check-ins, after-hours answering, hand-off | Bookings released through class-1 rules; dialogue queue-class |
| 21 Campaign generation (revision 2; front-office profile) | yes | yes | `gen-summary` over a typed brief; claims-boundary lint (CAP-21, A7) | Queue-class; publishes only through the compiler |
| 22 Document batch intake (revision 2) | no | yes | `docai` (CAP-25) with services 1 to 6 and routing rules; field review queue | Facts above floor released; below floor queue only |
| 23 Panel worklist and outreach (revision 2) | deferred | deferred | Not operated at the first release (E3, section 8.1) | Rows render exactly the verdict class |
| 24 Cost attribution (revision 2) | deferred | deferred | Not operated at the first release (G4, section 8.1) | Released (class 1); never on the patient face |

Consequence: the first release carries the whole platform for the two settings, including the generative loop and class-3 queues, with the permitted-prompt whitelist as signed configuration (D-06). Every class-2 engine needs a validation report in its pin (1A.7) and every class-3 output passes the class-2 testers of the bounded loop before it is queued.

Capabilities in scope for this release: CAP-01 to CAP-25 (CAP-21 to CAP-25 added 15 Oct 2026); CAP-26, CAP-27 and CAP-28 are built per D-20 and deferred from operation with L2, I3 and G4. The research path through CAP-07 (cohorts), CAP-15 (enrolment), CAP-14 (extracts) and CAP-19 is a first-launch item because of G-10; de-identification (CAP-14) remains the export path until the tokenisation gateway (CAP-26) operates.

### 8.3 Claim types in the first release (stated 25 Sep 2026)

The closed vocabulary for the set is the union of Volume 4.2 (diagnosis, prescribing, referral, recall, coding proposal, pre-intake summary, patient message), the types used in Volumes 1A, 7, 7.4 and 10 (risk, safety-signal, differential, eligibility, suppression, gather_information, pre-intake question) and, from revision 2, `projection` (Volume 12.8: a flagged class-2 argument answering a hypothetical, never released and never acted on); see change request CR-01 as amended by CCR-04 and on 15 Oct 2026. No separate engagement or outreach claim type exists (ruled 15 Oct 2026): lead and engagement rules run outside the evaluator in the lead compartment (3A.2 A6), and outreach reuses recall, eligibility, gather_information and patient message (2A.3). The first release ships these ten, each needing a ratified loss matrix (D-05, CST-10) and a compiled template before go-live:

| Claim type | Drafted by (1A.2, 1A.3) | Settings |
| --- | --- | --- |
| prescribing | Rule engine, operation 4 | Telehealth, HITH |
| differential | Bayesian differential, operation 3 | Telehealth |
| risk (deterioration, sepsis, readmission) | `risk-*` engines, operation 13 | HITH, telehealth |
| safety-signal | `lang-ae`, CAP-09 | Both |
| pre-intake summary | Pre-intake agent (Volume 2A) | Telehealth |
| recall | Recall rules, operation 15 | HITH |
| gather_information | Abstention render (Volume 4A), class 1 | Both |
| suppression | Governed suppression rule (Volume 9.6) | Both |
| patient message (confirmed 25 Sep 2026) | `lang-voice` triage and the class-3 suggested-response draft, operation 12; patient-facing engagement-loop messages (Volume 2.2); class 3 for drafted content, class 1 for rule-driven reminders | Telehealth, HITH |
| eligibility (confirmed 25 Sep 2026) | `match` engine, CAP-15, operation 14; class 1; released only when Fit In and all criteria met, else flagged | Both; drives prospective enrolment (CAP-19) and pathway matching |

Out of the first release: diagnosis, referral, coding proposal, projection (12.8; deferred with the body map, section 8.1).

Order of priority if further claim types are added, judged by G-10 and the release settings:

| Order | Claim type | Why here | Class |
| --- | --- | --- | --- |
| 1 | eligibility | Prospective enrolment on phenotype match is the recruitment mechanism for every study; without it studies use fixed id lists only | 1 |
| 2 | referral | Telehealth hand-back packet and HITH discharge-to-GP handover are referral-shaped acts; rule-driven | 1 |
| 3 | coding proposal | Closes the coverage gap (MET-01) and register completeness (MET-06), which are study endpoints | 2 |
| 4 | diagnosis | Highest regulatory weight; nothing in the first-launch settings needs a released diagnosis claim | 2 |
| 5 | projection | What-If projections for the clinician face only (12.8); capped at flagged; no downstream resource; needs its own loss matrix and validation report | 2 |

Milestones: the first release requires M1 to M9 complete, with M9 delivering the Bayesian, conformal-wrapper and extractor engines, the bounded generative loop and the voice sidecar (CAP-20) in the Tier 3 build.

## 9. Constraints and their sources

Derived from Volume 13.1 and 11.3, 11.4.

| Id | Constraint | Source |
| --- | --- | --- |
| CST-01 | Core language is Rust for ledger, evaluator, argument types, terminology and render; `#![forbid(unsafe_code)]` in evaluator and argument crates; `cargo deny` bans float-math crates from the evaluator | D-01; Volume 11.3 |
| CST-02 | Regulatory profiles are build-time exclusions with a signed manifest (build hash, features, crate hashes, sidecar digests, SBOM, seccomp profiles, pin classes) | Volume 11.1, 11.2 |
| CST-03 | New Zealand (first): under the Medicines Act 1981 there is no pre-market approval or classification to confirm; a New Zealand sponsor is appointed, the device is notified in Medsafe's WAND database within 30 days, evidence of safety for intended purpose is held, and post-market obligations (complaints, adverse events, recalls, changes) are met. These gate the first release. Australia (second): device classification per tier as D-11 states, confirmed with the TGA; Tier 3 is the highest class. United States (possible third, stated 25 Sep 2026): FDA classification as a compliance item, captured through the Ketryx integration. The Medical Products Bill, once commenced, will regulate software as a medical device including AI for a therapeutic purpose in New Zealand | D-11 as amended by CCR-03; section 8.1; 02-conops.md section 5 |
| CST-04 | Terminology edition pinned to the current national edition for the jurisdiction in force: New Zealand first, then Australia; licence recorded in the obligations register | D-07; stated 25 Sep 2026 |
| CST-05 | Sidecars (JVM rule engine, Bayesian/conformal, extractor, generative) run as separate seccomp-wrapped processes, no network namespace, stdin/stdout only, killed on any denied syscall | Volume 11.3 |
| CST-06 | Store is PostgreSQL 16 with row-level security per role; ledger schema insert-only; store-level encryption plus per-patient hash chain and Merkle anchor | Volume 11.3, 11.4 |
| CST-07 | Identity per face; professional tokens bind registration number and scope-of-practice profile; mTLS between faces and gateway; break-glass requires reason, writes an act, sentinel entry | Volume 11.4 |
| CST-08 | No clinical behaviour depends on any secret; secrets only for transport and signing keys in a hardware-backed store | Volume 11.4 |
| CST-09 | Provisional (unratified) templates may reach flagged but never released | D-02 |
| CST-10 | Loss matrices per claim type must be ratified by clinical governance before Tier 2; the first release is Tier 3, which contains Tier 2, so ratification for every claim type it ships gates it | D-05; section 8.1 |
| CST-11 | Edge node is the Rust core compiled to WASM with an embedded store, additive sync | Volume 11.3, Volume 3.6 |
| CST-13 | Voice interaction uses a self-hosted voice model whose weights are content-hash pinned (pin class W), so that Laws 5 and 7 hold; a vendor-hosted voice API is not acceptable. Examples stated: Fish Audio | Stated 25 Sep 2026; 02-conops.md open questions |
| CST-12 | Timeline: as fast as possible, driven by a closing window of regulatory opportunity in New Zealand: the Medical Products Bill (replacing the Medicines Act 1981) will regulate software as a medical device including AI for a therapeutic purpose; the Government intends to introduce it in 2026 with commencement around 2030 and a longer transition for many devices (Cabinet decisions to 7 April 2026). The window closes at commencement. No fixed date, budget or partner commitment stated. Commercial constraints: none stated | Ken Lee, 25 Sep 2026 |
| CST-14 | Tenancy: every resource, fact, lead, attempt and act carries a tenant and a project; row-level security and attribute-based access evaluate both; a module subset for a tenant is a profile manifest difference recorded in the build manifest, never a runtime toggle of clinical behaviour; brand packs are class U fragments under the claims-boundary lint (revision 2; applies from the first release even though L1 partner tenancy is deferred) | Volume 3A.12b L1, 11.8; D-17 |
| CST-15 | Tokenisation boundary: analytics, evaluation-zone work, research export and any authoring-time hosted-model proposer receive identifiers only as deterministic tokens produced inside the tenant trust boundary with keys in a customer-owned vault; re-identification needs a recorded authority act and is never cached or batched. Until the gateway (L2) operates, the de-identification engine (CAP-14) with type-level identifier exclusion is the only export path (revision 2) | Volume 12.4, 3A.12b L2; D-16 |
| CST-16 | Hosting posture and in-region inference: every model sidecar runs inside the chosen hosting posture (managed cloud, private cloud, on-premise, air-gapped) and no model call crosses the trust boundary; a hosted model, including one under tenant-supplied keys, never runs on the release path in any engine, tester or renderer and may serve only as an authoring-time proposer whose outputs enter review queues (revision 2) | Volume 11.7, 11.9; D-19; CST-13 generalised |
| CST-17 | Messaging and telephony providers: WhatsApp Business and telephony (SIP or hosted) are reached only through adapter traits; provider agreements, template approvals, data-processing terms and a residency statement are recorded in the obligations register before the channel operates; the WhatsApp 24-hour window and provider-approved template rule bind every loop (revision 2) | Volume 3A.11 J4, J5; 10.8; D-14, D-15 |
| CST-18 | Vendor figures quoted from the Care Execution Platform teardown (reminders cutting no-shows "by up to 40%", remote monitoring revenue, language and field-type counts) are claims, never baselines or targets; every baseline in this set is captured at cut-over (revision 2) | Compendium "How to read", 1A.6; 13.4 |

## 10. Decisions already taken

Carried verbatim from Volume 13.1.

| Id | Decision | Default in the compendium | Owner | Affects volumes |
| --- | --- | --- | --- | --- |
| D-01 | Core language: Rust for ledger, evaluator, argument types, terminology, render | Adopted | Architecture | 4, 5, 8, 11 |
| D-02 | Provisional templates (not yet ratified) may reach flagged but never released | Adopted | Clinical governance | 5, 6 |
| D-03 | Qualifier shape: six typed signals including ignorance | Adopted; supersedes any earlier five-signal or set-based shape | Architecture | 4 |
| D-04 | Conflict predicate vocabulary (contradicts, excludes, supersedes, duplicates, interacts) | Provisional list; closed once ratified | Clinical governance | 5, 8 |
| D-05 | Loss matrices per claim type | Placeholder matrices ship; ratification required before Tier 2 | Clinical governance | 5 |
| D-06 | Tier 3 prompt whitelist as signed configuration, not build feature | Adopted | Architecture | 7, 11 |
| D-07 | Terminology edition pin and licence for the jurisdiction | Pin the current national edition; licence recorded in obligations | Compliance | 6, 12 |
| D-08 | External Merkle anchoring mechanism | Publish root to an independent append-only log with a receipt; exact provider open | Architecture | 8 |
| D-09 | Live differential during encounter versus synthesis before | Synthesis before; live differential only as pre-intake question ordering | Clinical governance | 7, 9 |
| D-10 | Severity tier vocabulary (four tiers) | Provisional | Clinical governance | 9 |
| D-11 | Regulatory assumptions requiring confirmation (device classification per tier) | Tier 1 not a device; Tier 2 decision-support class; Tier 3 highest | Compliance | 11 |
| D-12 | Lead and engagement scoring shape | Per-factor typed rule outputs rendered as chips; no stored or displayed composite; queues ordered by response clock and stage | Architecture; clinical governance for any factor drawn from coverage or billing bands | 1A, 3A |
| D-13 | Overlay deployment posture | Adopted as a second profile with incumbent snapshots pinned by content hash; not operated at the first release (section 8.1); demand confirmed before the incumbent snapshot path is built | Architecture | 11 |
| D-14 | WhatsApp Business provider and coexistence mode | Adapter trait; provider open. Owner platform operator; selected and coexistence capability recorded before M5 (13.2; confirmed 15 Oct 2026) | Platform operator | 3A, 9 |
| D-15 | Telephony provider (SIP or hosted) and warm-transfer support | Adapter trait; provider open. Owner platform operator; selected and warm-transfer capability recorded before M5 (13.2; confirmed 15 Oct 2026) | Platform operator | 3A |
| D-16 | Tokenisation key custody | Customer-owned vault, HSM or tenant KMS; rotation cadence open. Owners compliance and architecture; decided before M8, or before the release that operates L2 if later (13.2; confirmed 15 Oct 2026) | Compliance; architecture | 12 |
| D-17 | White-label, reseller and pricing terms | Outside this compendium; usage meters provided as Measures | Product | 3A, 11 |
| D-18 | Theatre scheduling and inpatient bed management | Not adopted: outside the intended purpose (primary care, telehealth, hospital in the home); the HITH census board is adopted instead | Product; clinical governance | 3A |
| D-19 | Bring-your-own hosted model keys | Authoring-time proposers only; never on the release path | Architecture | 11 |
| D-20 | Tier placement of the revision 2 capabilities | Class-1 modules in Tier 1; classifiers and OCR at volume in Tier 2; dialogue, drafting and query drafting in Tier 3 | Architecture; compliance | 11 |
| D-21 | Intent taxonomy, urgency bands and tone classes | Twelve intents as shipped from the teardown's list; ratified as a codebook before M7 | Clinical governance | 3A, 6 |

## 11. Change requests to upstream

| Id | Target document | Target item | Change |
| --- | --- | --- | --- |
| CR-01 | Mākoha Design Compendium | Volume 4.2, Claim row (closed vocabulary) | The closed vocabulary lists diagnosis, prescribing, referral, recall, coding proposal, pre-intake summary, patient message, while Volumes 1A, 7, 4A and 9 also use risk, safety-signal, differential, eligibility, gather_information, suppression and (7.4) pre-intake question. Close the vocabulary as the union of the two lists, or state which list governs. This PRD builds to the union. Amended 25 Sep 2026 by CCR-04. Amended 15 Oct 2026: revision 2 adds `projection` (Volume 12.8) to the union; no engagement or outreach claim type is added (section 8.3). Still open against the compendium (carried as an approvals condition). |
| CR-02 | Mākoha Design Compendium | Volume 13.2, open item "Raise a change request against the phase set (01-prd.md and downstream)" | Discharged by this revision of 15 Oct 2026: capabilities 21 to 28, operations 18 to 24, the front-office role and the tenancy and tokenisation constraints are minted here and carried downstream. Tick the item at the next compendium revision. |

## 12. Assumptions

Seeded from the provisional rows of Volume 13.1 and the compendium's own conventions.

| Assumption | Confidence | How it would be checked |
| --- | --- | --- |
| Device classification per tier as stated in D-11 holds in the target jurisdiction | Low | Regulator confirmation (13.2 open item) |
| The national terminology edition can be licensed and pinned for the jurisdiction (D-07) | Medium | Licence obtained and recorded in the obligations register |
| Loss matrices for every first-release claim type can be ratified by clinical governance before go-live (D-05), given the first release is Tier 3 | Low | Ratification acts recorded as signed fragments through the compiler (gate 11) before the Tier 2 build is cut |
| A 10,000-patient synthetic practice is representative enough for Volume 3 latency budgets | Medium | Parity suite E2E-01..12 and budget tests on the synthetic set, then re-run on first live data |
| An independent append-only log with a receipt format exists for Merkle anchoring (D-08) | Medium | Provider selected and receipt format recorded |
| Baselines for MET-01..11 can be captured at cut-over from the incumbent system | Medium; depends on the incumbent system at the first site, which is unknown (site agnostic) | Audit sample and migration-month measures |
| The first launch can be notified in WAND and operating before the Medical Products Bill commences (around 2030) | Medium; introduction intended 2026, commencement stated as around 2030, transition period expected | Bill progress tracked against the M1 to M9 plan; reviewed at every milestone exit |
| Targets for MET-02 and MET-06 can be derived and captured through the Ketryx integration | Medium (scope confirmed 25 Sep 2026) | Targets recorded in Ketryx and quoted back here |
| A WhatsApp Business provider offering coexistence mode on the practice's existing number, and a telephony provider with warm transfer, are available in New Zealand under acceptable data-processing terms (D-14, D-15) | Medium | Providers selected and terms recorded in the obligations register before M5 |
| Front-office staff can operate the restricted clinician aperture without a professional registration, under the practice's own identity provider | High | 1A.4 front-office profile tests; identity binding at onboarding (phase 3 onboarding mode) |
| The twelve-intent taxonomy shipped from the teardown is adequate for New Zealand telehealth and HITH enquiries until ratified (D-21) | Medium | Clinical governance ratifies the codebook before M7; misrouting measured in the channel surveillance signals |

## 13. Open questions

Seeded from Volume 13.2; PRD questions added.

- [ ] Ratify loss matrices for the first five claim types (D-05)
- [ ] Close the conflict predicate vocabulary (D-04)
- [ ] Select the external anchor provider and record its receipt format (D-08)
- [ ] Confirm device classification per tier with the regulator (D-11)
- [ ] Publish the first threshold set and codebooks through the compiler before M6
- [ ] Produce the 10,000-patient synthetic practice for the performance suite before M5
- [x] First adoptable version: telehealth and HITH, GP plus nurse and pharmacist prescriber workforce, Tier 3, site agnostic (section 8.1; revised from Tier 2 on 25 Sep 2026)
- [x] Patient message included as the tenth first-release claim type (section 8.3, 25 Sep 2026)
- [ ] Whether the chosen self-hosted voice model is a native full-duplex speech-to-speech model or the capability is composed from speech recognition, a text engine and speech synthesis; decided in phase 4 (CST-13)
- [x] Claim types for the first release: the ten in section 8.3
- [x] Jurisdiction and regulator: New Zealand and Medsafe first, then Australia and the TGA (CST-03)
- [x] New Zealand billing scope: private billing, no claiming gateway in the first release (OCR-03)
- [ ] Baseline values for MET-01 to MET-11: deferred until the first site; captured at cut-over (section 6)
- [x] Commercial and timeline constraints: as fast as possible, none other (CST-12)
- [x] The New Zealand regulatory window closes at commencement of the Medical Products Bill, around 2030 (CST-12, revised 25 Sep 2026)
- [ ] Track the bill's progress so the launch date can be set against it; owner {{TBD: who tracks the bill (deferred)}}
- [x] Eligibility confirmed as the ninth first-release claim type (section 8.3)
- [x] Intended purpose confirmed unchanged; launch strategy recorded as detail in section 8.1
- [x] Ketryx integration: greenfield capture of applicable standards for TGA and possibly FDA applications; MET-02 and MET-06 targets captured there (OCR-02)
- [x] Revision 2 modules operated at the first release: A6, A7, J4, J5, H4, F5 with the front-office profile; the rest built per D-20 and deferred (section 8.1, 15 Oct 2026)
- [x] `projection` added to the CR-01 union; no engagement or outreach claim type (section 8.3, 15 Oct 2026)
- [x] D-14 to D-16 owners and milestones: compendium roles and dates carried; named holders remain under the approvals conditions that name role holders (section 10, 15 Oct 2026)
- [ ] Ratify the intent taxonomy codebook and the default routing rules (D-21) before M7
- [ ] Select the WhatsApp and telephony providers and record coexistence and warm-transfer capability (D-14, D-15) before M5
- [ ] Decide the tokenisation vault type and rotation cadence (D-16) before M8
- [ ] Confirm demand for the overlay posture before building the incumbent snapshot path (D-13)
- [ ] Baseline values for MET-14, MET-15 and MET-17: captured at cut-over (section 6)
