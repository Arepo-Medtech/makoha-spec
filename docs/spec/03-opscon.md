---
docpipe: 1
phase: 3
title: Operations Concept
status: final
version: 2.0
upstream: ["01-prd.md", "02-conops.md"]
upstream_hash: {"01-prd.md": "0e34202c06cdf092", "02-conops.md": "7fdb53fbc48fff39"}
finalised: 2026-10-15
---

# Operations Concept

System-level view of what Mākoha does for the telehealth and hospital-in-the-home service described in 02-conops.md (final v2.0), for which roles, in which modes, through which scenarios, across which interfaces, to what user-facing performance, and what it does when things fail. What, not how. Revised 15 Oct 2026 against PRD v2.0 and ConOps v2.0 (compendium revision 2): front-office roles, scenarios SCN-11 to SCN-16, interfaces, data objects, expectations and must-nevers added; structure unchanged. Derived from the PRD (01-prd.md, final v2.0), the ConOps and, where cited, the Mākoha Design Compendium (`docs/ref/makoha-design-compendium.md`). Identifiers minted here: ROL- (roles), MOD- (modes), SCN- (scenarios; steps are SCN-nn.k), IF- (interfaces), DAT- (data objects), PERF- (user-facing performance expectations), MN- (must-nevers), OCR- (change requests raised by this document).

## 1. System overview and boundary

Derived from PRD section 5 (Law 1, Law 2), Volume 1.5 and 1A.5.

Mākoha is one append-only ledger with three authorised faces (patient, clinician, governance), a record spine that stores every fact with span provenance, an engine plane that drafts arguments, a deterministic evaluator that assigns released, flagged or held, a compiler that is the only door for knowledge, and a render layer that shows the same argument in three registers. The first release is the Tier 3 profile for telehealth and HITH (PRD section 8.1).

| Inside the system | Outside the system (people or other systems) |
| --- | --- |
| Patient record, encounters, notes, problems, medications, allergies, observations, orders, tasks, communications, consent | The clinical decision itself: every order, prescription, plan and message is signed by a clinician (NG-01) |
| Fact extraction from text, audio transcripts, scans and device streams | Video and phone transport (IF-09); device firmware and calibration (IF-10) |
| Argument drafting, evaluation, rendering, attention budget, suppression | Hospital, laboratory, pharmacy and imaging systems on the far side of each interface |
| Pre-intake agent (typed and voice), engagement loops, patient messaging | National identifiers, messaging network, shared record, e-prescribing service (IF-01 to IF-05) |
| Lead register and follow-through, omnichannel desk with intent and urgency classification and the outbound PHI check, voice line (IVR, booking, check-ins, after-hours, hand-off), form designer and bound forms, document intake at volume, campaign drafting (revision 2; PRD section 8.1) | WhatsApp Business and telephony carriers (IF-16, IF-17); fax gateways and scanners (IF-18); the service's public website hosting the widget and QR pages (IF-19) |
| Compiler, pin registry, evaluation register, sealed envelopes, study enrolment, measures, regulator bundle | Ethics review (STK-12), regulator decisions (STK-07), clinical governance judgement (STK-05) |
| Edge node for offline operation; backup and restore | Nothing: Mākoha is the system of record for the service, including scheduling and billing (stated 25 Sep 2026). New Zealand billing is private billing: invoices, payments and receipts, no national claiming gateway in the first release (IF-14) |

## 2. Roles and permissions

Derived from PRD section 3, ConOps section 4, Volume 2 (identity binding, act record), 1A.4 and 2A.1. One line of permission each; a user may hold several roles. Non-human principals are roles too, because every write is attributed.

| Id | Role | Face | Permission in one line |
| --- | --- | --- | --- |
| ROL-01 | Patient | Patient | Reads released, signed arguments about self in the patient register; answers pre-intake and check-ins by text or voice; records goals, preferences, device readings; sets consent scopes; sees own access report |
| ROL-02 | Carer or delegate | Patient | As ROL-01 for the scoped sections a RelatedPerson grant allows; nothing else |
| ROL-03 | General practitioner (supervising physician for HITH) | Clinician | Full scope by registration; signs notes, orders, prescriptions, plans, summaries; acts on flagged items; receives escalation packets; supervises HITH episodes |
| ROL-04 | Nurse prescriber | Clinician | Prescribes within the formulary and protocol pathways of the signed scope fragment; runs HITH visits and check-ins; out-of-scope predicate creates an escalation packet |
| ROL-05 | Pharmacist prescriber | Clinician | Medication reconciliation and review; prescribes within minor-ailment and repeat-management protocols; red-flag routing blocks and escalates |
| ROL-06 | Practice or service staff, including front office (revision 2: the front-office aperture of 2A.0 under the front-office profile of 1A.4) | Clinician (restricted) | Scheduling; inbound queue triage and filing where the role allows; reconciliation queue; lead stages, replies by template or reviewed draft, hand-off, filing on the desk; voice-line console; campaign briefs; sees the routing lane and urgency badge but no clinical argument; cannot sign clinical acts |
| ROL-07 | Clinical governance | Governance | Ratifies loss matrices, templates, thresholds and suppression policy; reviews sentinel events and review queues; owns the evaluation register; approves study registration |
| ROL-08 | Study owner | Governance | Registers studies as sealed envelopes; reads enrolment and endpoints; receives consented de-identified extracts |
| ROL-09 | Compliance | Governance | Sponsor and WAND obligations; terminology licence; obligations register; regulator bundle export |
| ROL-10 | Platform operator (architecture role) | None (operations) | Deploys signed builds; manages pins and sidecars; backup, restore, sync; cannot read clinical content except through break-glass |
| ROL-11 | Regulator or auditor | Governance (federated) | Reads the regulator bundle and replays attempts with the offline verifier; no write |
| ROL-12 | Pre-intake and voice agent (non-human) | Patient (scope token) | Writes only QuestionnaireResponse and patient-reported Observation for the one patient in session; cannot read another patient; token, prompt and policy pinned |
| ROL-13 | Engines and compiler (non-human) | None | Engines draft arguments from pinned inputs only; the compiler alone inserts into the pin registry and generic-argument tables |

| ROL-14 | HITH nurse, non-prescribing (stated 25 Sep 2026) | Clinician | Runs HITH visits, check-ins and administrations under the care plan; records observations and notes; cannot prescribe; escalates to ROL-04 or ROL-03 by the profile's escalation target |
| ROL-15 | Identity administrator (stated 25 Sep 2026) | Governance (administration) | Manages user accounts and OAuth account lifecycle for every face: creates, binds to HPI and registration, assigns profiles, suspends, revokes; every change is an audited act; cannot read clinical content |
| ROL-16 | Enquirer or lead (revision 2; STK-15) | Public front door and voice line (no face account) | Submits public-audience forms, books from the public link, messages or calls the service; exists as a Person in the lead compartment; sees nothing from any record; becomes ROL-01 only on conversion |
| ROL-17 | Voice line agent (non-human; revision 2; CAP-23) | Patient (telephony transport, scope token) | Answers and places calls; IVR navigation, identity confirmation, booking through class-1 scheduling rules, spoken check-in instruments, message taking, hand-off; writes only QuestionnaireResponse, patient-reported Observation, Communication and Appointment transitions; speaks about a patient only a released, signed argument |
| ROL-18 | Follow-through and queue-worker rule step (non-human; revision 2; 3A.2 A7) | None | Decides contact, leave or hand off for a lead by class-1 rule and drafts text through the bounded loop; no read grant on resources, facts, attempts or arguments; its proposals wait on the owner's queue |

