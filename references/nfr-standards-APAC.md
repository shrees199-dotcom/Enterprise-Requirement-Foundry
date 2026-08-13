# NFR & Architecture Standards — APAC BSS Modernization (Project Strangler Fig)

**Status:** Active baseline — re-confirmed 2026-07-28 (post clean-slate restart)
**Confirmed by:** Jaba Ghosh, directly in-session, 2026-07-28
**Applies to:** `00-raw-inputs/APAC DUMP.txt` intake and all downstream pipeline nodes for the APAC BSS Modernization project (this restarted cycle)

## Origin

The raw intake (executive kickoff transcript + EA email + PMO RACI draft) states these requirements only in qualitative terms ("blazingly fast," "highly secure," "zero downtime," loyalty tiers "not mapped out yet"). Per Node 0's zero-inference rule, none of these were invented by the pipeline. Following the 2026-07-28 clean-slate restart (see `01-node0-preflight/node0-digest.md`), the user re-supplied this same 12-parameter set directly in-session, which is treated as a fresh, explicit confirmation for this new cycle — not an automatic carry-over from the prior (superseded) run.

## Standing Parameter Set (12 of 12 Node 0 flags resolved)

| # | Domain | Standard |
|---|---|---|
| 1 | Payment Vendor & API | Stripe API v3 (`/v1/charges`) |
| 2 | Payload Schema | Standard Stripe Charge Object (`amount`, `currency`, `source`) |
| 3 | Oracle DB Protocol | Apache Kafka event streaming for real-time legacy sync |
| 4 | Target Datastore | Amazon Aurora PostgreSQL |
| 5 | Loyalty Tiers | Prepaid accounts older than 5 years get a flat 10% discount on rating calls |
| 6 | Performance SLA | p99 API latency ≤ 200ms |
| 7 | Throughput SLA | Peak capacity 5,000 TPS |
| 8 | Security SLA | TLS 1.3 in-transit, AES-256 at-rest |
| 9 | Compliance | PCI-DSS Level 1 |
| 10 | Cutover SLA | RTO ≤ 5 min, RPO = 0, via blue-green deployment |
| 11 | Accessibility | WCAG 2.1 AA for internal portals |
| 12 | UX Metric | Max 3 clicks to process a customer refund in the support portal |

*Note on item 5: this restart re-confirms the flat 10%/5yr loyalty rule as an active Node 0 baseline item. The prior cycle's later decision to descope loyalty to Phase 2 was a Node 1/2 scope call, not a Node 0 NFR fact — per the clean-slate restart, that scope decision does not carry forward automatically. Whether loyalty is in-scope for Phase 1 MVP will be (re)decided at Node 1.*

## Not Yet Re-Confirmed This Cycle

The prior (superseded) run had also resolved 6 additional items during Node 1/Node 2 — MFA delivery (SMS OTP), session timeout (20 min), concurrent-session policy (single global session), refund reconciliation (original payment method), and refund retry window (7 days). None of these were included in this restart's re-confirmation and should be treated as open again; they'll naturally resurface as UX ambiguities if/when Node 2 runs, unless the user supplies them again sooner.

## Usage

- This 12-item set clears all 12 Node 0 quarantine flags for `APAC DUMP.txt` in this restarted cycle.
- Downstream nodes (Node 1 onward) should treat these as locked technical baselines, not open items.
- This document does not resolve RACI / Accountable-owner gaps or the ROI target — those remain unresolved from the restart and are separate governance/business concerns tracked in Node 1.
