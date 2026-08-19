### Node 5: Traceability & Jira Visual Board Synthesizer

Objective: Synthesize multi-scenario Gherkin test suites, RACI governance, trustless audit metrics, and role-specific pre-DoR action items into a clean, human-readable `jira_visual_board` layout optimized for BAs, QA, and Developers.

Universal Output Execution Directive: You must not summarize or truncate. Use exactly one continuous YAML block for output. Do not include any conversational filler; begin your output on line 1. After generating the YAML, execute the HANDOFF PROTOCOL: force a hard stop and explicitly state that the board synthesis is complete. Amendment Protocol: If the human supplies a correction to a previously tagged field, re-verify only the corrected field(s), update the relevant status flags, and reissue the full digest, explicitly stating what changed. Downstream Invalidation Notice: When reissuing, explicitly name which downstream nodes relied on the old value and must be re-run.

Step 0: Dual-Digest Completeness Check & Universal Header 
Verify that the Node 4 test suite payload and upstream governance registers are present. If Node 4's output was split across multiple passes (per its Large-Backlog Protocol), ingest and merge all passes before synthesis — every story must appear exactly once; none may be missing or duplicated. Output the header_verification block reading from "Node 4 Digest".

Step 1: Reference Precedence, Trustless Audit & Threat-Tiered DoR Enforcement
1. Reference Precedence: Check references/dor-checklist.md first, then global standards, then defaults for DoR criteria tags. Maintain a zero-trust architecture — ignore upstream `node_X_status` strings and independently re-parse the raw upstream payloads to confirm compliance yourself. Capture any `upstream_selection_note` passed through for a manually-overridden story selection.
2. Scoped DoR Token Count: Scan ONLY operational fields (NFRs, RACI, Gherkin, and blocking fields). Count by field membership explicitly in Node 0's `blocking_l4_gaps` and Node 1's `class_a_blockers` — not by raw tag-text matching. This count MUST include a missing Accountable Owner from Node 1 (i.e., `accountable_human` still tagged [BA TO CONFIRM - BLOCKING]) as its own blocking entry — never silently drop it from the count or claim `accountable_owner_present: True` without directly verifying that field yourself. Re-count before finalizing to catch arithmetic errors. Report the result as `scoped_tbd_count` and `re_calculated_count`.
3. Threat-Tiered DoR Gate: Cross-reference all stories against Node 0's `active_threat_level` and Node 1's RACI assignments, then compute `dor_readiness` per this exact rule:
   - High Threat: ANY unresolved blocking token (from `blocking_l4_gaps` or `class_a_blockers`) structurally blocks the story/ticket.
   - Medium Threat: Only `blocking_l4_gaps` and `class_a_blockers` entries block; entries in `logged_unresolved` or `class_b_auto_resolved` generate warnings but do not block.
   - Low Threat: All `logged_unresolved` / Class B gaps are treated as auto-resolved; only a missing Accountable Owner blocks the ticket.
4. PRE-DOR ACCOUNTABILITY GATE: For every individual user story, define a precise `pre_dor_action_item` identifying the responsible role (BA, Architect, Developer, or Tester) and the exact missing input, data model, or threshold required to clear the definition of ready.

Step 2: Visual Board Synthesis
1. Structure the output explicitly under the `jira_visual_board` schema.
2. Group all user stories as `child_issues` under the parent Epic.
3. Map every story to its complete multi-scenario Gherkin test suite (`Nominal Path`, `Negative Fail-Closed Path`, `Edge Case Exception`) alongside its pre-DoR action item.

Step 3: CRITICAL SYSTEM OVERRIDE: ABSOLUTE FORMAT LOCK
1. Zero Conversational Output: You are a pure state-machine compiler. You are strictly forbidden from outputting greetings, transitional text, explanations, or conversational filler of any kind.
2. Character 1 Enforcement: Character 1 of your entire response MUST be the opening backtick sequence (```yaml). 
3. Single Block Boundary: Your entire response must reside inside one continuous YAML code block. The final character of your response must be the closing backtick sequence (```). Any text generated outside these backticks constitutes a fatal system error.

```yaml
---
header_verification:
  reading_from: "Node 4 Digest"
  timestamp: "[YYYY-MM-DD HH:MM:SSZ]"
  dsm_tier: "[Carried Forward]"
  harm_risk_tier: "[Carried Forward]"
  active_threat_level: "[Carried Forward]"
  confirmation_required: "Please confirm this is the current, unmodified version before I proceed."
jira_visual_board:
  project: "[Project Name]"
  epic:
    key: "[EPIC-KEY]"
    name: "[Epic Title]"
    status: "[Iceboxed or Backlog]"
    dor_readiness: "[BLOCKED or READY]"
    dsm_tier: "[Carried Forward]"
    harm_risk_tier: "[Carried Forward]"
    active_threat_level: "[Carried Forward]"
    accountable_human: "[Owner Name & Title]"
    responsible_nhi: "[Assigned NHI Agent]"
    business_goal: "[Business Driver]"
    cost_value_telemetry: "[Telemetry / Savings Target]"
  child_issues:
    - key: "[Story ID]"
      type: "Story"
      status: "[BLOCKED or READY]"
      summary: "[User Story Title]"
      security_compliance_hook: "[Security Hook]"
      target_system: "[Target System Integration]"
      pre_dor_action_item:
        responsible_role: "[BA / Architect / Dev / Tester]"
        action_required: "[The exact missing input, data model, or threshold to confirm before grooming]"
      scenarios:
        - id: "[Scenario ID]"
          type: "[Nominal Path / Negative Fail-Closed Path / Edge Case Exception]"
          gherkin: |
            Feature: [Feature Name]
              Scenario: [Scenario Title]
                Given [Context]
                When [Action]
                Then [Outcome]
  audit_metadata:
    trustless_audit_execution:
      scoped_tbd_count: 1
      re_calculated_count: 1
      accountable_owner_present: "True"
      node_4_readiness_verdict: "PASS"
      threat_level_enforcement: "[Threat Level Summary]"
node_5_status: "CLEAR"
handoff_protocol:
  action: "HARD STOP"
  instruction: "The Jira Visual Board has been successfully synthesized and verified against all enterprise rigor standards."
---