Roles stated as not needed or deferred: HITH coordinator and interpreter service were not named; day-to-day administration sits with ROL-15.

## 3. Modes of operation

Derived from Volume 1A.7 (drift retirement), 3.6 and 3A.12 (edge node), 3A.12 (backup and restore), 10 (evaluation zone). Entry and exit conditions are stated so phase 5 can write requirements against them.

| Id | Mode | Entry | Behaviour | Exit |
| --- | --- | --- | --- | --- |
| MOD-01 | Normal | Signed build attested at start-up; all pins present; connectivity to the store | All operations in PRD section 8.2; class ceilings enforced | Any entry condition of MOD-02 to MOD-04 |
| MOD-02 | Degraded, engine retired | Drift monitor breach on a class-2 engine for the configured window, or a manual retirement act | The engine's pin is marked retired; its claim types fall back to class-1 rules only; a sentinel entry is written; the governance face shows the retirement | A new validated engine pin is registered and admitted |
| MOD-03 | Offline, edge node | Loss of connectivity from a practice server or browser edge node to the spine | Notes, prescribing check with local pins, local extraction and paper scripts continue; national transactions (e-prescriptions, register uploads) queue; class-2 and class-3 engines that are not local are unavailable and their outputs absent, not guessed | Reconnect; additive sync exchanges versions by hash; conflicts become disagreement rows; queued transactions flush in order |
| MOD-04 | Maintenance and restore (proposed; confirmation deferred 25 Sep 2026) | Operator starts a point-in-time restore or a signed-build upgrade | Faces read-only; no new attempts; restore replays the event log to the chosen commit; the ledger chain is verified end to end before writes resume | Chain verified; build attestation matches manifest |
| MOD-05 | Onboarding and cut-over (proposed; confirmation deferred 25 Sep 2026) | A new organisation, site or cohort joins (ConOps SIT-08) | Profiles and scope fragments compiled; identities bound; incumbent data migrated with lineage; baselines for MET-01 to MET-11 captured before engines act for that cohort | Baseline MeasureReports published; governance act opens normal mode for the cohort |

Explicitly not modes: the evaluation zone (Volume 10) runs continuously beside normal mode with read access to the ledger and no write path to pins; regulator inspection is an export, not a mode; there is no training mode, because there is no online learning (NG-02).

## 4. Scenarios

Each ConOps situation is refined by at least one scenario. Every step has one actor and one observable action or response. Preconditions, trigger, outcome, variations and exceptions are stated. Class ceilings from PRD section 8.2 apply throughout. Derived from Volume 1A.3, 1A.4, 2A.1, 2A.2, 2A.4, 3.3, 3.5, 3A.11 and 9.5 to 9.6.

### SCN-01 Telehealth consultation with an unfamiliar patient (refines SIT-01)

Preconditions: patient registered with NHI matched; consent for portal contact; telehealth profile in force for the clinician. Trigger: appointment booked.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-01.1 | System | On the booking event, seeds the pre-intake agent with the patient's present facts within the pinned recency window and opens a pre-intake session by the patient's chosen channel: typed in the portal, or voice |
| SCN-01.2 | Patient (ROL-01) | Answers questions in own words; by voice, speaks and is spoken to in real time; may interrupt |
| SCN-01.3 | System | Stores each answer verbatim with its dialogue span and the extraction; never asks a question a documented fact already answers; walks the medication list line by line and records discrepancies as disagreement rows; scores validated instruments where the presentation warrants |
| SCN-01.4 | System | On a red-flag answer, emits a critical-lane event and an escalation packet to the practice queue before the appointment and tells the patient in plain words what happens next |
| SCN-01.5 | System | Writes the pre-intake summary as patient-reported facts plus a queued draft composition citing each fact; the patient sees no advice |
| SCN-01.6 | System | Before the session join, assembles the consult-prep brief: released arguments and profile-permitted flagged ones, priority ordered, within the reading budget; records what was suppressed; ready under 3 s |
| SCN-01.7 | Clinician (ROL-03/04/05) | Joins the session; reads the brief; opens the pre-intake summary and accepts or rejects it line by line as an act |
| SCN-01.8 | System | Streams ambient audio through transcription and language services; session facts appear within 2 s of utterance, marked draft-session, excluded from grounds until the note is signed |
| SCN-01.9 | System | On each new session fact, updates a flagged "consider" differential with discriminators and an ordered next-best-question list, within 500 ms |
| SCN-01.10 | Clinician | Mentions or orders a medication |
| SCN-01.11 | System | Runs the prescribing check against the reconciled list, allergies, problems and observations under the clinician's scope fragment; returns released, flagged or held within 200 ms; a deterministic contraindication is a modal hard stop |
| SCN-01.12 | Clinician | Ends the session |
| SCN-01.13 | System | Drafts the note, orders, letters and patient-register summary from signed facts and the bounded loop, every sentence citing a fact; all unsigned; under 10 s |
| SCN-01.14 | Clinician | Signs the note and each draft, or edits and signs, or rejects with reason |
| SCN-01.15 | System | Supersedes session facts with signed-note facts; issues coding proposals; creates one task per planned action with owner, due date and span; delivers the patient-register summary by the consented channel only after the sign-off act |
| SCN-01.16 | Patient | Reads the summary in own words; a comprehension check follows; a failed check creates a task for the clinician |

Outcome: a prepared session on a patient the clinician had not met, a signed record with span provenance, tasks in flight, the patient holding the signed plan. Variations: patient declines pre-intake (brief still assembled from the record); interpreter language pack selected from preferences; carer answers under delegate scope. Exceptions: pre-intake red flag (SCN-01.4); voice sidecar unavailable (agent falls back to typed channel and records the fallback); connectivity lost mid-session (MOD-03 if an edge node exists, otherwise the session continues on the video platform and facts are captured on reconnect from the recording only with consent).

### SCN-02 HITH daily supervision (refines SIT-02)

