# Enterprise Requirement Foundry (Iteration 9.0): Operational Runbook & README

---

## 1. Executive Summary & Core Architecture

The **AI-Native Enterprise Requirement Foundry (Iteration 9.0)** transitions generative AI from an unconstrained, probabilistic utility into a strictly governed, mathematically deterministic enterprise engineering pipeline. Designed for Senior Business Analysts and Enterprise Architects, this 6-node sequential engine ingests raw business intake—ranging from brief executive concepts to 300-page Business Requirement Documents (BRDs)—and systematically transforms them into execution-ready, zero-hallucination Jira backlogs.

### Core Governing Principles

* **Maximal Precedence DSM × Harm Rule:** Automatically calculates the overarching `Active_Threat_Level` (`max(DSM_Tier, Harm_Risk_Tier)` on an ordinal scale of High > Medium > Low). High-threat projects mechanically trigger mandatory Human-in-the-Loop (HITL) approval consoles and absolute blocking on governance gaps.
* **Tiered Evidence Classification (L1–L4):** Categorizes non-functional requirements from explicit regulatory bounds (L1) down to unrecoverable ambiguities (L4), preventing trivial gaps from paralyzing high-velocity deployments.
* **Bifurcated Halt Severities:** Separates catastrophic data-sensitivity overflows (**Compliance Emergency Full Halt**) from subjective semantic fluff (**Quarantine-and-Continue Partial Halt**).
* **Zero-Trust Architecture & Sourcing Integrity:** Eliminates shadow AI and technical debt by enforcing strict Non-Human Identity (NHI) locks, persona source tracing, and independent validation loops.

---

## 2. Global Setup & Master Instruction Placement

To deploy the Enterprise Requirement Foundry, configure **six distinct custom Gems or assistant instances** within your workspace. Each instance operates as a specialized deterministic state machine.

| Node | Assigned Persona / Role | Primary Objective |
| --- | --- | --- |
| **Node 0** | Elite Enterprise Solutions Architect & AI Governance Lead | Preflight ingestion, DSM/Harm Genesis Gate, Large-Intake parsing, and L1–L4 NFR baseline validation. |
| **Node 1** | Elite Enterprise Business Analyst & AI Governance Lead | MVP scope partitioning, NHI RACI matrix mapping, and Class A/B boundary assumption calibration. |
| **Node 2** | Lead UX Architect & AI Systems Designer | Behavioral Mermaid.js flows, Hybrid GraphRAG/Semantic Cache mapping, workflow reconciliation, and HITL wireframes. |
| **Node 3** | Senior Agile Delivery Manager & AI Product Owner | INVEST user story mapping, AI governance slicing, and single-active-story isolation. |
| **Node 4** | Lead QA Automation Engineer & AI BDD Specialist | Exhaustive Gherkin scenario generation for non-deterministic AI exceptions (DLP, Validator blocks, Fallbacks). |
| **Node 5** | Lead Systems Analyst & AI Governance Delivery Manager | Trustless audit execution, scoped DoR math computation, and final Jira JSON payload synthesis. |

---

## 3. Reference Document Ingestion Matrix

To maintain organizational consistency across pipeline runs, place the following reference files in your repository or provide them to the corresponding node environments:

* **`references/nfr-standards.md` (Node 0):** Contains organizational performance baselines, security standards, and default metrics tagged as `[PROJECT STANDARD]`.
* **`references/raci-matrix.md` (Node 1):** Standing enterprise governance owners, compliance contacts, and information security authorities.
* **`references/dor-checklist.md` (Node 5):** Mandatory Definition of Ready (DoR) criteria tags and organizational readiness checklists.

---

## 4. End-to-End Sequential Workflow & Handoff Protocol

Because chat-based LLM nodes operate independently, the pipeline relies on **Manual Handoff via Continuous YAML Blocks**.

```
[Raw Intake / BRD] 
       │
       ▼
┌──────────────┐      Copy Entire      ┌──────────────┐      Copy Entire      ┌──────────────┐
│    Node 0    │ ────────────────────► │    Node 1    │ ────────────────────► │    Node 2    │
│  (Preflight) │     YAML Output       │ (Scope/RACI) │     YAML Output       │  (UI / Flow) │
└──────────────┘                       └──────────────┘                       └──────────────┘
                                                                                     │
                                                                                     ▼
┌──────────────┐      Copy Entire      ┌──────────────┐      Copy Entire      ┌──────────────┐
│    Node 5    │ ◄───────────────────  │    Node 4    │ ◄───────────────────  │    Node 3    │
│(Jira Payload)│     YAML Output       │  (BDD QA)    │     YAML Output       │ (Backlog S.) │
└──────────────┘                       └──────────────┘                       └──────────────┘

```

### Universal Handoff Instructions

1. **No Conversational Filler:** Every node output begins strictly on line 1 inside a single, continuous `yaml` code block.
2. **The Hard Stop:** After generating the YAML state digest, the model enforces a hard stop and instructs the operator to copy the output into the next node.
3. **Zero-Trust Inbound Reading:** Downstream nodes independently re-evaluate inbound payloads and ignore unverified status strings, maintaining absolute architectural integrity.

---

## 5. Advanced Protocols

### 1. Large-Intake Protocol (Node 0)

When ingesting extensive documentation (200+ page BRDs or structured specs):

* **Structural Inventory First:** Node 0 halts NFR extraction to output a section map with a one-line summary per section for human sign-off.
* **Section-by-Section Processing:** Extracts data sequentially against the confirmed map, accumulating partial digests.
* **Completeness Manifest:** The final YAML digest logs explicitly which sections were processed and which were deferred.

### 2. Workflow Reconciliation (Node 2)

When the human operator supplies an external reference workflow (e.g., Miro, Visio, meeting notes):

* **Independent-First Generation:** Node 2 generates its Mermaid flow purely from Node 1's digest first to prevent anchoring.
* **Divergence Report:** Runs a secondary comparison pass outputting a structured table: `Point of Difference → AI's Version → User's Version → Why They Differ → Recommended Resolution`. The human operator makes the final call per tradeoff.

### 3. Batch QA Mode vs. Single-Story Mode (Nodes 3, 4, 5)

* **Default Mode (Single-Story Deep-Dive):** Isolates the single highest-risk compliance story for exhaustive scrutiny.
* **Batch QA Mode (Nodes 4 & 5):** When invoked, Node 4 loops through every story in Node 3's backlog, executing the full BDD rigor stack per story (with a visible tradeoff notice regarding the per-story adversarial rigor budget). Node 5 then aggregates these into a multi-issue JSON array (`"issues": [...]`) complete with a `batch_qa_manifest` tracking processed vs. un-QA'd backlog items.

---

## 6. Definition of Ready (DoR) & Trustless Payload Synthesis

Node 5 performs the terminal mathematical audit before SCM/Jira import:

* **Scoped Token Counting:** Scans exclusively operational fields (`blocking_l4_gaps`, NFRs, RACI, Gherkin syntax) for unresolved tags.
* **Threat-Level Gate Enforcement:**
* **High Threat:** Any unresolved token structurally blocks the ticket.
* **Medium Threat:** Unresolved Class A gaps and entries in `blocking_l4_gaps` block the ticket; `logged_unresolved` items generate warnings without blocking.
* **Low Threat:** Class B gaps auto-resolve; only a missing Accountable Owner halts readiness.


* **Execution Verdict:** Outputs either `"READY FOR SPRINT"` or `"BLOCKED"` within a clean Jira-ready JSON schema envelope.
