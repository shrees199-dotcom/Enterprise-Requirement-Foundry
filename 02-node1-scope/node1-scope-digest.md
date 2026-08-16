---
Digest: Node 1 Scope
Timestamp: 2026-08-14 05:19:09Z
DSM_Tier: Medium
Upstream_Dependency: Node 0 Preflight Digest
---

```yaml
node_1_status: "CLEAR"
project_name: "Project Astra - Clinical Data Mesh & Patient API"
target_milestone: "MVP — real-time vitals ingestion + FHIR R4 mapping + secure third-party reporting API"

executive_intake:
  business_context: "Enterprise data mesh aggregating clinical trial data and syncing patient vitals across regional hospitals, discovery phase."
  core_drivers:
    - "Real-time ingestion of patient vitals from IoT hospital beds"
    - "Mapping data to the FHIR R4 standard"
    - "Secure API exposure for third-party reporting tools"
  roi_targets:
    - "Successful payload mapping rate > 99.9%"
    - "Zero unauthorized access events per quarter"
    - "API adoption by at least 3 regional hospitals within 60 days of launch"

raci_matrix:
  - domain: "Overall Business Sponsorship"
    accountable: "Mark (VP of Clinical Innovation)"
    accountable_source: "[CONFIRMED]"
    responsible: []
    consulted: []
    informed: ["Internal Support / Operations / Sales"]
  - domain: "Delivery / Enterprise Integration"
    accountable: "Mark (VP of Clinical Innovation)"
    accountable_source: "[CONFIRMED]"
    responsible: ["Silva (Head of Enterprise Integration)"]
    consulted: ["Srimant Sahu (Discovery Lead / Lead BA)"]
    informed: []
  - domain: "Technical Architecture (data mesh design, FHIR R4 mapping)"
    accountable: "Mihaa"
    accountable_source: "[CONFIRMED]"
    responsible: ["NOT ASSIGNED — Principal Systems Architect role still stated as vacant in original roster; Mihaa confirmed as Accountable, execution Responsible seat not yet named"]
    consulted: ["Srimant Sahu (Discovery Lead / Lead BA)"]
    informed: []
  - domain: "Security & Compliance (HIPAA, data masking, access control)"
    accountable: "Vishal"
    accountable_source: "[CONFIRMED]"
    responsible: ["Neha (Principal InfoSec Engineer) — security controls execution"]
    consulted: ["Nakish"]
    informed: []
  - domain: "Product / Clinical Portals"
    accountable: "Mark (VP of Clinical Innovation)"
    accountable_source: "[CONFIRMED]"
    responsible: ["Srihari (Clinical Portals PM)"]
    consulted: ["Aksh (Head of Clinical Operations)"]
    informed: []
  - domain: "QA & Test Automation"
    accountable: "Mark (VP of Clinical Innovation)"
    accountable_source: "[CONFIRMED]"
    responsible: ["Praneeth (Automation & Test Director)"]
    consulted: []
    informed: []
  - domain: "Legacy Data Migration (batch vs. event-driven, unresolved)"
    accountable: "Srimant"
    accountable_source: "[CONFIRMED]"
    responsible: []
    consulted: ["Aksh (Head of Clinical Operations)", "Vijay (External Vendor API Gateway Tech Lead)"]
    informed: []
  - domain: "External Vendor / API Gateway Integration"
    accountable: "Mark (VP of Clinical Innovation)"
    accountable_source: "[CONFIRMED]"
    responsible: ["Vijay (API Gateway Partner Tech Lead)"]
    consulted: ["Silva (Head of Enterprise Integration)"]
    informed: []

accountable_owner_status: "CONFIRMED: Mark (VP of Clinical Innovation) — overall project; Mihaa, Srimant, and Vishal now confirmed as domain Accountables for Architecture, Legacy Migration, and Security & Compliance respectively. All three prior Class A blockers resolved."
blocking_items: []

mvp_scope_boundaries:
  in_scope_phase1:
    - "Real-time ingestion of patient vitals from IoT hospital beds"
    - "Mapping ingested data to the FHIR R4 standard"
    - "Secure API for third-party reporting tools, including data masking controls (see Boundary Assumptions Registry)"
    - "OAuth2 + mTLS security layer for all API traffic"
  deferred_phase2:
    - "[BA TO CONFIRM] — no explicitly named Phase 2 items in the raw intake; nothing has been deferred beyond MVP without a stated basis"
  target_personas:
    - "Clinician / Doctor (explicit: 'so doctors don't experience lag' during clinical rounds; live ICU telemetry consumer)"
    - "[BA TO CONFIRM] — end-user type for third-party reporting API consumers not explicitly named in intake (referred to only as 'third-party reporting tools' / 'third-party analytics vendors', not a named human persona)"

boundary_assumptions_registry:
  - item: "Data masking requirements for third-party reporting dashboard"
    original_status: "[BA TO CONFIRM]"
    applied_assumption: "IN-SCOPE"
    justification: "BRD's own Risk A explicitly ties masking failure to a Class 1 HIPAA violation, making masking a mandatory MVP control rather than a deferrable extension. The exact masking rule set remains open pending the Compliance Officer/Accountable role being filled and BA follow-up (per intake's own Action 2) — the capability is scoped in, the detailed spec is not yet defined."
  - item: "Technical Architecture execution ownership (Responsible seat)"
    original_status: "[BA TO CONFIRM]"
    applied_assumption: "IN-SCOPE"
    justification: "Mihaa is now confirmed Accountable for this domain, resolving the Class A blocker. The Principal Systems Architect Responsible/execution seat is still stated as vacant in the original roster — logged here as a non-blocking follow-up (Class B) since an Accountable owner now exists to direct the work, distinct from the earlier Class A gap of no owner at all."
```

==================================================
RESOLUTION & HANDOFF
==================================================
node_1_status: CLEAR. Copy this ENTIRE response (the data payload + this digest) and paste it into Node 2.