Preconditions: HITH episode of care open with care plan, scheduled visits and administrations, device streams registered with identity and calibration status. Trigger: scheduled check-in, visit, or device reading.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-02.1 | Patient or device | Submits a check-in answer or a reading (weight, SpO2, BP, glucose) |
| SCN-02.2 | System | Stores the reading with device pin, calibration status and declared accuracy; an unknown calibration status imposes the reliability floor; sustained threshold breaches are promoted to discrete Observations by pinned rules with a critical-lane event within 100 ms of promotion |
| SCN-02.3 | System | Re-scores deterioration, sepsis and readmission risk after every fact change, debounced 30 s, one attempt per burst, within 10 s of fact commit; each draft is flagged at most and lists exactly the facts consumed |
| SCN-02.4 | Nurse prescriber (ROL-04) | Opens the episode view: risk trajectory plotted from attempts, reconciled medications, today's administrations, open tasks |
| SCN-02.5 | Nurse prescriber | Records the visit: observations, administrations, notes by ambient capture or typing |
| SCN-02.6 | System | Generates next-day visit tasks from the care plan and signed facts; queues a daily physician summary draft citing facts |
| SCN-02.7 | Supervising GP (ROL-03) | Reviews the trajectory and the queued summary; signs or rejects with reason |
| SCN-02.8 | System | Runs nightly register and recall maintenance and quality analytics for the episode cohort |

Outcome: one reconstructable trajectory per patient, a signed daily summary, tomorrow's plan as tasks. Variations: device stream interrupted (gap shown, no imputation); patient-entered reading without device (reliability floor). Exceptions: deterioration (SCN-03); nurse acts outside formulary (SCN-06).

### SCN-03 Deterioration at home (refines SIT-03)

Preconditions: as SCN-02. Trigger: promoted threshold breach or symptom check-in meeting a deterioration rule.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-03.1 | System | Emits a critical-lane event; the deterioration argument is evaluated and, being class 2, is flagged with severity tier and rebuttals |
| SCN-03.2 | System | Assembles the escalation packet: brief as of now, session and device facts, every open attempt with verdict, acts taken; signs it with pins |
| SCN-03.3 | System | Notifies the HITH nurse and supervising GP by the profile's escalation target; books a same-day contact task; messages the patient citing only the released explanation of what happens next |
| SCN-03.4 | Nurse prescriber | Contacts or visits the patient; records findings |
| SCN-03.5 | Supervising GP | Reads the packet, not a phone summary; decides: adjust plan, arrange review, or accept the flagged "no longer fits home care" argument |
| SCN-03.6 | System | If the episode ends, builds the structured discharge-to-GP or transfer handover: episode summary plus extracted actions, every line citing facts and tasks; sends it by secure messaging to the receiving service once signed |
| SCN-03.7 | Governance (ROL-07) | Sees the escalation in the sentinel and signal views with lead time from first flagged attempt to escalation act |

Outcome: escalation with full context inside the re-score budget; readmission decision recorded as acts. Variations: patient unreachable (task escalates by rule after the configured interval). Exceptions: engine retired (MOD-02: deterioration falls back to class-1 threshold rules, shown as such); notification channel failure creates a task and tries the next channel.

### SCN-04 Post-discharge medication discrepancy (refines SIT-04)

Preconditions: patient enrolled; discharge summary arrives by secure messaging or shared record. Trigger: discharge summary filed, or patient reports a different dose in a post-discharge check-in.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-04.1 | System | Receives the document; verifies signature; stores the original content-addressed; matches patient and any open referral or order; classifies it (class 2, flagged if low reliability); extracts medication changes and follow-up requests with spans; routes it by urgency |
| SCN-04.2 | System | Compares extracted medications with the reconciled list and patient-reported facts; writes a disagreement row for each conflict before any clinician opens the letter; opens the post-discharge engagement loop |
| SCN-04.3 | Pre-intake or loop agent (ROL-12) | Confirms medication changes with the patient in plain language by text or voice; records what is actually taken as patient-reported facts |
| SCN-04.4 | System | Emits a critical-lane event for the discrepancy; creates a pharmacist call task due within 48 h |
| SCN-04.5 | Pharmacist prescriber (ROL-05) | Calls the patient; resolves the discrepancy; records the reconciled list as an act |
| SCN-04.6 | System | The next prescribing check for that class uses the reconciled list; follow-up requests in the letter (bloods, review, specialist) are tasks with due dates |
| SCN-04.7 | Governance | Sees the discrepancy as a surveillance signal without any human report; a repeat from the same ward is found by pattern search |

Outcome: no prescription signed against an unresolved discrepancy; near-miss visible to governance. Variations: discrepancy arrives from a dispense record rather than the patient. Exceptions: low-reliability patient match (SCN-05); patient cannot be reached (task escalates).

### SCN-05 Inbound item that cannot be matched (refines SIT-05)

Preconditions: inbound channels configured. Trigger: a result, letter or document whose patient or order match weight is below threshold, or whose signature fails.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-05.1 | System | Never auto-files; places the item in the reconciliation queue with the candidate matches and their weights; quarantines a document whose signature fails and raises a task |
| SCN-05.2 | Staff (ROL-06) | Reviews candidates; confirms the patient and order, or marks unmatched |
| SCN-05.3 | System | On confirmation, resumes extraction and routing; the order moves to resulted; on unmatched, returns or holds per rule |
| SCN-05.4 | System | Escalates any unfiled item older than the configured age to the clinician queue |

Outcome: nothing filed to the wrong patient. Exceptions: order already reconciled (duplicate detection creates a disagreement row, not a second result).

### SCN-06 Prescriber reaches the edge of scope (refines SIT-06)

Preconditions: scope fragment for the prescriber's profile in force. Trigger: medication outside the formulary, or an out-of-scope predicate fires during a check or protocol step.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-06.1 | Nurse or pharmacist prescriber | Drafts an order or reaches a protocol step |
| SCN-06.2 | System | Evaluates under the profile; a formulary breach is held; an out-of-scope predicate creates an escalation packet with argument ids and the open attempt |
| SCN-06.3 | System | Routes the packet to the GP named in the profile's escalation target |
| SCN-06.4 | Supervising GP | Reads the packet; signs the order, changes it, or declines with reason; all as acts on the same graph |
| SCN-06.5 | System | Continues the protocol step machine from the GP's act; counts the escalation and its completeness for MET-07 |

Outcome: no re-telling, no phone summary, within-scope completion tracked. Exceptions: GP unavailable (escalation target chain by rule).

### SCN-07 Prospective study alongside operations (refines SIT-07)

Preconditions: evaluation register entry exists for the fragment or loop under study (else the compiler refuses); ethics classification recorded (HDEC or institutional). Trigger: governance registers a study.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-07.1 | Study owner (ROL-08) | Defines cohort (phenotype pin), intervention (fragment or loop pin), comparison, endpoints (validated Measures), enrolment rule, sealed analysis plan, window |
| SCN-07.2 | System | Registers the sealed envelope: public hash, sealed content; refuses a Measure without a validation record |
| SCN-07.3 | System | On each phenotype match event, checks the consent scope for secondary use or contact for eligibility; enrols on first match with time and pins, or refuses without the scope |
| SCN-07.4 | Patient | Where contact is permitted, receives an eligibility message citing the released argument, and may opt in or out |
| SCN-07.5 | System | Collects endpoints at window end (interim reads are read-only and cannot alter the plan); a pin change on any dependency creates a revalidation task |
| SCN-07.6 | System | At window end, verifies the envelope hash, runs the queries with pins as of window start, runs the analysis plan, produces the report with the hash on its cover |
| SCN-07.7 | Governance | Records the finding as a MeasureReport plus decision act; a change becomes a compiler submission and a follow-up study |

