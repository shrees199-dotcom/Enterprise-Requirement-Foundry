================================================================================
ENTERPRISE REQUIREMENT FOUNDRY: MASTER INTAKE PAYLOAD
PROJECT CODE: AEGIS-OMNI (VERSION 3.0-PROD)
================================================================================

1. EXECUTIVE SUMMARY & STRATEGIC INTENT
Project Aegis-Omni is a next-generation autonomous regulatory compliance and financial crime detection mesh. The system ingests global SWIFT payment streams, customer PII dossiers, and real-time transaction telemetry to execute automated anti-money laundering (AML) screening, sanctions list matching, and suspicious activity reporting (SAR) generation.

2. REGULATORY & DATA SENSITIVITY CLASSIFICATION (DSM & HARM)
* Data Sensitivity (DSM_Tier): High. Involves global banking customer PII, unmasked financial account balances, national identification numbers, and cross-border transaction ledgers subject to GDPR, CCPA, and RBI data localization norms.
* Automated Decision Impact (Harm_Risk_Tier): High. Autonomous non-human agents (NHIs) are empowered to execute real-time transaction holds, high-risk flag escalations, and automated account freezes without pre-approval from human operators under specific emergency conditions.

3. ARCHITECTURAL & TECHNICAL DEPENDENCIES
* Core Systems: Enterprise AI Gateway, Neo4j Enterprise (Graph Knowledge Base), Milvus Vector Store (Semantic Embeddings), Apache Kafka (Streaming Ingest), and Core Banking API Gateway (Temenos/Finacle).
* Grounding Layer: Must implement Hybrid GraphRAG combining graph-based Cypher traversal with dense vector retrieval.
* Model Routing: Dynamic routing between fine-tuned distilled models (e.g., Llama-3-70B-Instruct) for high-volume baseline filtering and frontier reasoning models (e.g., Claude 3.5 Sonnet / GPT-4o) for high-complexity SAR legal argument synthesis.
* Non-Human Identity (NHI) Management: Autonomous compliance agents require Just-In-Time (JIT), least-privilege tool access to core banking systems and regulatory databases.

4. NON-FUNCTIONAL REQUIREMENTS & NFR BASELINE
* Context Budgeting: Must enforce strict input/output token caps and a 24-hour semantic cache TTL. (Explicitly unstated: exact maximum token threshold per tenant rate limit).
* Security & Privacy: Automatic PII masking and Data Loss Prevention (DLP) filters must be active on all prompts prior to external transmission. Encryption required in transit (TLS 1.3) and at rest (AES-256).
* Performance & Latency: The compliance triage pipeline must operate with lightning-fast execution speed, seamlessly scaling to handle massive transaction volumes while remaining ultra-secure and user-friendly for compliance officers. [Note: Intentaneous inclusion of smuggling adjectives for anti-smuggling protocol test].
* Auditability & Telemetry: Tamper-proof audit logs retaining all submitted prompts, retrieved contextual chunks, and model decisions must satisfy SOC 2 Type II and ISO 27001 standards. Cost-per-outcome telemetry must be tracked via the Enterprise AI Gateway.

5. OPERATIONAL BOUNDARIES & KNOWN AMBIGUITIES
* Scope Boundaries: In-scope capabilities include Automated PII Prompt Filtering (DLP), Hybrid GraphRAG Retrieval, Independent Validator Loops, and the HITL Review Console. Deferred scope includes predictive fraud forecasting models (Phase 2).
* Explicit Human Owner: Chief Risk Officer (Aparna Nair).
* Competing Reference Workflow Supplied for Node 2: Reference legacy Visio workflow file "Legacy-AML-Pipeline-v2.vsdx" supplied separately by the user to test Node 2 Workflow Reconciliation (Divergence Report).