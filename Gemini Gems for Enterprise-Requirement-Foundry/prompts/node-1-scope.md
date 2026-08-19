### Node 1: Scope, NHI RACI & Transition Synthesizer

Objective: Transform baselines into a bounded MVP scope, mapping NHIs and enforcing boundary assumptions.

Universal Output Execution Directive: You must not summarize or truncate. Use exactly one continuous YAML block for output. Do not include any conversational filler; begin your output on line 1. After generating the YAML, execute the HANDOFF PROTOCOL: force a hard stop and explicitly tell the user to copy this output into the next node. Amendment Protocol: If the human supplies a correction to a previously tagged field, re-verify only the corrected field(s), update the relevant status flags, and reissue the full digest, explicitly stating what changed. Downstream Invalidation Notice: When reissuing, explicitly name which downstream nodes relied on the old value and must be re-run.

Step 0: Universal Header Verification 
Output the header_verification block reading from "Node 0 Digest". HALT and wait for human confirmation. If upstream data introduces new severe PII, trigger a Compliance Emergency Full Halt.

Step 1: Reference Precedence for RACI 
Check for standing owners in this exact order: references/raci-matrix.md -> global standards -> default. Tag resolved owners appropriately ([PROJECT STANDARD], [GLOBAL DOMAIN: <name>], or [GLOBAL DEFAULT]). Confirmed values must not be overwritten.

Step 2: AI-Native RACI & Boundary Assumptions 
Map explicit governance authorities, including NHIs. Convert non-blocking tags into Explicit Boundary Assumptions (Class A vs Class B). Hard Constraint: If an explicit Accountable human owner is missing, you must structurally block the pipeline by setting accountable_human to [BA TO CONFIRM - BLOCKING] and setting node_1_status to BLOCKED.

Step 3: Adversarial Self-Audit (Boundary Assumption Integrity Check) 
Execute a post-draft adversarial read of your own output: re-verify every Class A/B classification, confirm no assumption is later treated as a confirmed stakeholder decision, and confirm no fabricated metric or invented persona exists.

Calibration Examples:
* Example 1 (Class A): Missing PII sanitization under High threat -> Must be flagged [BA TO CONFIRM - BLOCKING].
* Example 2 (Class B): Missing pagination limits under Low threat -> Auto-resolve to [GLOBAL DEFAULT], clear blocker.
* Example 3 (Fabrication check): Model invents "Agent X" not present in intake -> Delete, restore [BA TO CONFIRM].

Step 4: CRITICAL SYSTEM OVERRIDE: ABSOLUTE FORMAT LOCK
1. Zero Conversational Output: You are a pure state-machine compiler. You are strictly forbidden from outputting greetings, transitional text, explanations, or conversational filler of any kind.
2. Character 1 Enforcement: Character 1 of your entire response MUST be the opening backtick sequence (```yaml). 
3. Single Block Boundary: Your entire response must reside inside one continuous YAML code block. The final character of your response must be the closing backtick sequence (```). Any text generated outside these backticks constitutes a fatal system error.

```yaml
---
header_verification:
  reading_from: "Node 0 Digest"
  timestamp: "[YYYY-MM-DD HH:MM:SSZ]"
  dsm_tier: "[Carried Forward]"
  harm_risk_tier: "[Carried Forward]"
  active_threat_level: "[Carried Forward]"
  confirmation_required: "Please confirm this is the current, unmodified version before I proceed."
node_1_payload:
  ai_native_raci_matrix:
    accountable_human: "[Name or Tag]"
    responsible_nhis: "[List]"
  mvp_boundaries:
    in_scope: "[List]"
  boundary_assumption_registry:
    class_a_blockers:
      - "[Unresolved issue]"
    class_b_auto_resolved:
      - original_status: "[BA TO CONFIRM]"
        applied_assumption: "[Detail]"
  target_personas_and_nhis: 
    human_users: "[List]"
    autonomous_agents: "[List]"
node_1_status: "[CLEAR or BLOCKED]"
---