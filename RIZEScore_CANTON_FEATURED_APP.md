# Canton Featured App – 00XX

> This document is a **descriptive record** for a Canton Featured App.
> It is **non-governance**, **non-normative**, and does not define or modify any
> Canton Improvement Proposal (CIP).
>
> This document is intended to support interpretability during normal operation
> and during anomalous activity periods.

---

## 1. App identity

- **App name:**
- **Organization / legal entity:**
- **Website:**
- **Public repository (if any):**
- **Primary contact:**
- **Security / technical contact (optional):**
- **Application-controlled PartyId(s):**
  - <PartyId or namespace>
  - <PartyId or namespace>

(These are the PartyIds operated by the application that may anchor
activity marker–relevant ledger state transitions.)

---

## 2. App summary

Provide a concise, factual description of what the application does.

- 2–5 sentences
- No marketing language
- No forward-looking statements

---

## 3. Role of Canton Network

Describe why and how the application uses Canton Network.

Examples:
- settlement or coordination layer
- issuance or registry infrastructure
- privacy-preserving workflows
- protocol or infrastructure signaling

---

## 4. Operational usage

Describe the application’s current operational usage of Canton Network.

- **Canton network environment(s):** (e.g. DevNet, TestNet, MainNet)
- **Application operational status:** (e.g. development, pilot, limited production, production)
- **Primary workflows on Canton:**  
  - bullet list of concrete workflows

---

## 5. Featured App Activity Markers (CIP-0047)

This section declares the **Featured App Activity Markers** emitted by the application,
as defined in **CIP-0047** and applicable amendments.

The information below is **declarative** and is provided to improve transparency,
interpretability, and governance oversight of application activity on Canton Network.

This document does **not** define, enforce, or modify activity marker mechanics.

---

### 5.1 Ledger anchoring (descriptive)

All declared activity markers correspond to **finalized state transitions**
recorded on Canton Network.

Activity markers are not emitted solely:

- in response to user interface actions,
- in response to API calls alone,
- prior to ledger finality,
- for speculative, reversible, or corrective actions.

The ledger is the sole source of truth for activity marker eligibility. 
Declared activity markers are anchored to finalized ledger state transitions involving one or more application-controlled PartyIds.

---

### 5.2 Declared activity markers

For each activity marker, provide the corresponding metadata fields defined in
CIP-0047 and applicable amendments.

Only activity markers intended to be public should be listed.

#### Marker format

```
activityCategory: <Enum>
activityDescription: <Text>
estimatedNotionalRange: <Enum | None>
assetClass: <Enum | None>
userCountIndicator: <Enum>
Notes: <Optional context>
```

---

### Illustrative examples (non-normative)

#### Example A — Single-user DvP settlement

```
activityCategory: DvPSettlement
activityDescription: Single-user initiated delivery-versus-payment settlement
estimatedNotionalRange: $100k–$1M
assetClass: Security
userCountIndicator: SingleUser
Notes: Represents one end user intentionally initiating a settlement.
```

---

#### Example B — Batch settlement across multiple users

```
activityCategory: DvPSettlement
activityDescription: Batch settlement of matched trades across multiple users
estimatedNotionalRange: >= $10M
assetClass: Security
userCountIndicator: MultipleUsersDistinctParties
Notes: One marker represents aggregated activity across many users.
```

---

#### Example C — Infrastructure / validator activity (no asset)

```
activityCategory: InfrastructureHealth
activityDescription: Validator liveness or protocol health signal
estimatedNotionalRange: None
assetClass: None
userCountIndicator: ValidatorOperator
Notes: Protocol-level activity; no asset movement involved.
```

---

#### Example D — Wallet-mediated wrapped asset activity

```
activityCategory: AssetRepresentation
activityDescription: Wallet-mediated wrapping, unwrapping, or movement of a represented asset
estimatedNotionalRange: Variable
assetClass: DigitalAsset
userCountIndicator: MultipleUsersPotentiallySharedWallet
Notes: Represents ledger-finalized activity initiated by wallet infrastructure.
May occur at high frequency due to user behavior or automated wallet logic.
```

> The volume, aggregation, or absence of activity markers does not imply per-user
> rewards, per-transaction granularity, or economic value outside the CIP-0047
> governance framework.

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

Describe, at a high level, how the application determines **when** and **how many**
activity markers are emitted, with reference to finalized ledger activity.

This description should clarify, where applicable:

- whether markers scale with economic value, transaction count, or completed workflows,
- whether markers are emitted per ledger event or per aggregated batch of ledger events,
- whether any minimums, maximums, or rate limits apply.

This section is descriptive only and does not define governance or tokenomics policy. 
This description is intended to provide context for interpreting observed marker volumes and patterns.

---

## 7. Dependencies and integrations

List dependencies and integrations relevant to understanding how the application
interacts with Canton Network and how activity may be generated or correlated.

This may include, where applicable:

- validators or infrastructure providers involved in operating the application,
- other Canton applications or shared on-ledger components,
- wallet infrastructure PartyIDs or custody systems interacting with Canton Network,
- external systems that initiate, aggregate, or automate ledger activity.

This section is descriptive and high-level; detailed architecture or security-
sensitive information is not required.

---

## 8. Security and abuse-mitigation (descriptive)

Provide a high-level, factual description of controls relevant to preventing
automated or synthetic activity.

Examples:
- economic friction (fees, limits)
- access gating or identity controls
- rate limiting or monitoring
- post-hoc review processes

(No implementation details required.)

---

## 9. Changelog

- YYYY-MM-DD — Initial version
- YYYY-MM-DD — Update summary

Material changes to activity marker behavior (e.g. introduction of new
marker categories, changes to aggregation logic, or changes in emission
patterns) are expected to be reflected in this document promptly, in
order to preserve interpretability of observed activity.