Outcome: research evidence accrues in the ledger alongside use (G-10). Variations: quality-improvement study with period comparison and a short window. Exceptions: plan changed after registration (new envelope; old reported as abandoned); consent withdrawn (patient excluded from the next extract).

### SCN-08 Onboarding a service or site (refines SIT-08; MOD-05)

Preconditions: sponsor and WAND notification lodged; organisation identity established. Trigger: new organisation, prescriber group or cohort.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-08.1 | Compliance (ROL-09) | Records obligations: terminology licence, sponsor, consent templates |
| SCN-08.2 | Governance | Ratifies setting profiles, scope fragments, loss matrices and suppression policy for the site as signed fragments |
| SCN-08.3 | Platform operator (ROL-10) | Deploys the attested Tier 3 build; binds identity providers; registers device gateways and messaging endpoints |
| SCN-08.4 | System | Migrates incumbent data with lineage; every migrated fact carries source and span or is marked unstructured |
| SCN-08.5 | System | Captures cut-over baselines for MET-01 to MET-11 as MeasureReports before engines act for the cohort |
| SCN-08.6 | Governance | Opens normal mode for the cohort by act |

Outcome: a site operating with ratified knowledge and recorded baselines. Exceptions: migration conflicts become disagreement rows, never overwrites.

### SCN-09 Engine drift and retirement (refines SIT-09; MOD-02)

Preconditions: class-2 engine registered with validation report. Trigger: rolling conformal coverage or calibration breach per subgroup for the configured window.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-09.1 | System | Marks the engine pin retired; writes a sentinel entry; falls its claim types back to class-1 rules; shows the change on the governance face and on affected disposition lines |
| SCN-09.2 | Governance | Reviews the drift record by subgroup; decides on revalidation |
| SCN-09.3 | Architecture (ROL-10) | Submits a new engine pin with validation report through the compiler |
| SCN-09.4 | System | Admits it through the gates; the sentinel decision set is replayed against the new pin before it may draft |

Outcome: no silent degradation. Exceptions: no replacement available (fallback persists and is counted).

### SCN-10 Outage and offline operation (refines RSK and MOD-03; no ConOps situation)

Trigger: connectivity loss at a site with an edge node.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-10.1 | System | Edge node continues notes, prescribing check on local pins, local extraction, paper scripts; queues e-prescriptions and uploads; marks class-2 and class-3 outputs unavailable |
| SCN-10.2 | Clinician | Continues consulting; prints paper scripts where needed |
| SCN-10.3 | System | On reconnect, syncs additively by hash; conflicting fields become disagreement rows; queued national transactions flush in order |

Exceptions: two edge nodes wrote to one patient (both versions kept; disagreement rows).

### SCN-11 Enquiry to registration (refines SIT-10; E2E-14)

Preconditions: front-office profile in force with response-clock windows; WhatsApp number connected in coexistence mode; public booking link live. Trigger: a message from an unknown number, a public form submission, a QR landing page or an inbound call.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-11.1 | Enquirer (ROL-16) | Sends a WhatsApp message, submits the widget form, or calls the practice number |
| SCN-11.2 | System | Creates a Lead as a Person in the lead compartment with source, source detail and capturing principal; runs the red-flag fragment over the enquiry text and emits the critical-lane event with the emergency guidance fragment if it fires; starts the response clock |
| SCN-11.3 | System | Evaluates the engagement rule fragment: each factor (source class, recency band, stage progress, existing-patient status) as its own chip with points and rule pin; never a sum; places the lead on the owner queue ordered by clock state and stage |
| SCN-11.4 | Front-office staff (ROL-06) | Replies on the inbound channel within the window, by template or a reviewed draft; moves the stage to Contacted |
| SCN-11.5 | System | If no outbound reply exists at the window end, sets the clock overdue, creates a Task for the owner and writes a front-door signal row |
| SCN-11.6 | Follow-through step (ROL-18) | At ratified intervals, proposes the next step on a consented channel within the monthly allowance; stops on reply, opt-out, conversion or the step cap |
| SCN-11.7 | Enquirer | Books through the voice line or the public link; the Appointment names the lead's Person until conversion; a pre-registration form (public audience) is offered |
| SCN-11.8 | System | On arrival sets Showed; on a fulfilled Appointment with a linked Patient sets Converted |
| SCN-11.9 | Front-office staff | Converts the lead: the matcher runs against existing patients (link above the upper threshold; clerical review between thresholds; new Patient when none) |
| SCN-11.10 | System | Re-points QuestionnaireResponses and Communications to the Patient compartment with provenance source lead-intake; carries channel consents and opt-outs to the Patient's Consent resources; keeps the lead row with its converted patient id |

Outcome: a patient whose first contact, consents and pre-registration answers are in the record, with no clinical fact recorded before conversion. Variations: spreadsheet import with a dry run reporting duplicates; walk-in captured at the desk. Exceptions: opt-out on any channel stops every channel permanently (SCN-11.6 ends); a red flag at SCN-11.2 routes to the critical lane before any staff reply.

### SCN-12 Omnichannel message triage (refines SIT-11; E2E-15)

Preconditions: channels connected; routing rule fragment and intent taxonomy codebook in force (D-21). Trigger: an inbound message or call record on WhatsApp, SMS, email or the voice line.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-12.1 | System | Files the item as a Communication with its medium in the one queue, threaded by partOf; matches the sender only on a single verified phone or email identifier; a partial or ambiguous match goes to the reconciliation queue; an unknown sender is a Person in the lead compartment |
| SCN-12.2 | System | Runs the class-1 red-flag floor first: a red-flag word or the possible-emergency intent reaches the critical lane within 100 ms regardless of the classifier |
| SCN-12.3 | System | Classifies intent from the ratified taxonomy, urgency band and tone class, each with reliability; applies the routing rule fragment to a lane, queue and owner role, with a Task carrying intent and urgency; within 2 s |
| SCN-12.4 | Front-office staff (ROL-06) or clinician by lane | Opens the thread; sees the classification strip as flagged class-2 content; replies on the inbound channel |
| SCN-12.5 | System | On WhatsApp outside the 24-hour window, refuses free-form text and offers approved template fragments only |
| SCN-12.6 | System | Runs the outbound PHI check on the rendered reply: shows the redacted version for any identifier pattern or out-of-class clinical content; blocks a record number with no override; records an override as an act with reason and a channel surveillance signal |
| SCN-12.7 | Staff | For an unknown sender, drafts demographics from the conversation; mentioned conditions, medications and allergies become provisional patient-reported facts with span links only after conversion |

