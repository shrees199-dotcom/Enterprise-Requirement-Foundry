**SCOPE NOTE:** This digest covers all 6 stories sliced in Node 3, per explicit user request, rather than Node 4's standard single-story Isolation Protocol. Only Story 4 ("Apply data masking to PHI/PII before returning reporting payloads") is Node 3's actual rubric-selected active story (highest dependency/risk count). Stories 1, 2, 3, 5, and 6 are supplemental coverage generated outside the normal isolation rule, at user direction.

==================================================
STORY 1 — "Ingest live vitals from IoT hospital beds"
Persona: Clinician / Doctor (confirmed)
==================================================

[Happy Path]
Given the Clinician / Doctor's dashboard is connected to an active IoT hospital bed stream
When a new vitals reading is transmitted from the bed
Then the dashboard displays the newly received vitals value
And the displayed value matches the value transmitted by the device

[Negative Path — Malformed Payload]
Given the dashboard is connected to an active IoT hospital bed stream
When the bed transmits a payload that does not conform to the expected schema
Then the dashboard does not display the malformed value as if it were valid
And the malformed payload is logged for review

[Edge Case — Simultaneous Multi-Bed Streams]
Given the Clinician / Doctor is viewing vitals from multiple IoT beds simultaneously
When two beds transmit new readings at the same time
Then each bed's vitals update independently and correctly, with no cross-bed data mixing

==================================================
STORY 2 — "View FHIR R4-mapped vitals on dashboard"
Persona: Clinician / Doctor (confirmed)
==================================================

[Happy Path]
Given raw vitals telemetry has been received from an IoT hospital bed
When the telemetry is mapped to the FHIR R4 standard
Then the dashboard displays the vitals in FHIR R4-conformant structure
And the mapped payload matches the source telemetry values exactly

[Negative Path — Mapping Failure]
Given raw vitals telemetry has been received from an IoT hospital bed
When the payload fails to map to the FHIR R4 standard due to a schema mismatch
Then the dashboard does not display an unmapped or malformed value
And the dashboard shows the stale-data fallback state instead
And the mapping failure is logged

[Edge Case — Mapping Success Rate Verification]
Given a batch of 1,000 vitals payloads is processed through the FHIR R4 mapping layer
When mapping completes for the batch
Then the successful mapping rate for the batch is measurable and traceable to the >99.9% successful payload mapping rate target stated in Node 1's ROI targets
And any payload below this threshold is flagged for review rather than silently discarded

==================================================
STORY 3 — "See stream connection status and reconnect state"
Persona: Clinician / Doctor (confirmed)
==================================================

[Happy Path — Reconnect Succeeds]
Given the connection status indicator displays "Live"
When the IoT bed stream disconnects and then reconnects successfully
Then the connection status indicator transitions "Live" -> "Connection Lost" -> "Live"
And the vitals stream resumes displaying current data

[Negative Path — Reconnect Fails]
Given the connection status indicator displays "Reconnecting"
When the reconnect attempt fails
Then the connection status indicator changes to "Connection Lost"
And the dashboard displays the stale-data indicator with the last-successful-sync timestamp

[Edge Case — Maximum Reconnect Attempts / Backoff Behavior]
Given the connection status indicator displays "Connection Lost"
When reconnect attempts continue to fail
Then [PERFORMANCE ASSERTION BLOCKED - NFR unresolved in Node 0, cannot verify a numeric bound for max attempts, backoff interval, or timeout duration; not stated anywhere upstream]

==================================================
STORY 4 — "Apply data masking to PHI/PII before returning reporting payloads"
Persona: [BA TO CONFIRM] — NODE 3's ACTUAL RUBRIC-SELECTED ACTIVE STORY
==================================================

[Happy Path]
Given an authenticated third-party reporting consumer has passed OAuth2 + mTLS verification
When the consumer requests a reporting payload containing PHI/PII
Then the returned payload has all defined PHI/PII fields masked per the applicable masking rules
And no raw/unmasked PHI or PII field is present in the response

[Negative Path — Masking Rule Application Fails]
Given an authenticated third-party reporting consumer has passed OAuth2 + mTLS verification
When the masking process fails to apply to one or more PHI/PII fields in the payload
Then the system does not return the partially-masked or unmasked payload
And the response is blocked (fail-closed) rather than returned with any unmasked field

[Edge Case — Undefined Masking Rule for a Given Field]
Given a reporting payload contains a data field for which no masking rule has been explicitly defined
When the system attempts to construct the response
Then [PERFORMANCE ASSERTION BLOCKED - NFR unresolved in Node 0, cannot verify a numeric bound] is not applicable here since this is a rules-completeness gap, not a timing gap — instead: the system must fail closed and withhold the field rather than return it unmasked by default
And this scenario is flagged: "[BA TO CONFIRM] — exact masking rule set for all PHI/PII fields is undefined in Node 1's Boundary Assumptions Registry; this scenario asserts fail-closed default behavior only, not the completeness of any specific rule set"

