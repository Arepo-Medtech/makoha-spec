---
docpipe: 1
phase: 2
title: Concept of Operations
status: final
version: 2.0
upstream: ["00-idea.md", "01-prd.md"]
upstream_hash: {"00-idea.md": "0e9f1f8a3d5668f2", "01-prd.md": "0e34202c06cdf092"}
finalised: 2026-10-15
---

# Concept of Operations

Organisation-level view of how a telehealth and hospital-in-the-home service operates once Mākoha exists. Revised 15 Oct 2026 against PRD v2.0 (compendium revision 2): front-office stakeholders, external systems, situations, policies and risks added; structure unchanged. Derived from the PRD (01-prd.md, final v2.0) and, where cited, the Mākoha Design Compendium (`docs/ref/makoha-design-compendium.md`). System-level behaviour belongs to phase 3. Identifiers minted here: SIT- (operational situations), STK- (stakeholders), POL- (policies), RSK- (operational risks), EXT- (external systems), CCR- (change requests raised by this document; CR- remains the PRD's family).

## 1. Mission and need

Derived from PRD section 2 and G-01 to G-10.

A telehealth and hospital-in-the-home service run by general practitioners with nurse and pharmacist prescribers needs to see a patient it may never have met in person, prepared, with the whole record reasoned over rather than re-read; to supervise patients at home as closely as a ward would; and to accrue evidence of its own safety and efficacy while it operates. Today's systems store the free text that holds most of the record's meaning but cannot reason over it, so preparation is re-reading, safety checks fire on coded fields only, deterioration is spotted per contact rather than as a trajectory, and audit or research means a separate project over sampled paper.

The need is a record that turns language into provenanced facts, lets machines propose decisions only as gated arguments with typed uncertainty, and makes every decision replayable, so that operations and prospective study are the same activity over the same ledger (PRD G-10, section 8.1).

## 2. How the job is done today

Stated 25 Sep 2026: the job is done today as a standard encounter or episode of care. Mākoha augments that encounter and episode; it does not replace the clinical process, the roles or the sequence. The walk-through is therefore the ordinary one: booking, pre-consultation history, consultation, orders and prescriptions, follow-up, inbound results and correspondence, and for HITH the admission to the episode, scheduled visits and monitoring, escalation and discharge.

Where it hurts, as stated: some patients are slow at, or less able to, text. Typed pre-intake, check-ins and messages exclude them. The stated solution is real-time voice-to-voice interaction for the patient face. OpenAI's GPT-Live-1 (API released 10 September 2026: full-duplex, listens and speaks at once, handles interruptions and backchannels, delegates reasoning and tool calls to a backend text model) was the first example named; on 25 Sep 2026 it was ruled that the voice model is self-hosted with content-hash-pinned weights so Laws 5 and 7 hold, examples including Fish Audio (PRD CST-13, CAP-20). The capability is class 3, which is why the first release is the Tier 3 profile (CCR-02, approved).

## 3. What changes: the desired operation as a delta

Derived from Volume 1A.3 (lifecycle: before, during, after, between, population), 1A.4 (setting profiles) and PRD section 8.2. Only what changes is named.

| Moment | Today (per PRD section 2) | With Mākoha |
| --- | --- | --- |
| Before the session | Clinician re-reads the record | A consult-prep brief of released arguments is ready before the session joins, within a reading budget; for telehealth, a pre-intake agent has already gathered structured grounds from the patient as a rejectable argument |
| During the session | Notes typed after; checks on coded fields | Ambient capture produces session facts; a flagged "consider" differential with next-best questions; prescribing checked against the reconciled medication story before signing |
| After the session | Follow-ups remembered or lost | Signed plan yields tasks with owners and due dates; coding proposals with span evidence; patient-register summary delivered after sign-off |
| Between contacts (HITH) | Deterioration noticed per visit | Device streams and check-ins re-score risk after every fact change; one trajectory; escalation packet carries the argument, not a phone summary |
| Inbound | Letters, results and messages read in arrival order | Classified, matched to the originating order, routed by urgency; discrepancies surfaced before a clinician opens the letter |
| Scope of practice | Nurse and pharmacist prescribers phone the GP | Profile applied at evaluation time; out-of-scope predicate creates an escalation packet with full context |
| Governance and research | Audit by sampling; studies as projects | Sentinel events, audits and prospective studies are queries over the ledger; a study is a sealed envelope with enrolment on phenotype match |
| Front door (revision 2; PRD section 8.1, CAP-21 to CAP-23) | Enquiries arrive on the reception phone, a WhatsApp number, email and web forms and live in spreadsheets or a separate CRM; after-hours calls go to voicemail | Every enquiry becomes a lead in its own compartment with a response clock; one desk over WhatsApp, SMS, email and calls with intent and urgency; a voice line answers, books, takes messages and hands off; nothing clinical attaches to a lead and no message carries an identifier the channel may not |
| Forms and documents at volume (revision 2; CAP-24, CAP-25) | Paper and PDF forms re-keyed; scanned backlogs and fax archives filed unread | Designer forms bound field by field to the record, completed on portal, SMS, WhatsApp or by voice; archives split, recognised and extracted with per-field reliability, low-reliability fields reviewed by a person |

## 4. Stakeholders

Users derived from PRD section 3; non-users derived from PRD sections 9, 10 and 13 and Volume 2A.3. Rows marked proposed are not in upstream.

| Id | Stakeholder | Stake | User? |
| --- | --- | --- | --- |
| STK-01 | General practitioners operating telehealth and HITH | Prepared sessions; safe prescribing; supervising physician for HITH episodes | Yes |
| STK-02 | Nurse prescribers | Protocol pathways within formulary; escalation with context | Yes |
| STK-03 | Pharmacist prescribers | Reconciled medication history; medication review; red-flag routing | Yes |
| STK-04 | Patients and carers | Pre-intake, check-ins, device readings, results and plan in their own words; consent | Yes |
| STK-05 | Practice governance (clinical governance role) | Ratifies loss matrices, templates, thresholds; reviews sentinel events; owns the evaluation register; ratifies the intent taxonomy codebook (D-21) and any engagement factor drawn from coverage or billing bands (D-12) | Yes |
| STK-06 | Study owners and clinical researchers | Register studies, enrol on match, read endpoints, receive consented extracts | Yes |
| STK-07 | Medsafe (New Zealand), then the TGA (Australia), possibly the FDA (United States) (OCR-01) | New Zealand: WAND notification by the sponsor and post-market obligations; Australia: device classification for the Tier 3 profile (D-11); United States: classification as a compliance item; regulator bundle for each | No |
| STK-08 | Compliance role | Terminology licence (D-07); obligations register; device confirmation; tokenisation key custody with architecture (D-16); tier placement with architecture (D-20); provider terms and marketing consent in the obligations register (CST-17) | No |
| STK-09 | Architecture role | Owns D-01, D-03, D-06, D-08, D-12, D-13, D-19, D-20 and, with compliance, D-16 | No |
| STK-10 | Hospitals discharging into HITH and receiving escalations | Send discharge summaries; receive handover and escalation packets | No |
| STK-11 | Laboratories, imaging providers, pharmacies | Receive orders; return results and dispense records | No |
| STK-12 | Health and Disability Ethics Committees (HDEC) and, for out-of-scope studies, an institutional ethics committee | Confirmed 25 Sep 2026 as low-friction. Mandated, not merely good practice, when a study is health and disability research within HDEC scope: intervention studies, and observational studies that use identifiable information without consent or carry other elevated risk. Audits and quality-improvement studies evaluating current or slightly changed practice are out of HDEC scope but still require ethics review by an institutional or independent committee under the NEAC National Ethical Standards (2019). Each study in SIT-07 is classified at registration | No |
| STK-13 | {{TBD: payer or funder of the service (deferred)}} | | No |
| STK-14 | Front-office and practice-growth staff (reception, intake, campaign owners) of the telehealth and HITH service (revision 2; PRD section 3, front-office profile) | Lead register with response clocks; omnichannel desk; voice-line console; campaign brief form; cannot sign any clinical act | Yes |
| STK-15 | Enquirers and leads: people who have contacted the service but are not yet its patients (revision 2; 3A.2 A6) | A reply within the response window; their channel consents honoured; nothing clinical recorded about them before conversion | Yes (public front door and voice line only) |
| STK-16 | Messaging and telephony providers: WhatsApp Business provider, SMS and email gateways, telephony (SIP or hosted) (revision 2; D-14, D-15, CST-17) | Provider agreements, template approvals, data-processing terms, residency statement in the obligations register; coexistence and warm-transfer capability | No |
| STK-17 | Platform operator role (revision 2) | Owns provider selection D-14 and D-15 before M5; operates adapters and credentials | No |
| STK-18 | Partners and integrators (revision 2; deferred with L1 and L3, PRD section 8.1) | No stake at the first release; tenancy, sandbox and SDKs follow a later release decision | No |

## 5. Operational environment

Derived from PRD sections 8.1 and 9, Volume 3A groups F, J and 3.2. External system names are as the compendium gives them; New Zealand instances are not yet named.

| Aspect | Description |
| --- | --- |
| Settings | Telehealth (video and phone sessions bound to encounters) and hospital in the home (episodes of care with scheduled visits, device streams, escalation rules); from revision 2, the front office of both services under the front-office setting profile (1A.4): lead register, omnichannel desk, voice line, forms and campaigns |
| Organisational unit | Deferred 25 Sep 2026 |
| Jurisdiction | New Zealand first (Medsafe), Australia second (TGA); site agnostic |
| Regulatory posture | Tier 3 profile (general-purpose assistant): class-2 outputs flagged only; class-3 outputs through review queues only, never a control; permitted-prompt whitelist as signed configuration (D-06). In New Zealand today there is no pre-market approval for medical devices under the Medicines Act 1981: a New Zealand sponsor notifies the device in Medsafe's WAND database within 30 days, holds evidence that it is safe for its intended purpose, and meets post-market obligations (complaints, adverse events, recalls, changes). The Medical Products Bill, to replace the Medicines Act, will regulate software as a medical device including AI used for a therapeutic purpose, with an internationally aligned definition that excludes general clinical software and general-use AI; Cabinet agreed further policy on 7 April 2026; the Government intends to introduce the bill in 2026 with commencement around 2030 and a longer transition for many devices. This is the closing window in CST-12. See CCR-03 |
| Physical | Clinicians remote; patients at home with connected devices (BP, glucose, SpO2, weight, wearables, HITH equipment); edge node possible on a practice server or in a browser |

| Id | External system (Volume 3A) | Direction | New Zealand instance |
| --- | --- | --- | --- |
| EXT-01 | National patient and provider identifiers | Lookup | National Health Index (NHI; new AAA11A# format issued from 1 July 2026) and Health Provider Index (HPI: Practitioner, Organisation, Facility, PractitionerRole), Health New Zealand \| Te Whatu Ora |
| EXT-02 | Secure clinical messaging network | Both | HealthLink (results, referrals, clinical documents, discharge summaries). GP2GP record transfer runs over it and is being stabilised then replaced by API-based transfer |
| EXT-03 | Shared national record | Both | Hira, Health New Zealand's national health information platform and API marketplace; NZ International Patient Summary (HISO 10099) as the exchange standard; regional clinical data repositories such as TestSafe (Northern region, on Sysmex Éclair) |
| EXT-04 | Electronic prescribing and dispense records | Both | New Zealand ePrescription Service (NZePS), via the Connected Health programme |
| EXT-05 | Laboratory and imaging result feeds | Inbound | Community and hospital laboratories and radiology via HealthLink; regional repositories (TestSafe) where available |
| EXT-06 | Hospital discharge summaries | Inbound | via EXT-02 or EXT-03 |
| EXT-07 | Terminology edition (national SNOMED CT edition) | Pinned | New Zealand edition (D-07); {{TBD: confirm release cadence and licence holder (deferred)}} |
| EXT-08 | Video session provider (WebRTC), SMS and email gateways | Both | Vendors deferred 25 Sep 2026. The voice agent is not an external system: it is a self-hosted sidecar (PRD CAP-20, CST-13); the telephony carrier it answers through is EXT-14 |
| EXT-09 | Home device gateways | Inbound | Vendors deferred 25 Sep 2026 |
| EXT-10 | Identity providers per face (professional registration, consumer identity) | Auth | Professional: HPI-bound registration (Medical Council, Nursing Council, Pharmacy Council). Consumer: {{TBD: national consumer health identity, unconfirmed by search (deferred)}} |
| EXT-11 | Billing | Both | Private billing in New Zealand: invoices, payments, receipts; no claiming gateway in the first release (OCR-03); Australian claiming channels return with the TGA release |
| EXT-12 | Independent append-only log for Merkle anchoring (D-08) | Outbound | Provider open |
| EXT-13 | WhatsApp Business provider with coexistence mode on the practice's existing number (revision 2; 3A.11 J4) | Both | Provider open (D-14); selected before M5; adapter trait; template approvals and the 24-hour window tracked per thread |
| EXT-14 | Telephony carrier, SIP or hosted, with warm transfer (revision 2; 3A.11 J5) | Both | Provider open (D-15); selected before M5; numbers per tenant and location; adapter trait |
| EXT-15 | Fax gateway, scanner batches and archive exports from incumbent systems (revision 2; 3A.7 F5) | Inbound | Vendors deferred 15 Oct 2026; content-addressed on arrival |
| EXT-16 | Public front door: website widget, QR landing pages, public booking link (revision 2; 2A.1, 3A.2 A4, A6) | Inbound | Hosted by the service on its own domain; submits public-audience forms (3A.9 H4) |
| EXT-17 | Tenant vault, HSM or KMS for tokenisation keys (revision 2; 12.4) | Internal to the trust boundary | Deferred with L2 (PRD section 8.1); custody decided by D-16 before M8 |

## 6. Operational situations

Derived from Volume 1A.3 operations, the discharge acceptance episode in Volume 2A.4 and PRD section 8.2. Each has a trigger, actors and outcome so phase 3 can refine it into scenarios.

| Id | Situation | Kind | Trigger | Actors | Outcome |
| --- | --- | --- | --- | --- | --- |
| SIT-01 | Telehealth consultation with an unfamiliar patient | Routine | Appointment booked | Patient, pre-intake agent, GP or prescriber | Pre-intake argument and brief ready before join; session facts captured; flagged differential considered; prescriptions checked; tasks and patient summary signed |
| SIT-02 | HITH daily supervision | Routine | Episode active; scheduled check-in or device reading | Patient, devices, HITH nurse, supervising GP | Facts posted; risk re-scored after every change; next-day visit plan as tasks; daily summary queued for sign |
| SIT-03 | Deterioration at home | Urgent | Sustained device threshold breach or symptom check-in | Patient, HITH team, supervising GP, hospital | Critical-lane event; flagged deterioration argument; escalation packet with brief, facts, open attempts and acts; same-day action or "no longer fits home care" argument |
| SIT-04 | Post-discharge medication discrepancy | Exception | Discharge summary filed; patient reports a different dose | Inbound pipeline, pharmacist prescriber, patient | Disagreement row exists before any clinician opens the letter; pharmacist call task within 48 h; reconciled list before next prescribing check |
| SIT-05 | Inbound item that cannot be matched | Exception | Result or letter with low patient or order match weight | Inbound pipeline, reconciliation queue, staff | Never auto-filed; reconciliation queue; unfiled items past configured age escalate |
| SIT-06 | Prescriber reaches the edge of scope | Exception | Out-of-scope predicate fires or medication outside formulary | Nurse or pharmacist prescriber, GP | Order held; escalation packet created with argument ids; GP acts on the same graph without re-telling |
| SIT-07 | Prospective study alongside operations | Routine (governance) | Governance registers a study; cohort phenotype matches | Study owner, governance, patients (consent), evaluator | Sealed envelope; enrolment on match with consent scope; endpoints as validated Measures at window end |
| SIT-08 | Onboarding a service or site | Onboarding | New organisation, prescriber or patient cohort joins | Compliance, governance, architecture, staff | Profiles and scope fragments compiled; identities bound; baselines for MET-01 to MET-11 captured at cut-over |
| SIT-09 | Engine drift or retirement | Exception | Drift monitor breach on a class-2 engine | Governance, architecture | Engine pin retired; its claim types fall back to class 1; sentinel entry; no silent degradation |
| SIT-10 | Enquiry to registration (revision 2; E2E-14) | Routine (front office) | An unknown person enquires on WhatsApp, SMS, the web widget, a QR page or by phone | Enquirer (STK-15), front-office staff (STK-14), voice line, engagement rules | A lead with source and response clock; staff reply within the window or the clock breaches to a Task; follow-through steps on consented channels; booking; arrival; conversion to Patient with pre-registration answers carried over; no clinical fact before conversion |
| SIT-11 | Omnichannel message triage (revision 2; E2E-15) | Routine (front office); urgent when red-flagged | Inbound messages and call records on any channel | Patients and enquirers, front-office staff, clinicians by routing lane | Each item classified for intent, urgency and tone and laned by rule; emergency keywords reach the critical lane under 100 ms by the class-1 floor; replies within the WhatsApp window or by approved template; an outbound draft carrying a record number is blocked |
| SIT-12 | After-hours call on the voice line (revision 2; E2E-16) | Routine (front office); exception on hand-off | Inbound call outside hours, or a scheduled outbound confirmation or check-in call | Caller, voice line, on-call clinician | Identity confirmed before anything patient-specific; after-hours guidance spoken; booking by class-1 rules; message taken as a Task with transcript; any clinical question handed off within one turn; emergency keyword plays the guidance fragment and emits the critical event; recording only after consent |
| SIT-13 | Form built and completed across transports (revision 2; E2E-17) | Routine (governance, then patients) | Clinical owner designs an intake form; patient completes it on phone, partly by IVR | Clinical governance, form designer, patient, voice line | Form compiled with every field bound; assigned to an appointment type; one transaction Bundle with provisional facts and spans; identical resources whichever transport carried the answer |
| SIT-14 | Document archive intake (revision 2; E2E-18) | Onboarding and routine | A 1,000-page archive, scanner batch or fax stream arrives | Fax gateway, document intake pipeline, reviewers (staff and clinicians) | Resumable batch; documents split, recognised, classified and matched; low-reliability fields reviewed before becoming facts; an extracted critical laboratory value fires the critical lane |
| SIT-15 | Campaign brief to published sequence (revision 2; 1A.3 op 21) | Routine (front office, governance) | Front office or governance files a typed campaign brief | Campaign owner (STK-14), drafting loop, claims-boundary lint, clinical governance | Drafts of landing-page copy, message sequence and nurture cadence; cure, guarantee and outcome claims rejected; publication only through the compiler as pinned templates and a loop fragment; audience consent-checked at launch |

Situations for the deferred revision 2 modules (panel worklist and outreach, tokenised analytics, white-label tenant, overlay deployment: E2E-19 to E2E-21 and operation 23) are not operated at the first release (PRD section 8.1) and are not refined by phase 3 in this revision.

## 7. Policies and constraints

Derived from PRD sections 5, 9 and 10 and Volume 2.1, 11.4. These bound how the service may be operated; phase 5 turns them into requirements.

| Id | Policy | Source |
| --- | --- | --- |
| POL-01 | No autonomous prescribing; no order acted on without a signing clinician | NG-01 |
| POL-02 | Only the evaluator assigns released, flagged or held; machine outputs are proposals until gated | PRD section 5, Law 4 |
| POL-03 | A held argument is invisible to every face; a flagged one is visible to clinician and governance only; a patient sees a released argument only after sign-off | Volume 2.1 |
| POL-04 | Scope of practice is a signed profile fragment applied at evaluation time; escalation carries the full context packet | PRD section 3; Volume 1A.4 |
| POL-05 | Consent gates secondary use, research export and contact for eligibility; withdrawal propagates as an event | Volume 2A.1; 3A.10 |
| POL-06 | Break-glass access requires a reason, writes an act and a sentinel entry | CST-07 |
| POL-07 | Loss matrices, templates and thresholds are ratified by clinical governance before use; provisional templates may reach flagged but never released | CST-09, CST-10 |
| POL-08 | Studies are registered as sealed envelopes before their window; a changed plan is a new envelope | Volume 10.4 |
| POL-09 | A New Zealand sponsor is appointed and the device notified in WAND, with safety evidence held, before the Tier 3 profile operates in New Zealand; TGA classification confirmed before Australia | CST-03 |
| POL-10 | No online learning in production; no fusion of probabilities across engines; no composite ranking of patients or clinicians | NG-02, NG-03, NG-05 |
| POL-11 | Privacy: Privacy Act 2020 and Health Information Privacy Code 2020; Telecommunications Information Privacy Code 2020 for telehealth traffic | Search 25 Sep 2026 |
| POL-12 | Practice: Health Practitioners Competence Assurance Act 2003; Health and Disability Commissioner's Code of Health and Disability Services Consumers' Rights; Medical Council of New Zealand Statement on Telehealth (same standard of care as in person, within the modality's limits; registration, examination and prescribing expectations); RNZCGP position statement on telehealth in primary care | Search 25 Sep 2026 |
| POL-13 | Prescribing: Medicines Act 1981 and Medicines Regulations 1984 (regulations 40 and 41 on prescriptions, with a current waiver on 41); Misuse of Drugs Regulations 1977; Medicines (Designated Prescriber: Registered Nurses) Regulations 2016 with the gazetted specified-medicines list and Nursing Council guidance (August 2024); pharmacist prescriber regulations {{TBD: exact instrument not confirmed by search (deferred)}} | Search 25 Sep 2026 |
| POL-14 | Devices: Medicines (Database of Medical Devices) Regulations 2003 (WAND notification by a New Zealand sponsor); the Medical Products Bill once enacted | Search 25 Sep 2026 |
| POL-15 | Research: NEAC National Ethical Standards for Health and Disability Research and Quality Improvement (2019); HDEC standard operating procedures for scope | Search 25 Sep 2026 |
| POL-16 | Lead compartment: a lead is a Person, never a Patient, until a conversion act; nothing clinical attaches to a lead; a lead's communications never become grounds; engines and the evaluator have no read path to the compartment; no lead score is stored or displayed as one number and a patient's clinical risk tier is never an input to an engagement rule | D-12; CAP-21; 3A.2 A6 |
| POL-17 | Outbound messages: every rendered message on SMS, WhatsApp, email, IVR or voice passes the outbound PHI check; a record number blocks the send with no override; any other identifier or out-of-class clinical content needs an override act with reason; every automated message carries the label and a reach-a-person route, spoken on the voice line | 9.8; CAP-22; 2A.1 automated-message labelling |
| POL-18 | Channel rules: WhatsApp free-form replies only within the 24-hour service window, otherwise provider-approved template fragments; an opt-out on any channel stops every channel for that Person permanently; quiet hours apply; provider agreements, template approvals, data-processing terms and residency recorded in the obligations register before a channel operates | CST-17; 3A.11 J4; 10.8 |
| POL-19 | Voice line: identity confirmed by two identifiers before any patient-specific action; no clinical question answered; every spoken patient-specific statement is a released, signed argument in the plain register; hand-off to a person within one turn on any cue; no audio stored before the consent prompt is accepted | CAP-23; 3A.11 J5 |
| POL-20 | Marketing and outreach: campaign copy passes the claims-boundary and plain-register lints; health information in campaigns is certified general information only; a patient-list audience needs the contact-for-programme consent scope per patient and excludes the deceased; outreach happens within the tenant's monthly message allowance; the Unsolicited Electronic Messages Act 2007 (consent, sender identification, functional unsubscribe) applies to commercial electronic messages | 3A.2 A7; 10.8; Act cited from general knowledge, to be confirmed by compliance |
| POL-21 | Vendor figures from the teardown are claims, never baselines or targets; baselines are captured at cut-over | CST-18 |
| POL-22 | Hosting and models: every model sidecar runs inside the chosen hosting posture; no hosted model, including one under tenant-supplied keys, runs on the release path | CST-16; D-19 |

## 8. Operational risks and mitigation concepts

Derived from the ten laws (PRD section 5), Volume 9.6, 3.4, 10 and PRD section 12.

| Id | Risk | For whom | Mitigation concept | Source |
| --- | --- | --- | --- | --- |
| RSK-01 | Alert fatigue: clinicians ignore flagged items | Clinicians, patients | Attention budget per encounter under a governed suppression policy; suppressed items reachable and counted | Law 9 |
| RSK-02 | Wrong-patient or wrong-order match on inbound | Patients | Probabilistic matcher with pinned weights; below threshold goes to reconciliation queue, never guessed | Volume 3.4 |
| RSK-03 | A class-2 engine degrades unnoticed | Patients | Drift monitor per engine per subgroup; breach retires the pin; claim types fall back to class 1 | Volume 1A.7 |
| RSK-04 | Home device miscalibrated or unknown | HITH patients | Device identity and calibration status stored; unknown calibration imposes a reliability floor | TH-04 |
| RSK-05 | Escalation loses context between prescriber and GP | Patients, prescribers | Escalation packet is a signed bundle of brief, facts, open attempts and acts | Volume 1A.4 |
| RSK-06 | Legislation receives royal assent before launch | The programme | Bill tracked against milestone exits; launch scope kept small | CST-12 |
| RSK-07 | Loss matrices not ratified in time for the first-release claim types | The programme | Ratification is an M9 exit gate; placeholders never reach a Tier 3 release build | CST-10 |
| RSK-08 | Study evidence contaminates training or knowledge | Research integrity, patients | Evaluation firewall; zone labels; compiler gate 1 rejects evaluation-zone provenance | Law 10 |
| RSK-09 | Patients slow at or unable to text are excluded from pre-intake, check-ins and messaging | Patients | Real-time voice-to-voice patient interaction (PRD CAP-20); voice answers stored as questionnaire responses with dialogue spans, as typed ones are; no recording without consent | Stated 25 Sep 2026 |
| RSK-11 | A class-3 voice or text output reaches a patient as advice | Patients | Bounded loop: class-3 outputs go to a review queue only and are never a control; the patient face renders released, signed arguments only | Law 4; Volume 7.5; POL-03 |
| RSK-10 | Organisation-specific operational risks (staffing, home connectivity, digital access) | Deferred 25 Sep 2026 | To be added when stated | |
| RSK-12 | Lead data leaks into clinical reasoning, or a patient's clinical standing shapes how quickly they are answered | Patients, enquirers | Lead compartment with no engine or evaluator read path; risk tier absent from every engagement rule input; queues ordered by clock and stage only | POL-16; LEAD-01 |
| RSK-13 | An identifier or clinical detail leaves the system in a WhatsApp, SMS or email message | Patients | Outbound PHI check at render time; record number blocks with no override; override acts surveilled | POL-17; OMNI-04 |
| RSK-14 | The voice line gives clinical advice, acts for the wrong caller, or records without consent | Patients, the programme | Dialogue class 3 under the bounded loop with hand-off cues; identity confirmation by two identifiers; consent prompt before audio storage; IVR floor is class 1 | POL-19; VOX-03, VOX-05 |
| RSK-15 | A mis-recognised field from a scanned archive becomes a fact | Patients | Per-field reliability; below floor and review-always types go to a review queue; accepted fields carry the reviewer as principal | DAI-01 |
| RSK-16 | Campaign or outreach copy makes a clinical claim, or reaches people who did not consent | Enquirers, patients, the programme | Claims-boundary lint; consent scope per audience member; permanent cross-channel opt-out; monthly allowance | POL-20; CAMP-01 |
| RSK-17 | WhatsApp or telephony provider outage, policy change or template rejection | Front office, patients | Adapter traits with provider selection before M5; fallback to SMS, email and the IVR floor; template approval status stored on the fragment | D-14, D-15; CST-17 |
| RSK-18 | Front-office staff act beyond the restricted aperture | Patients | Front-office token cannot post a sign-off or any clinical act (1A.4 front-office profile tests); every write attributed | PRD section 3; 2A.0 |

## 9. Operational Concept Graphic

Mermaid is the source of truth. Actors, the capability as one node, external systems, the environment as the enclosing subgraph, principal flows labelled.

```mermaid
flowchart LR
  subgraph NZ["Telehealth and hospital-in-the-home service, New Zealand (Tier 3)"]
    P[Patient at home<br/>devices, check-ins, voice]
    E[Enquirer or lead<br/>WhatsApp, SMS, call, web form]
    F[Front-office staff<br/>desk, lead register, voice-line console]
    C[GP, nurse and pharmacist<br/>prescribers]
    G[Governance and<br/>study owners]
    M[Mākoha<br/>record, argument, gate, ledger]
    P -->|pre-intake, readings, messages| M
    M -->|released plan, reminders| P
    E -->|enquiry, booking, answers| M
    M -->|reply within clock, confirmation| E
    F -->|lead stage, reply, hand-off, file| M
    M -->|lanes, clocks, call transcripts| F
    C -->|session, orders, signed acts| M
    M -->|brief, flagged items, escalation packet| C
    G -->|ratify, register study| M
    M -->|sentinel events, measures, bundle| G
  end
  W[WhatsApp and telephony<br/>providers] <--> M
  X[Fax gateway, scanner,<br/>archive exports] -->|documents at volume| M
  H[Hospitals] -->|discharge summaries| M
  M -->|handover, escalation| H
  L[Labs, imaging, pharmacies] -->|results, dispense| M
  M -->|orders, prescriptions| L
  N[National identifiers,<br/>messaging, shared record] <--> M
  R[Medsafe] -->|classification| G
```

## 10. Change requests to upstream

The PRD is final. All four were approved and applied to 01-prd.md on 25 Sep 2026; `docpipe update` run afterwards. Revision of 15 Oct 2026: no new change request; PRD v2.0 was revised directly from compendium revision 2 and this document derives from it.

| Id | Target | Item | Change |
| --- | --- | --- | --- |
| CCR-01 | 01-prd.md | Section 8.2, operation 1 row and the consequence paragraph; section 3 telehealth row | The pre-intake conversational agent runs under the Volume 7.5 bounded generative loop (Volume 2A.1, 3A.11 J2, POR-03), which is class 3 and excluded from the Tier 2 build. The PRD places "the telehealth pre-intake summary as a rejectable argument" in the Tier 2 first release. Correct to: typed or form-based pre-intake questionnaires (class 1) in Tier 2; the conversational pre-intake agent in Tier 3 |
| CCR-02 | 01-prd.md | Section 7 (CAP-20), section 8.1, 8.2, CST-13, RSK-09 here | Add real-time voice-to-voice patient interaction for pre-intake, check-ins and messages for patients slow at or unable to text. A generative voice model is class 3 under Law 4 and Volume 7.5, so the capability belongs to the Tier 3 profile. Ruled: first release is Tier 3 so voice ships from day one; the voice model is self-hosted with pinned weights, not a vendor API (examples: Fish Audio) |
| CCR-03 | 01-prd.md | CST-03, CST-12, section 12 | In New Zealand today there is no device classification or pre-market approval to confirm (Medicines Act 1981): the obligation is WAND notification by a New Zealand sponsor with evidence of safety for intended purpose and post-market duties. Reword CST-03 for New Zealand to "sponsor appointed, WAND notification lodged, safety evidence held", keeping the decision-support classification for the TGA and for the Medical Products Bill once enacted. Reword CST-12: the window closes at commencement of the Medical Products Bill, planned around 2030 after introduction in 2026, with a transition period |
| CCR-04 | Compendium (via CR-01) | Volume 7.4 | "pre-intake question" is used as a claim type and is in neither vocabulary list; add to the union |

## 11. Assumptions

| Assumption | Confidence | How it would be checked |
| --- | --- | --- |
| The operating organisation can staff HITH with a nurse-led team under GP supervision across the launch cohort | Deferred 25 Sep 2026 | Staffing plan at SIT-08 |
| Patients in the launch cohort have connectivity and devices adequate for daily check-ins | Deferred 25 Sep 2026 | Digital-access screening at enrolment |
| New Zealand national systems (EXT-01 to EXT-05) expose interfaces the compendium's adapters can implement | Medium | Named in section 5 from public sources, not yet from integration documentation; confirmed in phase 4 |
| The Medical Products Bill commences around 2030, so a Tier 3 launch under the current WAND-notification regime is achievable | Medium | Bill progress tracked at every milestone exit (RSK-06) |
| The service's existing reception number can be kept on WhatsApp coexistence mode and ported or forwarded to the telephony provider without a service break | Medium | Provider selection and a cut-over rehearsal before M5 (EXT-13, EXT-14) |
| Front-office staff of the launch service can staff the desk, the lead queues and the review queues for intake fields without a new role | Medium | Queue volumes measured in the onboarding pilot (phase 3 onboarding mode) |

## 12. Open questions

- [x] Current-operations walk-through: standard encounter and episode of care, augmented (section 2)
- [ ] Operating organisation and structure (section 5) {{TBD: operating organisation (deferred)}}
- [x] New Zealand names for EXT-01 to EXT-05 from public sources; EXT-08, EXT-09 vendors and consumer identity deferred
- [x] HDEC confirmed and its mandate stated (STK-12); payer or funder deferred (STK-13)
- [x] New Zealand law and standards (POL-11 to POL-15); pharmacist prescriber instrument unconfirmed
- [ ] Organisation-seen operational risks deferred (RSK-10)
- [x] CCR-01 to CCR-04 approved and applied; first release is Tier 3
- [x] Voice engine: self-hosted, weights content-hash pinned; examples include Fish Audio (PRD CST-13)
- [x] Revision 2 (15 Oct 2026): front office added as a setting, stakeholders STK-14 to STK-18, external systems EXT-13 to EXT-17, situations SIT-10 to SIT-15, policies POL-16 to POL-22, risks RSK-12 to RSK-18
- [ ] Confirm the Unsolicited Electronic Messages Act 2007 reading in POL-20 with compliance
- [ ] Vendors for EXT-13 to EXT-15 (deferred to D-14, D-15 before M5)
