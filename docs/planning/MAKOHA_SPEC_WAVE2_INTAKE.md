# Mākoha Specification Repository — Wave 2 Intake Assessment

**Repository:** <https://github.com/Arepo-Medtech/makoha-spec>  
**Original source:** <https://github.com/Kenny-bytes/makoha-spec>  
**Reviewed baseline:** `974352d` (`main`, 25 September 2026)  
**Assessment date:** 26 September 2026  
**Decision:** Accept as a high-value candidate design baseline; qualify and reconcile it before execution or regulatory reliance.

## Executive read

This repository supplies the project-specific context that the project-agnostic AI-native SaMD CDSS SDLC needs. It contains a coherent product-to-validation chain, a substantial architecture compendium, 176 active specific requirements plus 11 withdrawn identifiers, 176 planned validation entries, and a traceability export containing 767 identifiers (768 lines including its header). Its `docpipe` mechanism is useful as a requirements compiler and controlled document generator.

Phase 7 records product-owner approval with conditions for construction. This assessment recommends reconciling that baseline with the Wave 2 execution controls; it does not revoke the recorded construction approval. Document finalisation is distinct from completed product validation or clinical release approval. The repository marks all seven phases final and approves M1–M4 while carrying 25 unresolved markers, one open change request, five residual risks awaiting acceptance, unnamed clinical/compliance/architecture authorities, and no completed validation evidence. The evidence pack explicitly says the pipeline is only “shape-compatible” with IEC 62304 and is not a QMS. Its regulatory citations are not yet strong enough for regulated reliance.

The correct role is therefore **design authority under qualification**, feeding the regulated SDLC after reconciliation. Jira/Ketryx remains the controlled requirements, risk, verification and approval record; Linear remains engineering execution; GitHub remains code, review, merge and immutable build-evidence provenance; Symphony orchestrates policy; Devin and other coding agents execute bounded work.

## What is strong

- Seven linked phases: PRD, ConOps, OpsCon, technical specification, requirements, validation plan and approval record.
- Explicit EARS-style requirements and machine-generated traceability.
- Content hashing and downstream-staleness propagation when an upstream document changes.
- A detailed architecture corpus with stable identifiers, interfaces, acceptance tests and milestone concepts.
- Strong engineering concepts for provenance, signed manifests, SBOMs, replay, model/knowledge pins, deterministic evaluation and build-time regulatory profiles.
- A stated Ketryx interface for requirements, risks, verification evidence, acceptance results and controlled targets.
- New Zealand-first and Australia-second sequencing is represented. The repository describes FDA as a possible third market; the established SDLC brief requires planning for all three from greenfield, so this scope difference needs explicit reconciliation.

## Baseline blockers and corrections

### 1. “Final” does not mean closed

`docpipe status` reports every phase final, but phases 1–5 contain 25 `{{TBD...}}` markers. Phase 7 knowingly approves these as conditions. `docpipe finalise --force` allows checks to be bypassed, so the frontmatter status cannot be treated as approval evidence by itself.

**Control:** introduce distinct lifecycle states: `draft`, `reviewed`, `conditionally-approved`, `approved`, `obsolete`. A document with open markers, unresolved high-risk change requests, missing required approvers or unaccepted residual risk cannot become `approved`. Force-finalisation must create a recorded deviation with owner, rationale, expiry and approval.

### 2. Validation coverage is not validation completion

The validation plan covers the requirement identifiers, but all 176 validation entries are marked incomplete. This is useful planning evidence, not verification or validation evidence.

**Control:** keep separate fields and gates for requirement coverage, test implementation, test execution, result, reviewer approval, build/version applicability and evidence integrity. Ketryx should calculate these states from linked evidence rather than infer completion from document coverage.

### 3. Regulatory evidence needs authoritative sources and jurisdiction-specific pathways

The repository's `docpipe/EVIDENCE.md` relies partly on Wikipedia and practitioner summaries for IEC 62304 and does not implement ISO 14971 or IEC 62366-1 artefacts. The applicable standards list is explicitly proposed and awaits compliance confirmation.