Outcome: every message laned by rule within budget, emergencies first, nothing leaving the system that the channel may not carry. Variations: email thread; call record from the voice line with transcript. Exceptions: classifier unavailable or retired (lanes by rule only; strip absent); provider outage (SCN-12 continues on the remaining channels; see section 8).

### SCN-13 After-hours call on the voice line (refines SIT-12; E2E-16)

Preconditions: telephony number bound; after-hours guidance fragment, hand-off cue list and IVR menus compiled; on-call escalation target in the profile. Trigger: an inbound call outside hours, or a scheduled outbound confirmation or check-in call.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-13.1 | Voice line (ROL-17) | Answers with the IVR menu in codebook terms; offers the consent prompt before any audio is stored |
| SCN-13.2 | Caller | Navigates by keypad or spoken keyword; states the reason for calling |
| SCN-13.3 | Voice line | Confirms identity by two identifiers before anything patient-specific; speaks the after-hours guidance fragment (what the service offers, where to go in an emergency) |
| SCN-13.4 | Voice line | For a booking, move or cancellation, applies the appointment type's class-1 rules against live availability, reads the confirmation back and sends it on the consented text channel |
| SCN-13.5 | Voice line | For a message, creates a Task with the transcript; for a clinical question, distress, a request for a person or repeated misunderstanding, hands off to on-call within one turn with warm transfer where the carrier supports it, or takes a message |
| SCN-13.6 | Voice line | On an emergency keyword, plays the emergency guidance fragment and emits the critical-lane event |
| SCN-13.7 | System | Files the call as a Communication with medium phone and, where consented, the transcript with spans; every dialogue turn passed the bounded-loop testers and the claims-boundary lint before synthesis |
| SCN-13.8 | Voice line | Next morning, places the outbound confirmation call as a loop step; a designed check-in speaks its form item by item and stores answers as QuestionnaireResponse with dialogue spans |

Outcome: calls answered at any hour, bookings made by rule, messages and hand-offs reaching a person, nothing clinical spoken that is not a released, signed argument. Exceptions: dialogue sidecar unavailable (IVR floor and message taking continue; fallback recorded); carrier outage (section 8).

### SCN-14 Form built and completed across transports (refines SIT-13; E2E-17)

Preconditions: form designer available on the governance face; calculator fragments and terminology edition pinned. Trigger: a clinical owner designs an intake form.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-14.1 | Clinical governance (ROL-07) | Arranges typed items, sets conditional rules from the fifteen operators, adds a formula citing the BMI calculator fragment, binds each field from the resource-template picker, previews in each register |
| SCN-14.2 | System | Compiles the form through the gates: refuses an unbound item or a binding to a non-existent path; publishes a pin on ratification; assigns the form to an appointment type |
| SCN-14.3 | Patient (ROL-01) | Completes the form on the phone portal; finishes the last items by IVR through the voice line |
| SCN-14.4 | System | Re-evaluates the conditional rules server-side on submit; assembles one transaction Bundle: QuestionnaireResponse with span index plus Observations, provisional Conditions and Consent with provenance patient-reported; stores the formula result as the calculator's Observation |
| SCN-14.5 | System | Renders older responses against their original pin after the form is republished |

Outcome: a form that is a compiled fragment, producing identical resources whichever transport carried the answer. Variations: public-audience form creating a Lead (SCN-11); clinician-audience form in session. Exceptions: formula disagreeing with the calculator fragment fails compile.

### SCN-15 Document archive intake (refines SIT-14; E2E-18)

Preconditions: fax gateway or archive source configured; OCR, layout and handwriting engines registered with benchmarks and pins; review queue staffed. Trigger: a 1,000-page archive, a scanner batch or a fax stream arrives.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-15.1 | System | Content-addresses each item; creates a batch with state and cursor; dedupes by hash |
| SCN-15.2 | System | Splits into documents with split reliability (whole item to the manual split queue when below floor); recognises each block, handwriting by its own engine; classifies the document type; parses sections; extracts fields with reliability; matches the patient by the probabilistic matcher; routes |
| SCN-15.3 | System | Writes facts with spans and capture context imported for fields above the floor; sends fields below the floor and every review-always field (medication doses, allergies) to the review queue grouped by document |
| SCN-15.4 | Reviewer (ROL-06 or clinician by field type) | Sees the image crop, recognised text and proposed code; accepts, amends or rejects as an act |
| SCN-15.5 | System | An accepted field becomes a fact at the review floor with the reviewer as principal; an extracted laboratory result becomes an unsolicited Observation and fires the same rules as a live result, including the critical lane |
| SCN-15.6 | System | Resumes a paused or interrupted batch from its cursor; a re-upload is idempotent; progress and per-document outcome visible |

Outcome: a backlog in the record with provenance, nothing below the floor filed as a fact without a person. Exceptions: patient match below threshold (SCN-05); handwriting engine retired (fields from it go to review; MOD-02).

### SCN-16 Campaign brief to published sequence (refines SIT-15; operation 21)

Preconditions: claims-boundary and plain-register lints compiled; consent scopes defined. Trigger: front office or governance files a typed campaign brief.

| Step | Actor | Action or response |
| --- | --- | --- |
| SCN-16.1 | Campaign owner (ROL-06 or ROL-07) | Files the brief as a typed form: audience (phenotype pin or lead filter), goal, offer, channels, cadence, spend, owner |
| SCN-16.2 | System | The bounded loop fills slot text only: landing-page copy, a message sequence and a nurture cadence as a loop fragment proposal, within 30 s |
| SCN-16.3 | System | Runs the claims-boundary and plain-register lints; rejects any cure, guarantee or outcome claim with the matching rule |
| SCN-16.4 | Clinical governance (ROL-07) | Ratifies the templates and the loop fragment through the compiler; publication is a pin |
| SCN-16.5 | System | At launch resolves the audience: excludes the deceased and anyone without the contact-for-programme scope; sends within the monthly allowance; records each touch for first- and last-touch attribution |

Outcome: outreach that is pinned, consent-checked and free of clinical claims. Exceptions: audience from a patient list where consent is absent for most members (launch proceeds for the consented subset and reports the exclusion count).

## 5. External interfaces

Derived from ConOps EXT-01 to EXT-12 and Volume 3A groups F, J, K. Owner is the party on the far side.

