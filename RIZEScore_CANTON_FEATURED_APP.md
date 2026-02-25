# RIZEScore Featured App

> This document is a **descriptive record** for the RIZEScore Featured App.
> This document is intended to support interpretability during normal operation
> and during anomalous activity periods.

---

## 1. App identity

- **App name:** RIZEScore
- **Organization / legal entity:** T-RIZE Group
- **Website:** [t-rize.io](https://www.t-rize.io/)
- **Public repository (if any):** [github.com/T-RIZE-Group/canton-featured-apps](https://github.com/T-RIZE-Group/canton-featured-apps)
- **Primary contact:** ceo@t-rize.io
- **Security / technical contact (optional):** cto@t-rize.io
- **Application-controlled PartyId(s):** 
  - TRIZEGroup-RIZEScore::12206ab3bf15b14410220357d6a6375eb1015f2e7fade1deb449463c2f2a25304889

(These are the PartyIds operated by the application that may anchor
activity marker–relevant ledger state transitions.)

---

## 2. App summary

RIZEScore is a Canton analytics and signaling application that converts publicly observable on-ledger activity into standardized, explainable indicators. It analyzes party interaction patterns (flows, counterparties, repetition, persistence) and publishes time-stamped Activity Marker signals when deterministic rule conditions are met. The result is a consistent on-ledger reference layer that supports interpretability and downstream monitoring integrations.

IMPORTANT: This App is transitioning away from on-ledger Activity Markers and instead integrates with external parties explorers to provide richer, feature-complete signals without relying on these small marker submissions. This integration exposes rich metadata (signal type, computed metrics, context) for more transparency and reach.
---

## 3. Role of Canton Network

RIZEScore uses Canton Network as:

- a source of publicly observable ledger state transitions,
- a finality layer for anchoring time-stamped signal publications,
- a coordination layer enabling transparent and auditable signaling.

This allows signals to be verifiably anchored to ledger finality, independently auditable, and consistently referenced by downstream tools (validators, explorers, monitoring systems) without relying on off-ledger logs or proprietary APIs.

---

## 4. Operational usage

Describe the application’s current operational usage of Canton Network.

- **Canton network environment(s):** MainNet
- **Application operational status:** Production
- **Primary workflows on Canton:**  
  - Ingest finalized on-ledger activity and compute Party ID indicators capturing flows, counterparties, repetition, and persistence.
  - Detect deviations via baseline-based rules and publish time-stamped Activity Markers from the application Party ID.
  - Surface signals in the UI and optionally deliver alerts and exports via APIs / email / webhook.
    
---

## 5. Featured App Activity Markers (CIP-0047)

This section declares the **Featured App Activity Markers** emitted by the application,
as defined in **CIP-0047** and applicable amendments.

The information below is **declarative** and is provided to improve transparency,
interpretability, and governance oversight of application activity on Canton Network.

This document does **not** define, enforce, or modify activity marker mechanics.

---

### 5.1 Ledger anchoring (descriptive)

RIZEScore anchors signals to ledger finality to make them independently verifiable and reusable across the ecosystem. Signals are computed from publicly observable, finalized activity aggregated by Party ID; when a rule triggers, RIZEScore publishes an Activity Marker via a transaction attributable to the application-controlled PartyId(s).

The ledger publication is the canonical reference for timing and existence of the signal. Any notifications or UI displays are derived views that reference the on-ledger marker.

---

### 5.2 Declared activity markers

RIZEScore emits diagnostic Activity Markers representing rule-triggered signal events derived from finalized on-ledger activity. These markers do not represent asset issuance, settlement, custody activity, or direct economic transfers initiated by the application.

Signal definitions (metrics, thresholds, severity bands, and interpretation criteria) are configuration-driven and may be co-defined with ecosystem participants through structured review processes. All configurations are deterministic and versioned; changes are reflected via policy_version to preserve interpretability over time.

#### Marker format

```
activityCategory: InfrastructureHealth
activityDescription: Diagnostic signal publication for a Party ID based on deterministic rule evaluation of finalized ledger activity
estimatedNotionalRange: None
assetClass: None
userCountIndicator: SingleUser
Notes: Represents a triggered integrity indicator for the referenced Party ID over a defined evaluation window (e.g., UTC day + rolling baseline). Configuration-driven and policy-versioned. Not a settlement, custody, or asset representation marker.
```

---

### 5.3 Non-emitting activities

As a general principle, Featured App Activity Markers are not emitted for
activity that does not represent an independent, finalized economic state
transition on the ledger.

The categories below illustrate common examples of such activity and are
provided for clarity only.

Illustrative examples include:

- onboarding or account setup
- configuration, reference data, or metadata updates
- retries, failures, or rollback-related actions
- cancellations, reversals, or voided workflows
- internal operational, administrative, or maintenance actions

This list is illustrative, descriptive, and explicitly non-exhaustive.

---

## 6. Marker emission policy (app-specific)

RIZEScore emits Activity Markers only to publish rule-triggered diagnostic signals anchored to finalized ledger activity. Markers are not emitted for activity that does not correspond to a finalized, signal-eligible ledger state transition or that does not change the evaluated signal outcome.

Illustrative examples include:

- UI interactions, dashboard views, searches, exports, or report generation
- API calls and off-ledger processing (ingestion, parsing, attribution, aggregation) when no signal is published
- rule evaluations that do not meet trigger thresholds or noise floors
- suppressed triggers due to rate limits or deduplication within the evaluation window
- policy configuration changes, simulations, backtests, or recalculations (unless a signal publication transaction is submitted)
- notification delivery (UI / email / webhook) and subscription management
- retries, failures, rollbacks, cancellations, reversals, or non-finalized activity

This list is illustrative, descriptive, and non-exhaustive.

---

## 7. Dependencies and integrations

RIZEScore operates as an analytics and signaling layer on Canton Network and depends on:

- Canton Scan APIs: Used to access finalized, publicly observable ledger activity for aggregation and rule evaluation.
- RIZEScore PartyId: Used to submit ledger transactions that publish Activity Markers.
- Validator observability (DAR): Validators can view and consume RIZEScore signals for the parties they host only if they run the relevant DAR and expose the corresponding events on their node.
- Off-ledger systems: RIZEScore UI, notifications (UI / email / webhook), and integration APIs that reference the on-ledger marker publication.

---

## 8. Security and abuse-mitigation (descriptive)

RIZEScore limits synthetic or automated signal amplification through:

- Deterministic, policy-versioned rules: Signals are emitted only when predefined conditions are met on finalized ledger data (policy_version).
- Noise floors + rolling baselines: Thresholds include minimum activity requirements and baseline comparisons to reduce low-volume or burst noise.
- Rate limits + deduplication: Per-party/per-signal caps ensure at most one emission per evaluation window (e.g., UTC day).
- Operational safeguards: Manual emergency stop for signal publication if needed.

---

## 9. Changelog

- 2026-01-28 — Initial version
- 2026-02-25  — Update summary
