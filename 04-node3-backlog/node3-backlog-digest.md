```yaml
jira_backlog_hierarchy:
  epic: "Project Astra - Clinical Data Mesh & Patient API MVP"
  features:
    - feature: "Real-Time Vitals Ingestion & FHIR Mapping"
      stories:
        - title: "Ingest live vitals from IoT hospital beds"
          full_text: "As a Clinician / Doctor, I want to receive a live stream of patient vitals from IoT hospital beds, so that I can monitor patient status during clinical rounds without delay."
        - title: "View FHIR R4-mapped vitals on dashboard"
          full_text: "As a Clinician / Doctor, I want to see patient vitals mapped to the FHIR R4 standard on my dashboard, so that the data displays consistently and can achieve the >99.9% successful payload mapping rate target."
        - title: "See stream connection status and reconnect state"
          full_text: "As a Clinician / Doctor, I want to see when the vitals stream has lost connection and is reconnecting, so that I know not to rely on stale data during an outage."

    - feature: "Secure Third-Party Reporting API Access"
      stories:
        - title: "Authenticate third-party reporting consumers via OAuth2 + mTLS"
          full_text: "As a [BA TO CONFIRM], I want to authenticate to the reporting API using OAuth2 credentials and an mTLS certificate, so that only authorized consumers can request clinical data, supporting the zero unauthorized access events per quarter target."
        - title: "Apply data masking to PHI/PII before returning reporting payloads"
          full_text: "As a [BA TO CONFIRM], I want the reporting API to apply data masking rules to PHI/PII before returning any payload, so that unauthorized exposure of patient data cannot occur and the system avoids a Class 1 HIPAA violation."
        - title: "Fail closed when masking cannot be verified"
          full_text: "As a [BA TO CONFIRM], I want the API to block the response and log a compliance alert when masking cannot be confirmed as applied, so that no raw PHI is ever returned by default."

node_3_status: "CLEAR"

dependency_map:
  - story: "Authenticate third-party reporting consumers via OAuth2 + mTLS"
    blocked_by: "[BA TO CONFIRM] — no confirmed end-user persona for reporting API consumer (Node 1 target_personas)"
  - story: "Apply data masking to PHI/PII before returning reporting payloads"
    blocked_by: "[BA TO CONFIRM] — exact masking rule set undefined (Node 1 Boundary Assumptions Registry: IN-SCOPE but spec not yet supplied); persona also unconfirmed"
  - story: "Fail closed when masking cannot be verified"
    blocked_by: "[BA TO CONFIRM] — same masking-spec and persona gaps as above; also depends on Security & Compliance domain (Accountable: Vishal) formally defining fail-closed alerting behavior"
```

```yaml
---
Digest: Node 3 Backlog
Timestamp: 2026-08-14 05:27:13Z
DSM_Tier: Medium
Upstream_Dependency: Node 2 UI Architecture Digest
---
```

==================================================
PIPELINE HANDOFF DIGEST
==================================================

```yaml
epic_name: "Project Astra - Clinical Data Mesh & Patient API MVP"
total_stories_sliced: 6
active_story_for_node_4: "As a [BA TO CONFIRM], I want the reporting API to apply data masking rules to PHI/PII before returning any payload, so that unauthorized exposure of patient data cannot occur and the system avoids a Class 1 HIPAA violation."
dependency_flags: 3
```

==================================================
HANDOFF
==================================================
node_3_status: CLEAR. The isolated story (highest dependency count + highest architectural/compliance risk: undefined masking spec, unconfirmed persona, and direct HIPAA exposure per the BRD's own Risk A) is "Apply data masking to PHI/PII before returning reporting payloads." Copy this ENTIRE response (the data payload + this digest) and paste it into Node 4.
