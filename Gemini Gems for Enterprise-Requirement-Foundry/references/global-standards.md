# GLOBAL ENTERPRISE STANDARDS & BASELINES
**System Role:** Core Knowledge Vault for the Foundry Engine.
**Execution Logic:** If project-specific metrics are missing in Node 0 or Node 1, the engine will suggest the parameters mapped in this file based on the declared project domain. The human operator retains final override authority.

## 1. UNIVERSAL DEFINITION OF READY (DoR)
*Applies to all Epics/Stories regardless of domain.*
- **Scope Isolation:** Sliced strictly to INVEST criteria (Independent, Negotiable, Valuable, Estimable, Small, Testable).
- **Dependency Map:** All upstream API, database, and third-party vendor dependencies are confirmed and unblocked.
- **Acceptance Criteria:** 100% of functional requirements are mapped to measurable Gherkin (BDD) scenarios.
- **NFR Attachment:** Domain-specific SLAs (Latency, Security, Resilience) are explicitly tied to the Jira ticket.
- **Sign-off:** The designated Accountable (A) owner has approved the bounded scope.

## 2. UNIVERSAL RACI BASELINE
*Default assignment matrix unless overridden by stakeholder availability.*
- **Accountable (A):** Product Sponsor / Business Owner (Must have budget/cutover authority).
- **Responsible (R):** Tech Lead / Principal Engineer (Executes the technical build).
- **Consulted (C):** Lead Business Analyst / Domain SMEs / Security Architect (Provides requirements, mapping, and compliance).
- **Informed (I):** Internal Support / Operations / Sales (Downstream consumers of the release).

## 3. DOMAIN-SPECIFIC NFR MATRIX
*Default Service Level Agreements and Compliance frameworks based on industry sector.*

| Domain | Performance (Latency) | Throughput / Scalability | Resilience (RTO/RPO) | Security & Compliance |
| :--- | :--- | :--- | :--- | :--- |
| **Aviation / Aerospace** | < 50ms (Mission Critical) | 1,000 TPS per node | 99.9999% (RTO < 10s, RPO = 0) | DO-178C, AES-256, Zero-Trust |
| **Banking / Finance** | < 100ms (Core Tx) | 5,000 TPS (Standard) | 99.999% (RTO < 1m, RPO = 0) | PCI-DSS, SOC 2 Type II, ISO 27001 |
| **E-Commerce / Retail** | < 2s (UI Load), < 200ms (API) | 100,000 TPS (Peak/Holiday) | 99.99% (RTO < 5m, RPO < 1m) | PCI-DSS Level 1, GDPR/CCPA |
| **Energy / Utility** | < 500ms (IoT Telemetry) | 10,000 TPS (Event Stream) | 99.99% (RTO < 15m, RPO < 5m) | NERC CIP, Edge/Offline Capability |
| **FMCG / Supply Chain** | < 500ms (Inventory Sync) | 2,000 TPS (Batch/Stream) | 99.9% (RTO < 1h, RPO < 15m) | ISO 28000, RBAC, TLS 1.3 |
| **Government / Public Sector** | < 1s (Portal Load) | 1,000 TPS | 99.9% (RTO < 4h, RPO < 1h) | FedRAMP High, FIPS 140-2, WCAG 2.1 AA |
| **Healthcare / Pharma** | < 500ms (EHR Sync) | 1,000 TPS | 99.99% (RTO < 5m, RPO = 0) | HIPAA, HITRUST, 7-Year Audit Logging |
| **Public Domain / Civic Tech**| < 2s (High concurrent read) | 10,000 TPS (Read Heavy) | 99.0% (RTO < 24h, RPO < 4h) | WCAG 2.1 AAA, GDPR, Open Data Stds |

## 4. DATA SENSITIVITY MATRIX (DSM)
*Use this framework to classify the risk profile before applying Domain-Specific NFRs. Classification is based on the highest triggered threshold.*

| Sensitivity Level | Financial Impact Unit | Regulatory/Compliance Unit | Human/Stakeholder Unit | Example Architecture |
| :--- | :--- | :--- | :--- | :--- |
| **HIGH (Tier 1)** | > $1M revenue loss/day OR catastrophic SLA penalty. | Triggers statutory breach (PCI-DSS, HIPAA, GDPR). Jail time or loss of operating license. | PII/PHI of > 10,000 users exposed. Risk to life, safety, or absolute brand destruction. | Core banking ledger, healthcare EHR, active flight telemetry. |
| **MEDIUM (Tier 2)** | $10k - $1M revenue loss/day. Recoverable SLA penalty. | Non-statutory compliance breach (SOC 2). Contractual vendor penalties. | Internal corporate IP exposed. < 10,000 users affected. Temporary brand embarrassment. | B2B CRM, internal financial reporting, supply chain logistics. |
| **LOW (Tier 3)** | < $10k revenue loss/day. No financial SLA impact. | Zero regulatory impact. | Zero PII. Zero customer impact. Completely public or anonymized data. | Public marketing portal, internal cafeteria app, open-data civic API. |