| Id | Interface | Direction | Crosses | Owner of the far side |
| --- | --- | --- | --- | --- |
| IF-01 | NHI and HPI (EXT-01) | Lookup, update of demographics | Patient identity and demographics; practitioner and facility identity | Health New Zealand \| Te Whatu Ora |
| IF-02 | HealthLink secure messaging (EXT-02) | Both | Referrals, letters, discharge summaries, results, handover; transport and application acknowledgements | HealthLink; sending and receiving organisations |
| IF-03 | Hira and NZIPS (EXT-03) | Both | Shared health summary and event summary upload; document retrieval | Health New Zealand |
| IF-04 | NZePS (EXT-04) | Both | Electronic prescriptions; dispense records | Health New Zealand; pharmacies |
| IF-05 | Laboratory and imaging results (EXT-05) | Inbound | Result messages matched to orders; TestSafe retrieval where available | Laboratories, radiology providers, regional repositories |
| IF-06 | Hospital systems (EXT-06) | Both | Discharge summaries in; escalation and handover out | Hospitals |
| IF-07 | Terminology edition (EXT-07) | Pinned import | SNOMED CT New Zealand edition releases | Health New Zealand as national release centre (to confirm in phase 4) |
| IF-08 | Patient channels: portal, SMS, email, print (WhatsApp through IF-16; telephony through IF-17) | Both | Consented communications with automated label; inbound replies parsed and triaged; the outbound PHI check on every send | Gateway vendors (deferred) |
| IF-09 | Video and phone sessions | Both | Session media bound to the encounter; recording only with consent | WebRTC provider (deferred) |
| IF-10 | Home device gateways (EXT-09) | Inbound | Time series with device identity, calibration status, sampling rate | Device and gateway vendors (deferred) |
| IF-11 | Identity providers (EXT-10) | Auth | Professional tokens binding registration and scope; consumer identity with proofing level; delegate grants | Councils and HPI; consumer identity provider (deferred) |
| IF-12 | Regulator bundle and offline verifier | Outbound | Signed archive of a time window with manifest and replay tooling | Medsafe, later TGA |
| IF-13 | Merkle anchor log (EXT-12) | Outbound | Ledger root hash with receipt | Provider open (D-08) |
| IF-14 | Private billing (EXT-11, resolved 25 Sep 2026) | Both | Invoices, payments and receipts for privately billed services; no claiming gateway in New Zealand for the first release; Australian claiming channels return with the TGA release | Payment provider (vendor deferred) |
| IF-15 | Ketryx (resolved 25 Sep 2026) | Both | Greenfield capture of every applicable standard for the planned regulatory applications: TGA, and possibly the FDA. Requirements, risks, verification evidence and the acceptance-test ids of this set trace into Ketryx; MET-02 and MET-06 targets are derived and captured there (PRD section 6). Standards proposed, pending confirmation: ISO 13485, IEC 62304, ISO 14971, IEC 62366-1, ISO 27001, IEC 81001-5-1 | Ketryx |
| IF-16 | WhatsApp Business provider (EXT-13; revision 2) | Both | Inbound and outbound messages on the practice's existing number in coexistence mode; template fragments with provider approval status; the 24-hour window per thread; delivery receipts | Provider open (D-14) |
| IF-17 | Telephony carrier (EXT-14; revision 2) | Both | Inbound and outbound calls on numbers per tenant and location; media to the voice sidecar; DTMF; warm transfer to on-call where supported; call records | Carrier open (D-15) |
| IF-18 | Fax gateway, scanner batches and archive exports (EXT-15; revision 2) | Inbound | Page images and PDF bundles, content-addressed on arrival; batch control | Gateway vendors (deferred) |
| IF-19 | Public front door (EXT-16; revision 2) | Inbound | Public-audience form submissions from the widget, QR pages and the booking link; creates Leads and Appointments on a lead's Person; red-flag fragment on enquiry text | The service's own website |

## 6. Data concept

Principal objects, where born, where persisted, retention. Derived from Volume 1A.1, 4.1, 5, 8, 3.3, 3A.9 and 2A.1.

| Id | Object | Born | Persisted | Retention |
| --- | --- | --- | --- | --- |
| DAT-01 | Fact (subject, predicate, object, assertion, time anchor, source span, extractor pin, reliability, consent) | Extraction from a document version, transcript, form or device stream | Fact graph tables; disagreement rows for conflicts | Never deleted; superseded |
| DAT-02 | Argument draft, attempt, actual argument | Engine, evaluator | Ledger, append-only, hash-chained | Never deleted; superseded by a new argument that names the old |
| DAT-03 | Act (accept, reject with reason, sign, override, deviation, break-glass) | A human principal | Ledger | Never deleted |
| DAT-04 | Order (drafted, checked, signed, transmitted, acknowledged, fulfilled, resulted, reconciled; overdue flag) | Clinician draft | Spine resources with transition acts | Never deleted |
| DAT-05 | Task, Communication (with automated label and reach-a-person route), Appointment | Rules, loops, staff | Spine resources | Never deleted |
| DAT-06 | QuestionnaireResponse with dialogue spans; patient-reported and device Observations | Pre-intake and loop agents, patient, devices | Spine resources with transcript or stream reference | Never deleted; recordings only with consent |
| DAT-07 | Consent resources and scopes | Patient | Spine; evaluated per request | Never deleted; withdrawal is an event |
| DAT-08 | Pin, fragment, template, threshold set, loss matrix, suppression policy, profile; from revision 2 also engagement loop, phenotype definition, form definition, routing rule and taxonomy, channel template, identifier pattern set, tokenisation policy, brand pack, cost schedule and programme contract (Volume 6.9) | Compiler | Pin registry, signed | Never deleted; superseded |
| DAT-09 | StudyDefinition, sealed envelope, enrolment, MeasureReport, evaluation-register entry | Governance and study owner | Ledger and reporting store | Never deleted; abandoned envelopes reported |
| DAT-10 | AuditEvent, SuppressionRecord, sentinel entry, drift record | Every request, brief, breach | Ledger | Never deleted |
| DAT-11 | Lead (Person with the lead extension; stage transitions; factor rows with points and rule pin; response-clock state; consent snapshot; converted patient id) (revision 2) | Any capture channel; the engagement rule fragment | Lead compartment of the spine; no read path for engines or the evaluator | Never deleted; linked to the Patient on conversion |
| DAT-12 | Thread and call record (Communication with medium whatsapp, sms, email or phone and a partOf chain; intent, urgency and tone labels with reliability; transcript DocumentReference with spans; PHI-check result and any override act) (revision 2) | Channels and the voice line | Spine resources; object store for audio with consent | Never deleted; audio only with consent |
| DAT-13 | Form definition (compiled fragment, also a Questionnaire with SDC extensions) and its response Bundle (QuestionnaireResponse with span index plus bound resources) (revision 2) | Form designer through the compiler; patient or staff submission | Pin registry; spine resources | Never deleted; responses render against their original pin |
| DAT-14 | Document batch (state, cursor, per-document outcome) and field review items (image crop, recognised text, proposed code, reliability, review act) (revision 2) | Archive, fax or scanner intake | Batch tables; review queue as a ledger view; facts on acceptance | Never deleted; originals content-addressed |
| DAT-15 | Campaign brief, drafts, published templates, loop fragment and touches (lead, campaign pin, step, channel, time) (revision 2) | Campaign owner; the drafting loop; the compiler | Pin registry for templates and fragments; touch table | Never deleted |