==================================================
STORY 5 — "Authenticate third-party reporting consumers via OAuth2 + mTLS"
Persona: [BA TO CONFIRM]
==================================================

[Happy Path]
Given a reporting consumer presents a valid OAuth2 credential and a valid mTLS certificate
When the consumer requests access to the reporting API
Then access is granted
And the granted access event is logged

[Negative Path — Invalid Credential or Certificate]
Given a reporting consumer presents an invalid OAuth2 credential or an invalid/expired mTLS certificate
When the consumer requests access to the reporting API
Then access is denied
And the denied access event is logged, contributing to the zero unauthorized access events per quarter target stated in Node 1's ROI targets

[Edge Case — Valid Credential, Invalid Certificate (Mismatch)]
Given a reporting consumer presents a valid OAuth2 credential but an invalid mTLS certificate
When the consumer requests access to the reporting API
Then access is denied
And the denial reason distinguishes certificate failure from credential failure in the log entry

==================================================
STORY 6 — "Fail closed when masking cannot be verified"
Persona: [BA TO CONFIRM]
==================================================

[Happy Path — Masking Verified]
Given a reporting payload has completed the masking process
When the system verifies that masking was successfully applied to all required fields
Then the payload is released to the requesting consumer

[Negative Path — Masking Verification Fails]
Given a reporting payload has completed the masking process
When the system cannot verify that masking was successfully applied to all required fields
Then the response is blocked and no payload is returned
And a compliance alert is logged for the blocked event

[Edge Case — Verification Check Itself Errors]
Given a reporting payload has completed the masking process
When the masking-verification check itself fails to execute (e.g., verification service unavailable)
Then the system treats this as a verification failure by default and fails closed
And no payload is returned despite the underlying masking possibly having succeeded

```yaml
qa_edge_risk_registry:
  - "Mock: IoT bed multi-stream simulation (Story 1)"
  - "Mock: malformed/non-schema-conformant vitals payload (Story 1, 2)"
  - "Mock: FHIR R4 mapping failure injection (Story 2)"
  - "Environment state: 1,000-payload batch harness to measure mapping success rate against >99.9% target (Story 2)"
  - "Mock: IoT bed disconnect/reconnect event sequences, success and failure (Story 3)"
  - "[BA TO CONFIRM] max reconnect attempt count / backoff strategy (Story 3) — unresolved upstream"
  - "Mock: OAuth2 + mTLS valid/invalid/expired credential and certificate combinations (Story 4, 5)"
  - "[BA TO CONFIRM] complete PHI/PII masking rule set per field (Story 4) — unresolved upstream, Node 1 Boundary Assumption IN-SCOPE but undefined"
  - "Mock: masking-verification service failure/unavailability injection (Story 6)"
```

```yaml
---
Digest: Node 4 QA (Full Backlog Coverage)
Timestamp: 2026-08-14 05:31:57Z
DSM_Tier: Medium
Upstream_Dependency: Node 3 Backlog Digest
---
```

==================================================
PIPELINE HANDOFF DIGEST (PER STORY)
==================================================

```yaml
stories_covered: 6
rubric_selected_active_story: "Apply data masking to PHI/PII before returning reporting payloads"
readiness_by_story:
  - story: "Ingest live vitals from IoT hospital beds"
    ready_for_tech_elaboration: "YES"
  - story: "View FHIR R4-mapped vitals on dashboard"
    ready_for_tech_elaboration: "YES"
  - story: "See stream connection status and reconnect state"
    ready_for_tech_elaboration: "BLOCKED: VAGUE ACCEPTANCE CRITERIA"
  - story: "Apply data masking to PHI/PII before returning reporting payloads"
    ready_for_tech_elaboration: "BLOCKED: VAGUE ACCEPTANCE CRITERIA"
  - story: "Authenticate third-party reporting consumers via OAuth2 + mTLS"
    ready_for_tech_elaboration: "BLOCKED: VAGUE ACCEPTANCE CRITERIA"
  - story: "Fail closed when masking cannot be verified"
    ready_for_tech_elaboration: "BLOCKED: VAGUE ACCEPTANCE CRITERIA"
```

==================================================
HANDOFF
==================================================
Readiness is computed per story, mechanically: any story whose Persona field is [BA TO CONFIRM], or that contains a [PERFORMANCE ASSERTION BLOCKED] scenario, is BLOCKED. Stories 1 and 2 (confirmed Clinician/Doctor persona, no unresolved numeric assertions) compute to YES. Stories 3, 4, 5, and 6 compute to BLOCKED — 3 for an unresolved reconnect-limit NFR, and 4/5/6 because their persona is still [BA TO CONFIRM] from Node 3. Node 5's Definition of Ready check should read the rubric-selected story (Story 4) as the canonical input; the others are supplemental. Copy this ENTIRE response (the data payload + this digest) and paste it into Node 5.
