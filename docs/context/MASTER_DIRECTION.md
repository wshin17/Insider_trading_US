# MASTER DIRECTION
## Insider_trading_US

## 1. Project mission

This repository is a US-first long-horizon research platform for studying insider selling, disclosure behavior, and multimodal inconsistency around executive communication.

The goal is not to build a one-off script for a single paper.
The goal is to build a reusable research system that can support:
- multiple papers
- repeated experiments
- continuous literature review
- continuous data collection
- later server-side execution and automation

## 2. Core research idea

The central idea of this project is:

Use insider-selling events in the US market as anchors, then attach multiple disclosure modalities to those events, and study whether cross-modal inconsistency helps identify opportunistic insider selling risk better than single-modality signals.

This project should NOT be framed as generic lie detection.

Preferred framing:
- opportunistic insider selling risk
- abnormal executive selling risk
- cross-modal inconsistency around insider selling events
- disclosure inconsistency and future risk

## 3. Core event definition

The main analysis unit is not a raw filing and not a raw conference call.

The main analysis unit should be a US insider-selling event.

Working definition:
- one issuer
- one reporting owner
- one security
- one sale or one sale cluster
- linked to nearby filings, disclosures, and conference call material

Suggested internal name:
`us_sale_cluster_event`

All later data collection, feature engineering, and multimodal linking should revolve around this event object.

## 4. Strategic principles

### 4.1 SEC-first
The project starts from official and reproducible US disclosure sources first.

### 4.2 Event-first, not modality-first
We do not start from audio research or video research in isolation.
We start from insider-selling events, then attach text, audio, and later video.

### 4.3 Data-first, then method, then modeling
We do not finalize methods before understanding actual source availability and field coverage.

### 4.4 Build the core stack before extensions
Phase 1 focuses on:
- insider transaction data
- SEC filing text
- earnings call transcript
- earnings call audio

Video, websites, news, and social data are later extensions.

### 4.5 Multi-paper friendly
Every design choice should support future paper tracks, not just one empirical test.

## 5. Phase order

## Phase 0. Repository and project scaffold
### Objective
Build the project shell and working rules.

### Why
A long-running research assistant needs persistent structure.

### Main outputs
- repository scaffold
- README
- AGENTS
- literature folders
- docs/context
- initial skills

### Next
Move to source intelligence and data collection planning.

## Phase 1. US source intelligence and data collection planning
### Objective
Define exactly what data should be collected first, from where, at what grain, and for what later use.

### Why this phase exists
This project starts from zero on the data side.
Without a clear source plan, later schema, event logic, and modeling decisions will drift.

### Main outputs
- `docs/context/us_data_strategy.md`
- `docs/context/data_collection_plan.md`
- `docs/context/source_registry_us.md`
- `docs/context/field_dictionary_us.md`
- `docs/context/data_questions.md`

### What belongs here
- identify Phase 1 core sources
- separate Phase 1 core sources from later optional sources
- define manual-first versus scripted-later collection
- define raw/interim/processed storage targets
- define expected identifiers and data grain

### Exit criteria
This phase is complete when:
- the Phase 1 source priority is locked
- collection order is clear
- the first-pass field dictionary exists
- major unresolved data questions are explicitly listed

### Next
Move to identifier strategy and event ontology.

## Phase 2. US identifier strategy and event ontology
### Objective
Define how data from different sources will be joined and what the core event object is.

### Why this phase exists
Without stable identifiers, multimodal matching is unreliable.

### Main outputs
- `docs/context/identifier_strategy_us.md`
- `docs/context/event_ontology_us.md`
- `docs/context/modality_registry_us.md`
- `docs/context/labeling_policy_us.md`

### Exit criteria
This phase is complete when:
- the project has one explicit event definition
- the main identifiers are documented
- a worked example of one event can be described end to end

### Next
Move to pilot acquisition.

## Phase 3. Pilot data acquisition
### Objective
Collect a small but high-quality pilot sample before any full-scale crawl.

### Why this phase exists
We need to test access, coverage, matching, and storage assumptions before scaling.

