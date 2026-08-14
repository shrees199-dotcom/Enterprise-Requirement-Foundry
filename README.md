
## Executive Overview & Architectural Philosophy

The **Enterprise Requirement Foundry** is a zero-infrastructure, platform-agnostic specification engine for Product Managers, Lead Business Analysts, and Enterprise Architects.

Unlike conventional AI tools that generate unconstrained narrative text or fabricate non-existent technical contracts, the Foundry operates on three strict architectural invariants:

1. **The Zero-Inference Imperative:** The engine never fabricates API endpoints, database schemas, or qualitative non-functional requirements (NFRs). Unsupplied data is explicitly tagged using standard fallback tokens (`[BA TO CONFIRM]` or `[ARCHITECT TO SUPPLY]`).
2. **Hard Circuit Breakers:** Three mechanisms can stop this pipeline moving forward, and they don't all behave the same way. **Step 0's DSM Classification Gate** is a true full halt — nothing else is generated until the human answers. **Node 0's DSM-Tier Escalation Rule** and **Node 1's missing-Accountable-owner check** work differently: the full analysis is still generated and shown in both cases — architectural dependencies, NFR baseline, RACI, scope, everything — only the handoff instruction to the next node is withheld until the human resolves the blocking item(s). The Escalation Rule specifically fires only when an NFR has no evidence at any tier (L4) *and* DSM_Tier is High; the same L4 gap under Medium or Low DSM is logged and carried forward, not blocking. NFRs matching a recognized industry standard (Tier L2) or strongly implied by other stated facts (Tier L3) never reach any of this — they're generated and tagged for later confirmation.
3. **Progressive State Digest Handoffs:** Nodes communicate exclusively via immutable Markdown state files saved directly to the local directory structure, ensuring 100% auditability and context window optimization.

---

## Repository Directory Layout

```text
Enterprise-Foundry/
├── README.md                  # Operational Runbook & Command Matrix
├── prompts/                   # Canonical System Instructions (Portable Logic)
│   ├── node-0-preflight.md    # Technical Pre-Flight & Numeric NFR Rules
│   ├── node-1-scope.md        # Scope, RACI & Boundary Assumption Protocol
│   ├── node-2-ui.md           # Mermaid Flows & UI Wireframe Rules
│   ├── node-3-backlog.md      # INVEST Slicing & Active Story Lock
│   ├── node-4-qa.md           # Gherkin BDD Engine (Happy/Negative/Edge)
│   └── node-5-jira.md         # Zero-Debt Jira Ticket Synthesizer
├── references/                # Org-specific standards — ACTIVELY INGESTED, not just documentation
│   ├── global-standards.md    # Populated core knowledge vault — Domain-Specific NFR Matrix, Universal RACI role-types, DSM thresholds, Universal DoR checklist (Nodes 0, 1, 5)
│   ├── dor-checklist.md       # Per-engagement DoR criteria override (Node 5) — empty until a specific project needs to add its own
│   ├── nfr-standards.md       # Per-engagement NFR override (Node 0) — empty until a specific project needs to add its own
│   └── raci-matrix.md         # Per-engagement standing Accountable owners (Node 1) — empty until a specific project needs to add its own
├── 00-raw-inputs/             # Raw PDFs, meeting notes, transcripts, RFPs
├── 01-node0-preflight/        # Output for Pre-flight audit report & Quarantine digests
├── 02-node1-scope/            # Output for Bounded MVP scope, RACI matrix & assumptions
├── 03-node2-ui/               # Output for Mermaid.js behavioral diagrams & wireframes
├── 04-node3-backlog/          # Output for INVEST Story hierarchy & Active Story selection
├── 05-node4-qa/               # Output for Exhaustive Given/When/Then BDD test suites
└── 06-node5-jira/             # Output for Production-ready Jira ticket payload

```

---

## The 6-Node Assembly Line Pipeline

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    NODE 0    │ ──> │    NODE 1    │ ──> │    NODE 2    │
│ Pre-Flight   │     │ Scope & RACI │     │  UI & Flow   │
└──────────────┘     └──────────────┘     └──────┬───────┘
                                                 │
                                                 │
        ┌────────────────────────────────────────┘
        ▼
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    NODE 3    │ ──> │    NODE 4    │ ──> │    NODE 5    │
│ Backlog Slic │     │  BDD Engine  │     │ Jira Payload │
└──────────────┘     └──────────────┘     └──────────────┘

