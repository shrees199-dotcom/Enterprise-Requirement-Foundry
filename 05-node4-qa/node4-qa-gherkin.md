**NOTE: MANUAL OVERRIDE.** Node 3's Story Isolation Rubric designated "Apply data masking to PHI/PII before returning reporting payloads" as the active story. This digest instead processes "See stream connection status and reconnect state" per explicit user override — not a rubric-based selection. Treat this digest as non-canonical relative to the pipeline's normal isolation protocol.

1. BDD ACCEPTANCE CRITERIA

[Happy Path — Reconnect Succeeds]
Given the Clinician / Doctor is viewing the Live Vitals Dashboard with an active IoT bed stream
And the connection status indicator displays "Live"
When the IoT bed stream disconnects
Then the connection status indicator changes to "Connection Lost"
And a reconnect attempt begins automatically
And when the reconnect succeeds, the connection status indicator changes back to "Live"
And the vitals stream resumes displaying current data

[Happy Path — Stale Data Flagged During Reconnect]
Given the connection status indicator displays "Reconnecting"
When the dashboard is still showing the last received vitals values
Then the dashboard visibly marks the displayed vitals as "Stale" or equivalent explicit non-live indicator
And the last-successful-sync timestamp is displayed alongside the stale data

[Negative Path — Reconnect Fails]
Given the connection status indicator displays "Reconnecting"
When the reconnect attempt fails
Then the connection status indicator changes to "Connection Lost"
And the system automatically initiates another reconnect attempt
And the dashboard continues to display the stale-data indicator from the prior scenario

[Negative Path — Repeated Reconnect Failures]
Given the connection status indicator displays "Connection Lost"
And a previous reconnect attempt has already failed at least once
When a subsequent reconnect attempt also fails
Then the connection status indicator remains "Connection Lost"
And the system logs the repeated failure event
And the displayed vitals remain marked "Stale" with the original last-successful-sync timestamp unchanged

[Edge Case — Reconnect Succeeds Mid-Transition]
Given the connection status indicator displays "Reconnecting"
When the underlying IoT bed stream re-establishes a connection at the exact moment a new reconnect attempt is triggered
Then the connection status indicator changes to "Live" exactly once, with no duplicate or conflicting status shown
And the "Stale" data indicator is cleared

[Edge Case — Maximum Reconnect Attempts / Backoff Behavior]
Given the connection status indicator displays "Connection Lost"
When reconnect attempts continue to fail
Then [PERFORMANCE ASSERTION BLOCKED - NFR unresolved in Node 0, cannot verify a numeric bound (e.g., max attempt count, backoff interval, or timeout duration) in QA; no reconnect-attempt-limit or backoff NFR was stated in the raw intake or resolved in Node 0's NFR Baseline]

2.

```yaml
qa_edge_risk_registry:
  - "Mock: IoT bed stream disconnect event (simulated mid-session)"
  - "Mock: reconnect success response"
  - "Mock: reconnect failure response (single and repeated)"
  - "Environment state: dashboard pre-loaded with a prior successful vitals sync timestamp before disconnect is triggered"
  - "[BA TO CONFIRM] exact UI copy/labels for 'Connection Lost', 'Reconnecting', and 'Stale' states — not specified in any upstream digest, scenarios above use placeholder state names"
  - "[BA TO CONFIRM] maximum reconnect attempt count and/or backoff strategy — no NFR or business rule defines this upstream"
```

```yaml
---
Digest: Node 4 QA
Timestamp: 2026-08-14 05:30:14Z
DSM_Tier: Medium
Upstream_Dependency: Node 3 Backlog Digest
---
```

==================================================
PIPELINE HANDOFF DIGEST
==================================================

```yaml
target_story: "As a Clinician / Doctor, I want to see when the vitals stream has lost connection and is reconnecting, so that I know not to rely on stale data during an outage."
gherkin_scenarios: 6
qa_edge_risks: 6
ready_for_tech_elaboration: "BLOCKED: VAGUE ACCEPTANCE CRITERIA"
```

==================================================
HANDOFF
==================================================
ready_for_tech_elaboration computed as BLOCKED: one scenario ("Maximum Reconnect Attempts / Backoff Behavior") contains a [PERFORMANCE ASSERTION BLOCKED] flag because no reconnect-limit or backoff NFR was ever resolved upstream. This is a mechanical computation, not a judgment call — Node 5 will read this value as-is. This digest is also a manual override of Node 3's rubric-selected story; flag this to Node 5 explicitly. Copy this ENTIRE response (the data payload + this digest) and paste it into Node 5.