Retention policy (stated 25 Sep 2026): retention is the statutory minimum, which in New Zealand is the Health (Retention of Health Information) Regulations 1996, ten years from the last day of treatment, with the exact text confirmed in phase 4 sources. The ledger's never-delete rule exceeds the minimum; whether any destruction duty (Privacy Act 2020 principle 9) conflicts with never-delete is an assumption below.

## 7. User-facing performance expectations

Derived from Volume 3.2, 3.7, 1A.3 budgets and PRD metrics. Stated as the user would experience them; each applies to the scenario named.

| Id | Expectation | Scenario | Source |
| --- | --- | --- | --- |
| PERF-01 | The brief is ready before the session join and assembled in under 3 s | SCN-01, SCN-02 | 3.7; MET-08 |
| PERF-02 | A spoken or typed pre-intake answer is acknowledged in real time; a red flag reaches the practice queue within 100 ms of the answer | SCN-01 | 2A.1 |
| PERF-03 | Session facts appear within 2 s of utterance; differential updates within 500 ms | SCN-01 | 1A.3 |
| PERF-04 | A prescribing check returns in under 200 ms | SCN-01, SCN-06 | 3.2 |
| PERF-05 | Drafts of note, orders, letters and summary appear within 10 s of session end | SCN-01 | 1A.3 |
| PERF-06 | A promoted device breach raises a critical event within 100 ms; risk re-score completes within 10 s of fact commit | SCN-02, SCN-03 | 3A.11; 1A.3 |
| PERF-07 | An inbound document is classified, extracted and routed within 5 s; nothing unrouted for more than 24 h | SCN-04, SCN-05 | 3.2; MET-11 |
| PERF-08 | A follow-up task exists within 1 s of the plan being signed | SCN-01 | 1A.3 |
| PERF-09 | Nightly register and recall run completes within 30 min for 10,000 patients; a cohort query over a year in under 2 s | SCN-02, SCN-07 | 1A.3; 3.7 |
| PERF-10 | Writes under 10 ms, searches under 50 ms, terminology lookup under 1 ms at the 99th percentile | All | 3.7 |
| PERF-11 | Offline: an edge node sustains consulting for at least 8 h and flushes queued transactions in order on reconnect | SCN-10 | 3A.12 |
| PERF-12 | Availability and accuracy as the service would state them: deferred 25 Sep 2026 | All | |
| PERF-13 | A lead's response-clock state is current within 1 s of any message event; a breached clock shows on the owner's queue at once (revision 2) | SCN-11 | 1A.3 op 18 |
| PERF-14 | An inbound message is laned within 2 s; an emergency keyword or possible-emergency intent reaches the critical lane within 100 ms (revision 2) | SCN-12 | 1A.3 op 19; OMNI-01 |
| PERF-15 | The voice line begins its spoken response within the ratified turn latency and hands off within one turn of a cue (revision 2) | SCN-13 | 1A.3 op 20; VOX-02; PERF-02 lineage |
| PERF-16 | Document batch intake sustains 1,000 pages per hour on the reference machine and resumes without re-processing after interruption (revision 2) | SCN-15 | 1A.3 op 22; DAI-02 |
| PERF-17 | Campaign drafts appear within 30 s of filing the brief (revision 2) | SCN-16 | 1A.3 op 21 |

## 8. Failure, degraded and recovery behaviour

Derived from Volume 1A.7, 3A.12, 7.5, 9.6 and ConOps section 8.

| Failure | Behaviour | Recovery |
| --- | --- | --- |
| Class-2 engine drift | MOD-02: retire pin, class-1 fallback, sentinel entry, visible on disposition lines | New validated pin admitted; sentinel set replayed |
| Class-3 output fails the fidelity or entailment testers | Retry within the bounded loop; three failures yield no draft and a queue note | Clinician writes the item by hand |
| Voice sidecar unavailable | Agent offers the typed channel; fallback recorded | Sidecar restart; no loss of answers already stored |
| Connectivity loss | MOD-03 on an edge node; otherwise faces show stale-as-of time and refuse new attempts | Additive sync; queued transactions flush in order |
| Inbound signature or match failure | Quarantine or reconciliation queue; task raised; never filed | Staff act |
| Notification channel failure | Task created; next channel in the profile's escalation target | Channel restored |
| Store failure | Failover to the second region from continuous event-log shipping; subscribers resume from cursors | Point-in-time restore verified by ledger hash comparison; weekly drill |
| Suspected tampering | Per-patient hash chain and Merkle anchor detect it independent of encryption; sentinel entry | Restore to last verified commit; regulator informed per obligations |
| Attestation mismatch at start-up | The node refuses to serve | Redeploy the signed build |
| WhatsApp provider outage or template rejection (revision 2) | Threads stay in the desk; outbound falls back to SMS or email by consent; the template's approval status is shown; the response clock keeps running | Provider restored; queued sends flush within the window rules |
| Telephony carrier outage (revision 2) | Calls are not answered by the system; the carrier's own voicemail or diversion applies; scheduled outbound calls are rescheduled and a Task notes the gap | Carrier restored; loop steps resume |
| Dialogue sidecar unavailable on the voice line (revision 2) | The IVR floor continues: menus, identity confirmation, booking by keypad, message taking; no dialogue; fallback recorded | Sidecar restart |
| Intent classifier retired or unavailable (revision 2) | Lanes by the rule fragment and red-flag floor only; the classification strip is absent, not guessed (MOD-02) | New validated pin admitted |
| OCR, layout or handwriting engine retired (revision 2) | Affected fields go to the review queue; batches continue for the other engines | New pin with its own benchmark admitted |

## 9. What the system must never do

Derived from PRD non-goals, the ten laws, ConOps policies and Volume 2.1, 9.6, 2A.1. Each names the consequence it prevents.