``` 
1. **Node 0 (Pre-Flight & NFR Baseline):** Rejects qualitative statements (e.g., "fast", "scalable") with no supporting basis, and enforces numeric SLAs (MTTR <= 30 min, CFR < 5%) — either stated directly, drawn from a recognized industry standard, or strongly implied by other stated facts. An NFR with no basis at any tier is logged and carried forward — it only blocks the handoff to Node 1 if the project's DSM tier is High.
2. **Node 1 (Scope & RACI Synthesis):** Establishes single Accountable sign-off and applies the Boundary Assumption Protocol to clear non-blocking scope gaps.
3. **Node 2 (UI Architecture & Behavioral Flows):** Renders Mermaid sequence diagrams, ASCII wireframes, and unmapped race conditions.
4. **Node 3 (Backlog Slicing & Single-Story Lock):** Enforces INVEST criteria and isolates exactly one high-risk story for downstream elaboration.
5. **Node 4 (BDD QA Engine):** Generates full Gherkin test suites covering Happy Path, Negative Path, and Edge Cases.
6. **Node 5 (Dev Handover Payload):** Synthesizes upstream digests into an Atlassian Jira payload with binding Definition of Ready (DoR) and Definition of Done (DoD) gates.

---

## Operational Command Matrix

Use these operational commands into your Claude workspace or Gemini session to pilot the foundry.

### 1. Cold Start & Ingestion

> Ingest all new files in the `00-raw-inputs/` directory. Execute the Node 0 Technical Pre-Flight specification. Validate all NFRs for numeric SLAs and output the Node 0 State Digest to `01-node0-preflight/node0-digest.md`. Do not proceed to Node 1 until authorized.

### 2. Sequential Execution Commands

* **Execute Node 1:**
> Node 0 circuits are cleared. Execute the Node 1 Scope Synthesis specification. Apply the Boundary Assumption protocol to any non-blocking scope gaps. Output the Node 1 State Digest to `02-node1-scope/node1-scope-digest.md`.


* **Execute Node 2:**
> Node 1 scope is locked. Execute the Node 2 UI Architecture specification. Generate the Mermaid.js behavioral flows and text wireframes strictly bound to the approved MVP scope in `03-node2-ui/node2-ui-architecture.md`.


* **Execute Node 3:**
> Execute the Node 3 Backlog Slicing specification. Enforce strict INVEST criteria. Select and isolate exactly one high-risk story for downstream elaboration in `04-node3-backlog/node3-backlog-digest.md`.


* **Execute Node 4:**
> Execute the Node 4 QA Engine specification on the isolated story. Generate comprehensive Gherkin BDD scenarios covering Happy, Negative, and Edge paths in `05-node4-qa/node4-qa-gherkin.md`.

  *Override — QA a different story:* Node 4's isolation protocol just means "exactly one story per run," not "only the story Node 3 designated." You can direct it at any single backlog story:
  > Execute Node 4 for Story [ID]: [Title]. Save the Gherkin output to its own file (e.g., `05-node4-qa/node4-qa-gherkin-[story-id].md`) so it doesn't overwrite the originally-designated story's QA output.


* **Execute Node 5:**
> Execute the Node 5 Dev Handover specification. Synthesize all upstream state digests into the final Jira ticket payload in `06-node5-jira/ticket-payload.md`. Enforce Definition of Ready (DoR) gates.

  *Note — multiple stories QA'd:* If more than one story has been through Node 4, Node 5 should synthesize one Jira ticket payload per QA'd story in the same output file (or ask it to), not just the first one. It should also state plainly which backlog stories are *not yet* represented, so the gap is visible at handoff.



### 3. Overrides & Quarantine Management

* **Clear NFR Quarantine (Node 0):**
> Resolving Node 0 Quarantine: The numeric SLA for the qualitative statement "[Insert Quote]" is [Insert Metric, e.g., <= 200 ms]. Apply this parameter, reduce quarantine flags to 0, and output a cleared state digest.


* **Confirm or Override a Tiered NFR (Node 0):**
  L2 (industry standard) and L3 (inferred) NFRs don't halt the pipeline, but they still carry a `BA TO CONFIRM` tag until a human resolves them. Resolve one of two ways:
> Confirming Node 0 Tier [L2/L3] NFR: the [Industry Standard / Inferred] value for "[Insert NFR]" is correct as tagged. Clear the confirmation flag and mark it CONFIRMED in the digest.

  Or, to override it with a different real value:
> Overriding Node 0 Tier [L2/L3] NFR: "[Insert NFR]" should instead be [Insert correct metric]. Replace the tagged value, mark it CONFIRMED, and note the override reason in the digest.


* **Inject Missing RACI Owner (Node 1):**
> Update for Node 1: The Accountable stakeholder is [Name/Title]. Re-run Node 1, clear the missing RACI circuit breaker, and overwrite the digest.


* **Force Full Downstream Resynchronization:**
> The scope digest in `02-node1-scope/node1-scope-digest.md` has been updated. Re-verify Nodes 2 through 5 sequentially against this updated file and regenerate the final Jira payload.


* **Back-Propagate a Scope Change After Downstream Nodes Have Already Run:**
  It's normal for a stakeholder to change their mind on scope *after* UI flows or backlog have already been built (e.g., "actually, descope that feature to Phase 2"). Don't just note it going forward — walk it backward through every node already run:
> Scope change: [feature] is now [descoped to Phase 2 / newly in-scope / changed to X]. Update Node 1's In-Scope/Deferred lists and Boundary Assumptions Registry, then update every downstream node already run (Node 2 flows/wireframes, Node 3 backlog, Node 4 Gherkin, Node 5 Jira payload) to remove or add the affected elements. Confirm each file was actually edited, not just the most recent one.


---

## Running Multiple Projects Through One Repo

This pipeline is designed to be reusable across many engagements, but the node specs (`prompts/node-*.md`) write to **fixed filenames** (`node1-scope-digest.md`, `ticket-payload.md`, etc.) with no project identifier baked in. If you run a second project through the same repo without changing anything, its outputs will silently overwrite the first project's deliverables in `01-node0-preflight/` through `06-node5-jira/`.

Two ways to avoid this — pick one per repo, don't mix:

1. **Suffix every output filename with a project tag**, e.g. `node1-scope-digest-APAC.md`, `ticket-payload-APAC.md`. Cheapest option; works well when a handful of projects share the same repo. State the tag explicitly in your first command of each session ("save all outputs for this run with a `-<ProjectTag>` suffix").
2. **Give each project its own numbered-folder set** (`00-raw-inputs-APAC/`, `01-node0-preflight-APAC/`, ...) if projects are large enough to warrant full separation.

Either way, before ingesting a new raw input file, check whether the target output folder already has content from a different project — if so, name accordingly rather than overwriting.

---

## Versioning, Renaming, and Manually Editing Digest Files

### Referencing a renamed or versioned file

None of the node specs, and none of the example commands above, contain any "find the newest file" or "detect a renamed version" logic. Every example command assumes the canonical default filename set at Cold Start. If you rename a digest — e.g., `node0-digest-preclient-review.md` — the pipeline has no way to know that's the file you mean unless you say so explicitly:

> Execute Node 1, reading the Node 0 digest from `01-node0-preflight/node0-digest-preclient-review.md`.

Always state the exact path in the command itself. A rename alone does nothing.

### Prefer git history over manual renaming for tracing what happened

Since this repo is git-tracked, commit history already gives you a full trace of how each digest evolved — who changed what, and when — without the ambiguity risk of multiple similarly-named files sitting in one folder (see "Running Multiple Projects Through One Repo" above for why that risk is worth avoiding). Editing a digest in place and committing it is generally cleaner than keeping numbered copies. Use named checkpoints only when you deliberately want a permanent snapshot at a specific milestone (e.g., `node0-digest-post-client-signoff.md`), and always reference them by explicit path per above.

### Manually editing a digest's content — source fields vs. computed fields

Every digest contains two kinds of fields:
- **Source fields** — actual facts: an NFR value, a persona name, a technical dependency, a RACI entry. Safe to hand-edit directly.
- **Computed fields** — `node_X_status`, `ticket_status`, `ready_for_tech_elaboration`, `blocking_items`, `unresolved_tokens`, and similar. These are *derived* from the source fields by that node's own mechanical logic (see the DoR Computation and Readiness Computation rules in Nodes 4 and 5). **Never hand-edit these directly.** Manually flipping `BLOCKED` to `CLEAR` without the underlying source fields actually changing produces a document that looks resolved but isn't — and nothing downstream is guaranteed to catch that.

The safe pattern: edit the source field, then explicitly tell whichever node you invoke next to **recompute status from the source fields rather than trusting any status field already present in the file**. This forces the mechanical logic to re-run fresh against the real data.

For most real updates — a newly confirmed SLA, a resolved persona, a name for a missing Accountable owner — the safer and simpler path is feeding the new fact back into the conversation with the node it actually originated from, and letting that node regenerate a complete, internally consistent digest (see "Back-Propagate a Scope Change" above). This guarantees source and computed fields move together, which hand-editing does not.

### An honest limitation, not a solved problem

Zero-Inference protects against the *AI* inventing a value. It cannot detect a *human* typing a fabricated value directly into a digest file outside the conversation — a properly-earned "200ms" and a hand-typed fake "200ms" are textually identical to the next node. This is a trust boundary around whoever edits the file, not something further prompt design can close. One real, existing safeguard worth knowing: Node 5's Definition of Ready computation always re-derives its status from raw field content and literal token counts, never from a trusted inbound status flag — so even a hand-edited upstream digest still gets caught at the final gate if a real gap remains.

---

## Multi-Machine Synchronization Protocol

To sync work between multiple machines (e.g., Windows and Mac) using GitHub Desktop:

```text
BEFORE YOU START WORK:
1. Open GitHub Desktop.
2. Click "Fetch origin" / "Pull" to pull the latest AI state digests.