The New Zealand WAND timing is supported by Medsafe: notification is required within 30 calendar days of becoming sponsor. The future Medical Products Bill and its SaMD/AI direction are supported by New Zealand Ministry of Health materials, but dates, transition assumptions and obligations must remain monitored rather than frozen as product facts.

Australia requires an intended-purpose and function-by-function assessment. A medical-device CDSS generally requires ARTG inclusion unless excluded or exempt; advanced analysis, diagnosis or treatment recommendations are unlikely to fit the limited-function exemption. TGA announced clarification amendments effective 1 November 2026. The project must not derive an Australian classification from the repository's internal “Tier 3” label.

For the United States, add the FDA device/non-device CDS analysis, software submission content, cybersecurity, clinical evidence, human factors, quality-system and AI-enabled device change strategy. The FDA PCCP pathway must be tied to the actual deployed model-change policy.

**Control:** establish a jurisdictional regulatory determination record in Ketryx, approved by the compliance authority, with intended purpose, claims, users, patient state, outputs, decision significance, device status, classification rationale and submission route for each market.

### 4. The orchestration pipeline is absent

The corpus mentions Ketryx extensively but contains no Jira, Linear, Devin or Symphony operating model. It therefore defines product intent and architecture, not the Wave 2 work-control pipeline.

**Control:** add a controlled mapping layer rather than embedding mutable work-management state in specification prose:

`spec identifier → Jira controlled item → Ketryx requirement/risk/test → Linear execution issue → GitHub branch/PR/commit/build → Ketryx evidence and Jira status`

Jira and Linear remain bidirectional for permitted fields. Regulatory approvals, risk acceptances, controlled requirement text and released evidence remain Jira/Ketryx-owned and are read-only mirrors in Linear.

### 5. GitHub PRs and merges do not need to route through Jira

GitHub should remain the direct PR and merge path. Each branch, commit and PR must carry the controlled Jira key and mapped specification/requirement identifiers. Ketryx consumes GitHub development evidence directly and uses Jira for controlled work and traceability. Jira should never proxy or duplicate the Git object lifecycle.

Required merge gates should include tests, code review, Copilot review as advisory evidence, security/supply-chain checks, traceability completeness, Ketryx impact analysis, required human approvals and signed build provenance. Merge permission stays with the designated release/merge mechanism.

### 6. Repository governance is not production-grade

- The original public repository was duplicated into `Arepo-Medtech/makoha-spec` on 26 September 2026. Both branches and their Git history were preserved and their hashes verified; organisation ownership of the copy is complete.
- No licence is declared.
- No CI workflow is present.
- Git history includes source pull request #1. The independent organisation copy did not import GitHub PR discussions, issues or repository settings; link source review records when qualifying the baseline.
- The shell regression suite fails on macOS at S6 because it uses GNU-style `sed -i`; this blocks the remaining test cases on the stated workstation even though S1–S6 pass.
- Root compendium/source files and `docs/ref` create potential duplication and ambiguity.

**Control:** retain the source-to-organisation provenance link and establish governance for the organisation copy; add CODEOWNERS, protected branches, signed commits/tags, CI, licence/proprietary notice, release tags, provenance attestations and a declared canonical path for every duplicated document.

## Proposed source hierarchy for Wave 2

The following is a proposed reconciliation policy, not an established approval or an instruction to override controlled records. Resolve conflicts using scope, version, approval and evidence; code describes implemented behaviour but cannot silently redefine approved product intent. Use this order as a starting point:

1. Applicable law, regulator guidance and controlled QMS procedures.
2. Approved Ketryx requirements, risks, controls, tests, approvals and released evidence.
3. Jira controlled work items and decisions, including their comment history.
4. Accepted GitHub code, PR review, test/build evidence and release artefacts.
5. Approved Confluence design and decision records.
6. This repository at a pinned commit, after item-level qualification.
7. Linear execution state and agent working notes.

Lower sources may propose changes to higher sources; they do not silently override them.

## Wave 2 intake sequence