### Priority order
1. insider transaction source
2. SEC disclosure text
3. conference-call transcript
4. conference-call audio
5. structured market and accounting data

### Exit criteria
This phase is complete when:
- a pilot sample can be downloaded repeatedly
- transaction, filing, transcript, and audio links exist for a meaningful subset
- access issues and missingness are documented

### Next
Move to canonical schema and data audit.

## Phase 4. Canonical schema, ingestion, and data audit
### Objective
Map the pilot data into a standardized schema and quantify what is actually usable.

### Main outputs
- canonical tables or table specs
- source-to-schema mapping
- coverage matrix
- missingness report
- `docs/context/data_onboarding_log.md`

### Exit criteria
This phase is complete when:
- the schema can represent the pilot sample cleanly
- coverage and data-quality problems are explicit
- matching failure modes are known

### Next
Move to literature-guided recalibration.

## Phase 5. Literature-guided recalibration after pilot onboarding
### Objective
Use actual pilot data constraints plus literature knowledge to refine methods.

### Questions to resolve here
- what exactly is the event window
- what benchmark windows are useful
- what weak labels are feasible
- which text layer matters most
- whether audio should start from presentation, QA, or both
- whether video is still worth a later phase

### Next
Move to code milestones.

## Phase 6. Engineering milestones

## M1. Schema-first synthetic skeleton
Build the minimum config, schema, and smoke path without assuming real production data.

## M2. Provenance and auditability
Track where each event and linkage came from.

## M3. Real-data onboarding
Replace synthetic assumptions with real pilot data.

## M4. First feature slice
Build the smallest useful event-level features.

## M5. Weak-label and review logic
Create early event-level soft labels or ranking heuristics.

## M6. Baseline modeling and evaluation
Build the first reproducible ranking baseline.

## Phase 7. Multimodal expansion
### Objective
Expand beyond the core stack only after the SEC-centered pipeline is stable.

### Candidate extensions
- company websites
- investor relations pages
- archived webpages
- news coverage
- video

## Phase 8. Multi-paper and experiment platform
### Objective
Turn the repository into a reusable research platform for multiple papers and repeated experiments.

## 6. What is Phase 1 core and what is deferred

## Phase 1 core
- insider transaction sources
- SEC filing text
- earnings call transcripts
- earnings call audio
- structured market and accounting data

## Deferred to later
- video as a core modality
- full website crawling as a core layer
- social media
- end-to-end deep multimodal model
- cloud automation and MCP
- large-scale server workflow orchestration

## 7. Working research directions

These are not final paper hypotheses.
They are working research directions.

### H1
Transaction-side abnormality already contains useful signal for insider-selling risk.

### H2
SEC text and conference-call text provide incremental signal beyond transactions alone.

### H3
Conference-call audio provides incremental signal beyond transaction and text.

### H4
Cross-modal inconsistency is more informative than any single modality alone.

### H5
Video may provide additional signal, but only after the core text and audio event pipeline is stable.

## 8. Codex execution protocol

Codex should follow these rules:

1. Read this file before major planning or implementation tasks.
2. Stay within the current phase unless explicitly told to move on.
3. Do not skip from early planning directly to advanced modeling.
4. Prefer small, reviewable deliverables.
5. At the end of each substantial task:
   - summarize files changed
   - summarize commands run
   - summarize open questions
6. Update the project status file after each completed phase or milestone.
7. Treat data availability and data quality as first-class research constraints.

## 9. Current project position

Current priority:
Phase 1, US source intelligence and data collection planning.

This means the immediate next work is:
- lock the source priority
- define the field dictionary
- define unresolved data questions
- prepare for identifier and event design

This means we should NOT yet:
- build a full real-data pipeline
- engineer large feature sets
- define final weak labels
- build multimodal deep models
- treat video as mandatory

## 10. Near-term success condition

The near-term success condition is not to run a model.

The near-term success condition is:
- a clear SEC-first source map
- a stable event definition direction
- a pilot data acquisition plan
- a canonical schema direction
- a realistic path from raw source to first baseline