AFTER GENERATING NEW OUTPUTS:
1. Open GitHub Desktop.
2. Enter a commit summary (e.g., "Cleared Node 1 Scope Digest").
3. Click "Commit to main" -> Click "Push origin".

```

---

## Quality & Governance Standards

* **Prompt Structure Standard:** Every prompt file in `prompts/` opens with a `Persona:` and `Objective:` declaration, then proceeds through numbered `STEP` sections (including the DSM Continuous Compliance Gate, Header Verification, and node-specific execution logic), and closes with `OPERATIONAL RULES`. All nodes conclude with an `OUTPUT EXECUTION DIRECTIVE (TOKEN DISCIPLINE)` instructing the model to suppress conversational filler and begin output immediately.
* **Zero-Inference Fallback Tokens:**
  - `[BA TO CONFIRM]` — business rules, personas, or values with no source in the intake.
  - `[ARCHITECT TO SUPPLY]` / `[TBD - ARCHITECT TO SUPPLY]` — technical schemas, API endpoints, or data models.
  - `[INVALID NFR FORMAT - BA MUST DEFINE NUMERIC SLA]` — an NFR with no numeric basis at any tier (Node 0).
  - `[INDUSTRY STANDARD — BA TO CONFIRM APPLICABILITY]` — an NFR defaulted to a recognized standard, pending confirmation it actually applies (Node 0, Tier L2).
  - `[INFERRED FROM CONTEXT — BA TO CONFIRM]` — an NFR logically implied by another stated fact, pending confirmation (Node 0, Tier L3).
  - `[PERFORMANCE ASSERTION BLOCKED - ...]` — a Gherkin assertion that would otherwise require a numeric bound Node 0 never resolved (Node 4).
  - `[ACCEPTED RISK — DSM:HIGH, NO SLA DEFINED, PROCEEDING ON HUMAN AUTHORIZATION]` — an NFR that triggered the DSM-Tier Escalation Rule, where a human explicitly chose to proceed without a value rather than supply one (Node 0).
  - `[PROJECT STANDARD]` / `[GLOBAL DOMAIN: <name>]` / `[GLOBAL DEFAULT]` — the source tag on every NFR category, showing whether it came from a per-engagement override, `global-standards.md`'s domain-specific matrix, or the built-in fallback (Node 0).
  - `[PROJECT DEFAULT — CONFIRM APPLIES TO THIS PROJECT]` / `[GLOBAL ROLE-TYPE: <description>]` — an unconfirmed Accountable owner suggestion, either a per-engagement standing default or a role-type hint from `global-standards.md`'s RACI baseline. Neither counts as confirmed (Node 1).
  - `[PROJECT DoR CRITERION]` / `[GLOBAL DoR CRITERION]` — an additional Definition of Ready check sourced from a reference file, always additive, never a relaxation of the built-in checks (Node 5).
* **Reference Precedence:** Two tiers of reference data exist, in priority order — a per-engagement override file (`nfr-standards.md`, `raci-matrix.md`, `dor-checklist.md`, empty until a specific project needs one) above `global-standards.md` (the populated core knowledge vault). Neither tier controls the pipeline's own enforcement: they supply which standard applies, which role type is expected, or which additional criteria must pass — never whether Zero-Inference, tiering, the DSM-Tier Escalation Rule, or a human sign-off can be bypassed. A missing or incomplete reference file at any tier simply falls through to the next; it never halts a node. Note that `global-standards.md`'s RACI baseline gives role *types* ("Product Sponsor / Business Owner"), not names — it can only help a human find the right person faster, never confirm one on its own.
* **Pipeline Status Enforcement:** Output tickets remain locked in `BLOCKED` status within the Definition of Ready until all architectural schema tokens are supplied by engineering.