1. **Pin and register the source.** Register commit `974352d`, repository owner, visibility, provenance and corpus inventory in Jira/Ketryx.
2. **Create a Baseline Qualification epic in Jira.** Do not create implementation work directly from all 767 identifiers.
3. **Reconcile identifiers.** Match each active requirement, decision, risk, interface and acceptance test to existing Jira, Ketryx, Confluence and GitHub evidence. Classify each as confirmed, superseded, duplicate, conflicted, unsupported or new.
4. **Resolve authority gaps.** Name product, clinical safety, quality/regulatory, security/privacy, architecture and release authorities. Obtain explicit risk and baseline decisions.
5. **Close release-blocking uncertainty.** Separate deferred design values from unresolved safety/regulatory requirements. Assign owner, due gate and impact.
6. **Perform jurisdictional determinations.** Complete New Zealand, Australian and US records using current primary sources and intended-use language.
7. **Import controlled records into Ketryx.** Preserve source identifiers and pinned-commit provenance. Import requirements, risks, controls, verification methods and acceptance tests as separate typed objects.
8. **Create Jira control items.** Jira holds the controlled change package, approvals and cross-system identities. Establish the allowed bidirectional field map to Linear.
9. **Generate bounded Linear work.** Create tasks only for the first accepted vertical slice or hardening objective, with requirement/risk/test links and explicit evidence expectations.
10. **Execute through Symphony.** Symphony assembles approved context, checks policy and dispatches Devin/Codex/Cursor/Claude/Rovo work. Agents receive the minimum complete context bundle and cannot approve their own regulated output.
11. **Prove the loop with one pilot.** Run one requirement through Jira/Ketryx → Linear → GitHub PR → CI/evidence → Ketryx verification → Jira closure before scaling.
12. **Scale by risk and value.** Iterate, refactor, harden and optimise. Preserve accepted work when it still carries its weight; replace or redesign it when evidence shows material inadequacy, missing capability, load failure, safety risk or a clearly superior controlled solution.

## First pilot recommendation

Choose a narrow, deterministic, already-implemented or nearly implemented capability with:

- one clear intended-use statement;
- one or two controlled requirements;
- an identified hazard/risk control;
- a reproducible automated test;
- no unresolved clinical model claim;
- an existing GitHub implementation candidate;
- a reviewable evidence package.

The pilot's objective is to validate the operating pipeline, identifiers, permissions and evidence return path. It is not to demonstrate the entire architecture.

## Acceptance criteria before the corpus becomes an execution baseline

- Repository governance and authoritative location decided.
- All active identifiers reconciled or explicitly dispositioned.
- Regulatory determination records approved for the current intended purpose.
- Required authorities named and role segregation implemented.
- Open markers and change requests assigned to gates with approved dispositions.
- Risk management, usability engineering, clinical evaluation, cybersecurity and AI/model-change controls linked into Ketryx.
- Jira–Linear field ownership and loop-prevention rules tested.
- GitHub–Ketryx evidence capture tested without routing merges through Jira.
- One end-to-end pilot passes with immutable, reviewable evidence.
- `docpipe` CI runs cross-platform and blocks invalid approval states.

## Primary regulatory references checked on 26 September 2026

- Medsafe, [The WAND Database](https://www.medsafe.govt.nz/regulatory/DevicesNew/3WAND.asp)
- New Zealand Ministry of Health, [Documents on the Medical Products Bill](https://www.health.govt.nz/regulation-legislation/medicines-legislation/regulating-medicines-medical-devices-and-natural-health-products/documents-on-the-medical-products-bill)
- New Zealand Ministry of Health, [Innovative medical products and regulatory pathways to market](https://www.health.govt.nz/regulation-legislation/our-legislation/regulatory-documents/innovative-medical-products-and-regulatory-pathways-to-market)
- TGA, [Understanding clinical decision support system software regulation](https://www.tga.gov.au/resources/guidance/understanding-clinical-decision-support-system-software-regulation)
- TGA, [Clinical decision support system exemption amendments](https://www.tga.gov.au/news/news-articles/clinical-decision-support-system-exemption-amendments)
- FDA, [Medical Device Software Guidance Navigator](https://www.fda.gov/medical-devices/regulatory-accelerator/medical-device-software-guidance-navigator)

