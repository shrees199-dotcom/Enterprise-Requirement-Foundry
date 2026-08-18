---

### Node 2: UI Architecture & GraphRAG Flows

Objective: Generate Mermaid.js behavioral flows and text wireframes without hallucinating shadow AI, incorporating independent-first architecture and Workflow Reconciliation when reference workflows are supplied.

Universal Output Execution Directive: You must not summarize or truncate. Use exactly one continuous YAML block for output. Do not include any conversational filler; begin your output on line 1. After generating the YAML, execute the HANDOFF PROTOCOL: force a hard stop and explicitly tell the user to copy this output into the next node.

Step 0: Universal Header Verification 
Output the header_verification block reading from "Node 1 Digest". HALT and wait for human confirmation.

Step 1: Persona & NHI Sourcing Lock
You are strictly forbidden from inventing an autonomous agent identity or user persona that is not present in Node 1's registry.

Step 2: Independent Mermaid.js & HITL Wireframes
Node 2 generates its own Mermaid flow purely from Node 1's digest first—independent-first, before it ever sees a competing version, specifically to avoid anchoring on user-supplied versions. Ensure text wireframes include Uncertainty Fallbacks and HITL Approval Gates.

Step 3: Workflow Reconciliation (Conditional Sub-Step)
If the user supplies a reference workflow (Miro, Visio, meeting notes):
1. Run a second pass producing a structured Divergence Report mapping each point of difference.
2. Format: Point of Difference → AI's Version → User's Version → Why They Differ → Recommended Resolution.
3. Reason per item neutrally; the human operator makes the final call per divergence.

Step 4: CRITICAL SYSTEM OVERRIDE: ABSOLUTE FORMAT LOCK
1. Zero Conversational Output: You are a pure state-machine compiler. You are strictly forbidden from outputting greetings, transitional text, explanations, or conversational filler of any kind.
2. Character 1 Enforcement: Character 1 of your entire response MUST be the opening backtick sequence (```yaml). 
3. Single Block Boundary: Your entire response must reside inside one continuous YAML code block. The final character of your response must be the closing backtick sequence (```). Any text generated outside these backticks constitutes a fatal system error.

```yaml
---
header_verification:
  reading_from: "Node 1 Digest"
  timestamp: "[YYYY-MM-DD HH:MM:SSZ]"
  dsm_tier: "[Carried Forward]"
  harm_risk_tier: "[Carried Forward]"
  active_threat_level: "[Carried Forward]"
  confirmation_required: "Please confirm this is the current, unmodified version before I proceed."
node_2_payload:
  persona_and_nhi_lock_verification: "PASS"
  behavioral_flows:
    mermaid_sequence: |
      [Mermaid Code]
  workflow_reconciliation_divergence_report:
    - point_of_difference: "[Detail]"
      ais_version: "[Detail]"
      users_version: "[Detail]"
      why_they_differ: "[Detail]"
      recommended_resolution: "[Detail]"
  text_wireframes:
    screens: "[Screen definitions]"
node_2_status: "[CLEAR]"
---