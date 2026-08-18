---
Digest: Node 2 UI Architecture (Compliance-Hardened)
Timestamp: 2026-08-17 20:02:00Z
DSM_Tier: Medium
Upstream_Dependency: Node 1 Scope Synthesis
---
<scratchpad>
1. DIGEST PARSING: Extracted DSM_Tier (Medium), objective ("Aggregate clinical trial data and sync real-time patient vitals across regional hospitals via a secure FHIR R4 data mesh"), and in-scope boundaries (real-time IoT vitals ingestion, FHIR R4 mapping, secure OAuth2/mTLS API for third-party reporting tools). Target personas include "Clinical Staff / Doctors", "Third-Party Reporting Tools" (which lacks a confirmed human persona and must be marked `[BA TO CONFIRM — no named human persona]`), and "Clinical Operations Managers".
2. NEGATIVE SPACE INTERROGATION: Identified that "Third-Party Reporting Tools" is an automated tool/system consumer, not a human persona; applied the persona lock constraint. Identified missing technical contracts around legacy data migration ownership (`[BA TO CONFIRM]`) and unassigned data masking rules for PHI/PII transit. Enforced strict fail-closed boundaries: any mTLS handshake failure, expired token, or undefined/failed data masking rule must halt outbound data, lock access, and log a critical compliance security alert.
3. ERROR-STATE GOVERNANCE: Mapped explicit operational failure modes including stale-data fallback states for IoT bed telemetry drops, schema mapping mismatches, and cryptographic or authentication handshake blockades under HIPAA/HITRUST mandates.
</scratchpad>

```yaml
node_2_status: "CLEAR"

wireframes:
  - screen_id: "SCR-01"
    screen_name: "Real-Time Patient Vitals Dashboard"
    bound_persona: "Clinical Staff / Doctors"
    header: "Live Regional Hospital Vitals Stream"
    cta_elements:
      - "Filter by Hospital Unit"
      - "Acknowledge Critical Alert"
    data_elements:
      - "Patient ID (Masked PHI)"
      - "Bed Number"
      - "Heart Rate (FHIR Observation)"
      - "SpO2 Level"
      - "Stream Timestamp"
    error_states:
      - "Connection Lost: Stale-data fallback banner active (explicit unrefreshed visual indicator)"
      - "Data Mapping Error: Schema mismatch / malformed payload fallback — [BA TO CONFIRM: exact error message copy]"

  - screen_id: "SCR-02"
    screen_name: "Clinical Operations & Mesh Monitoring Console"
    bound_persona: "Clinical Operations Managers"
    header: "FHIR R4 Data Mesh Operations"
    cta_elements:
      - "Export Ingestion Logs"
      - "Restart Ingestion Pipeline"
    data_elements:
      - "Total Connected IoT Beds"
      - "FHIR R4 Mapping Latency"
      - "Active Data Sync Nodes"
      - "Error Rate Percentage"
    error_states:
      - "Mesh Node Unreachable: Fallback Mode Active, compliance audit log updated"

  - screen_id: "SCR-03"
    screen_name: "Third-Party API Integration Portal"
    bound_persona: "BA TO CONFIRM — no named human persona in Node 1"
    header: "OAuth2 & mTLS Consumer Management"
    cta_elements:
      - "Generate mTLS Certificate"
      - "Revoke OAuth2 Token"
    data_elements:
      - "Client ID"
      - "Certificate Expiry Date"
      - "API Request Rate (req/sec)"
      - "Token Scope Status"
    error_states:
      - "Access Denied: Invalid mTLS handshake or expired token [FAIL-CLOSED: no raw data returned]"
      - "Access Blocked: Data masking rule undefined or failed execution [FAIL-CLOSED: system halts outbound payload, locks access, and logs critical HIPAA compliance alert]"

behavioral_flows:
  - flow_name: "Real-Time IoT Vitals Ingestion and Fallback State Machine"
    mermaid_sequence: |
      sequenceDiagram
      autonumber
      Clinical Staff / Doctors->>System: Open Dashboard
      System-->>Database: Query Telemetry
      Database-->>System: Return Stream
      System->>System: Map to FHIR R4
      alt Mapping Success
          System-->>Clinical Staff / Doctors: Render Live Feed
      else Mapping Failure / Schema Mismatch
          System-->>Clinical Staff / Doctors: Display Stale-Data Fallback Banner
          System->>System: Log Schema Anomaly for Compliance Review
      end

  - flow_name: "Secure Consumer Data Request & Fail-Closed Gate"
    mermaid_sequence: |
      sequenceDiagram
      autonumber
      Third-Party Reporting Tools->>System: Initiate API Request
      System->>System: Verify mTLS & OAuth2 Token
      alt Authentication Failed
          System-->>Third-Party Reporting Tools: Access Denied (Fail-Closed)
      else Authentication Valid
          System->>System: Evaluate Data Masking Rules for PHI/PII
          alt Masking Rules Applied Successfully
              System-->>Third-Party Reporting Tools: Return Masked FHIR Payload
          else Masking Rule Undefined or Failed
              System->>System: Trigger Fail-Closed Blockade & Security Alert
              System-->>Third-Party Reporting Tools: Access Blocked (No Raw Data Exposed)
          end
      end

ux_edge_cases:
  - id: "EC-01"
    description: "IoT bed telemetry stream disconnects due to regional hospital network lag; stale-data fallback indicators must activate immediately to prevent clinical misinterpretation."
    classification: "RACE"
  - id: "EC-02"
    description: "Data masking rules for secondary reporting tool ingestion are undefined or experience execution failure; system must enforce fail-closed blockade and halt outbound PHI transmission."
    classification: "GAP"
  - id: "EC-03"
    description: "Third-party reporting tool consumer lacks a confirmed human persona in upstream synthesis scope boundaries."
    classification: "BA_TO_CONFIRM"