| Id | Must never | Prevents |
| --- | --- | --- |
| MN-01 | Act on an order, prescription or plan without a signing clinician's act | Autonomous treatment (NG-01) |
| MN-02 | Show a held argument to any face, or a flagged one to a patient, or a released one to a patient before sign-off | Leaking an unreleased inference; patient acting on unreviewed advice |
| MN-03 | Present a class-2 or class-3 output as released advice, or generate an interruptive item from a class-3 engine | Model opinion masquerading as a control (Law 4, NG-04) |
| MN-04 | Convert, average or compare uncertainty signals across kinds, or fuse probabilities across engines | Un-auditable composite scores (Law 3, NG-03) |
| MN-05 | Evaluate an attempt without all eight pins, or admit knowledge except through the compiler | Irreproducible decisions; hand-edited rules (Laws 5, 6) |
| MN-06 | File an inbound item to a patient or order below the match threshold | Wrong-patient results |
| MN-07 | Ask a patient a question a documented fact already answers, or let the agent read another patient | Wasted intake; privacy breach |
| MN-08 | Send an automated message without the automated label and a reach-a-person route, or to a channel without consent, or urgent clinical detail by SMS | Patient deception; consent breach |
| MN-09 | Contact a patient for eligibility, or include them in an extract, without the consent scope | Research without consent |
| MN-10 | Suppress an interruptive item silently, or render fewer items than the budget without a suppression record | Hidden alerts (Law 9) |
| MN-11 | Delete or edit a ledger row, argument or act | Loss of audit; broken replay |
| MN-12 | Learn online in production, or let evaluation-zone artefacts reach training or knowledge except through the compiler | Drift without validation; contaminated evidence (NG-02, Law 10) |
| MN-13 | Rank patients or clinicians by a composite | Unaccountable league tables (NG-05) |
| MN-14 | Store or display a summed lead score, or feed a patient's clinical risk tier into an engagement rule (revision 2) | Triage by commercial value; a composite by another name (D-12, POL-16) |
| MN-15 | Send an outbound message that carries a record number, or free-form WhatsApp text outside the 24-hour window (revision 2) | Identifier leakage on consumer channels; provider policy breach (POL-17, POL-18) |
| MN-16 | Let the voice line answer a clinical question, act for a caller before identity is confirmed, or speak anything about a patient that is not a released, signed argument (revision 2) | Advice from a class-3 model; wrong-caller disclosure (POL-19) |
| MN-17 | Make a recognised field below the reliability floor, or of a review-always type, a fact without a review act (revision 2) | Mis-read archives becoming grounds (RSK-15) |
| MN-18 | Let a lead's communications become grounds, or create a Patient from a message or enquiry without a conversion act (revision 2) | Clinical reasoning over unverified people; duplicate patients (POL-16) |
| MN-19 | Publish campaign copy with a cure, guarantee or outcome claim, or send outreach to a person who opted out on any channel (revision 2) | Misleading health claims; consent breach (POL-20) |

## 10. Support, maintenance and operations concept

Derived from Volume 3A.12 and 11; the operating organisation is deferred in the ConOps.

| Aspect | Concept |
| --- | --- |
| Who runs it | Platform operator role (ROL-10) under the architecture owner; clinical governance (ROL-07) owns knowledge and policy; compliance (ROL-09) owns regulatory obligations. Which organisation staffs these roles, support hours and on-call: deferred 25 Sep 2026 |
| Release and change | Signed build with manifest and SBOM; profile is build-time; any pin change replays the sentinel decision set before admission; knowledge changes are compiler submissions with owner and ratifier signatures |
| Backup and restore | Continuous event-log shipping to a second region; point-in-time restore; weekly automated restore drill with hash comparison |
| Monitoring | Health endpoints per crate; drift monitor per engine per subgroup; sentinel board; latency suite on every build against the 10,000-patient synthetic practice |
| Incident handling | Sentinel entries and review queues on the governance face; break-glass with reason and act; obligations register drives regulator notification; from revision 2 the review queues include lead hand-offs, document intake fields, voice-line messages, PHI-check overrides and outreach breaches (Volume 10.5) |
| Providers (revision 2) | WhatsApp Business and telephony providers behind adapter traits; agreements, template approvals, data-processing terms and residency in the obligations register; selection owned by the platform operator before M5 (D-14, D-15) |
| Training and onboarding | MOD-05; role-based profiles; no training mode exists in the system |

## 11. Change requests to upstream

| Id | Target | Item | Change |
| --- | --- | --- | --- |
| OCR-01 | 01-prd.md; 02-conops.md | PRD CST-03, section 8.1 jurisdiction order; ConOps STK-07 | The FDA is a possible third regulator after Medsafe and the TGA (stated 25 Sep 2026 with the Ketryx scope). Add "possibly the FDA" to the jurisdiction order and to the regulator stakeholder row; device classification for the United States becomes a compliance item |
| OCR-02 | 01-prd.md | Section 6 MET-02, MET-06; section 13 | Ketryx scope resolved: standards capture and traceability for TGA and possibly FDA applications; targets for MET-02 and MET-06 captured there. Close the two Ketryx open questions |
| OCR-03 | 02-conops.md | EXT-11; PRD open question on billing | New Zealand billing scope resolved: private billing, no claiming gateway in the first release. Close the open question |

Revision of 15 Oct 2026: no new change request.

## 12. Assumptions

| Assumption | Confidence | How it would be checked |
| --- | --- | --- |
| A single edge node per site suffices for MOD-03 in HITH, where clinicians are mobile | Low | Phase 4 decides whether HITH mobile devices are edge nodes or thin clients |
| Voice pre-intake can meet PERF-02 on self-hosted hardware | Medium | Phase 4 turn-latency test on the chosen model |
| The Tier 3 build's class-3 review queues can be staffed by the launch workforce without adding a role | Medium | Queue volume measured in MOD-05 pilot |
| Never-delete does not conflict with Privacy Act 2020 principle 9 for health information held under the retention regulations | Medium | Compliance review in phase 4 |
| The proposed standards list for Ketryx is the right set for a Tier 3 SaMD application to the TGA and FDA | Low; proposed, not stated | Compliance confirms against the TGA essential principles and FDA guidance |
| The telephony carrier chosen under D-15 can stream call media to the self-hosted voice sidecar inside the trust boundary (CST-16) | Medium | Carrier selection before M5; media path test in phase 4 |
| Front-office staff can review intake fields for non-clinical document types; medication doses and allergies are reviewed by a clinician | Medium | Review-always rules per document type ratified by governance |

## 13. Open questions

- [x] Boundary: Mākoha is the system of record including scheduling and billing (section 1)
- [x] Roles: non-prescribing HITH nurse and identity administrator added (ROL-14, ROL-15)
- [ ] Confirm or rule out the proposed modes MOD-04 and MOD-05 (deferred)
- [ ] Availability and accuracy expectations as the service states them (PERF-12, deferred)
- [x] Retention: statutory minimum (section 6)
- [ ] Support organisation, hours and on-call (deferred)
- [x] IF-14 private billing and IF-15 Ketryx scope resolved; OCR-01 to OCR-03 raised
- [x] OCR-01 to OCR-03 approved and applied upstream 25 Sep 2026
- [ ] Confirm the proposed standards list for IF-15 {{TBD: standards list confirmation (deferred to compliance)}}
- [x] Revision 2 (15 Oct 2026): ROL-16 to ROL-18, SCN-11 to SCN-16, IF-16 to IF-19, DAT-11 to DAT-15, PERF-13 to PERF-17, MN-14 to MN-19 added; deferred modules (PRD section 8.1) not refined
- [ ] Which document types front-office staff may review and which need a clinician (SCN-15.4): ratified with the review-always rules before M5
