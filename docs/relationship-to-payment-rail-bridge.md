# Relationship to Payment Rail Bridge

Royalty Event Layer v0.1 sits upstream of Payment Rail Bridge.

Royalty Event Layer does not connect directly to external payment rails.

It prepares structured event context that may later support Allocation Intent,
Royalty OS allocation logic, and eventually Payment Rail Bridge translation.

This document explains how Royalty Event Layer relates to Royalty OS Payment
Rail Bridge.

---

## 1. Core Relationship

The basic relationship is:

```text
Royalty Event Layer
        ↓
Allocation Intent
        ↓
Royalty OS
        ↓
Payment Rail Bridge
        ↓
External Payment Rail
```

Royalty Event Layer classifies value-relevant events.

Payment Rail Bridge translates allocation intent into payment-rail-compatible
instructions.

They are connected, but they must remain separate.

---

## 2. Different Responsibilities

Royalty Event Layer answers:

```text
What value-relevant event happened?
```

Payment Rail Bridge answers:

```text
How can approved allocation intent be translated toward external circulation?
```

These are different questions.

A Royalty Event is not a payment instruction.

A Payment Rail Bridge record should not be created directly from a raw event
without allocation intent and review-aware processing.

---

## 3. Why the Separation Matters

If Royalty Events directly triggered Payment Rail Bridge flows, the system would
be too aggressive.

Unsafe path:

```text
access_event
        ↓
payment rail instruction
```

or:

```text
influence_event
        ↓
external settlement
```

These flows are too strong.

The safer path is:

```text
Royalty Event
        ↓
Event Bundle
        ↓
Allocation Candidate
        ↓
Allocation Intent
        ↓
Allocation Readiness
        ↓
Royalty OS
        ↓
Payment Rail Bridge
```

Each layer adds review, context, dispute awareness, and safety.

---

## 4. Royalty Event Layer Responsibilities

Royalty Event Layer is responsible for:

- classifying raw signals
- preserving trace references
- defining event types
- recording event confidence
- preserving review status
- preserving dispute status
- identifying allocation relevance
- preparing event bundles or trigger candidates

Royalty Event Layer does not:

- execute payment
- generate external settlement instructions
- define legal entitlement
- determine final allocation shares
- bypass Allocation Readiness
- connect directly to payment providers

---

## 5. Payment Rail Bridge Responsibilities

Payment Rail Bridge is responsible for:

- receiving allocation intent
- translating allocation intent into payment-compatible instructions
- preserving allocation references
- preserving trace references
- preserving review and dispute status
- mapping recipients to payment-rail-compatible identities
- preparing settlement context
- receiving settlement status from external rails
- maintaining payment rail neutrality

Payment Rail Bridge should not:

- receive raw unreviewed events as payment instructions
- treat access events as automatic payments
- treat influence events as final allocation
- erase upstream dispute context
- claim official integration with any payment rail unless explicitly supported

---

## 6. Interface Boundary

The boundary between the two repositories is Allocation Intent.

```text
Royalty Event Layer
        ↓
Allocation Intent
        ↓
Payment Rail Bridge
```

Royalty Event Layer may produce or support Allocation Intent.

Payment Rail Bridge should consume Allocation Intent.

This boundary prevents events from becoming direct financial actions.

---

## 7. Data Flow

A safe data flow may look like this:

```text
trace_record
        ↓
royalty_event
        ↓
event_bundle
        ↓
allocation_candidate
        ↓
allocation_intent
        ↓
payment_rail_bridge_record
        ↓
payment_rail_candidate_flow
```

At each step, context should be preserved.

---

## 8. Example Flow

```yaml
royalty_event:
  event_id: evt_reuse_001
  event_type: reuse
  source_reference: source_framework_001
  trace_reference: trace_reuse_001
  confidence: 0.76
  review_status: approved
  dispute_status: none
  allocation_relevance: high

event_bundle:
  bundle_id: bundle_royalty_001
  events:
    - evt_reuse_001
    - evt_citation_001
    - evt_influence_001
  aggregate_confidence: 0.78
  review_status: approved
  dispute_status: none
  allocation_relevance: high

allocation_intent:
  allocation_id: alloc_001
  event_references:
    - evt_reuse_001
    - evt_citation_001
    - evt_influence_001
  trace_references:
    - trace_reuse_001
    - trace_citation_001
    - trace_influence_001
  recipient_reference: contributor_001
  allocation_value:
    type: share
    value: 0.15
    unit: ratio
  review_status: pending
  dispute_status: none
  payment_eligibility: pending_review
```

Only after this stage should Payment Rail Bridge become relevant.

---

## 9. Relationship to XMoney Candidate Flow

In the Payment Rail Bridge repository, XMoney may be treated as one possible
payment-rail candidate.

Royalty Event Layer does not depend on XMoney.

Royalty Event Layer does not prepare XMoney instructions.

It only prepares upstream event context that may eventually become allocation
intent.

The correct chain is:

```text
Royalty Event
        ↓
Allocation Intent
        ↓
Payment Rail Bridge
        ↓
XMoney Candidate Flow
```

The incorrect chain is:

```text
Royalty Event
        ↓
XMoney Payment
```

The incorrect chain skips allocation, review, and bridge context.

---

## 10. Context Preservation

Payment Rail Bridge should preserve references back to Royalty Events where
appropriate.

Recommended references may include:

```yaml
allocation_intent:
  event_references:
    - evt_access_001
    - evt_citation_001
    - evt_reuse_001
  trace_references:
    - trace_access_001
    - trace_citation_001
    - trace_reuse_001
```

This allows settlement flows to remain connected to upstream event context.

---

## 11. Review and Dispute Propagation

Review and dispute status should propagate downstream.

If an event is disputed, the Allocation Intent should preserve that status.

If Allocation Intent is disputed, Payment Rail Bridge should preserve that status.

Example:

```text
disputed_event
        ↓
disputed_allocation_intent
        ↓
blocked_or_pending_bridge_flow
```

Payment Rail Bridge should not erase dispute state.

---

## 12. Payment Eligibility

Payment eligibility should not be determined by Royalty Event Layer alone.

A Royalty Event may have allocation relevance.

But payment eligibility should be determined downstream through:

- event review
- event aggregation
- allocation candidate formation
- allocation intent
- allocation readiness
- Royalty OS allocation logic
- Payment Rail Bridge safety checks

This prevents raw events from triggering settlement too early.

---

## 13. Relationship to Payment Rail Bridge Examples

The Payment Rail Bridge repository includes examples such as:

```text
examples/allocation-intent.sample.yaml
examples/xmoney-candidate-flow.sample.yaml
```

Royalty Event Layer may provide upstream context for these examples.

A future version may add a cross-repository example:

```text
Royalty Event Layer event bundle
        ↓
Allocation Intent sample
        ↓
Payment Rail Bridge candidate flow
```

This would demonstrate the full path from trace to circulation.

---

## 14. Anti-Direct-Payment Rule

The core rule is:

```text
Royalty Events must not directly trigger payment rails.
```

The proper rule is:

```text
Royalty Events may support Allocation Intent.
Allocation Intent may later be translated by Payment Rail Bridge.
```

This keeps the system review-aware, dispute-aware, and payment-rail-neutral.

---

## 15. Non-Goals

This relationship does not imply that Royalty Event Layer:

- connects directly to XMoney
- connects directly to any payment rail
- executes settlement
- creates payment obligations by itself
- bypasses Allocation Intent
- bypasses Allocation Readiness
- bypasses Royalty OS
- determines final allocation shares
- removes dispute context

The Royalty Event Layer is upstream context, not downstream settlement.

---

## 16. Summary

Royalty Event Layer and Payment Rail Bridge are complementary but separate.

Royalty Event Layer classifies value-relevant events.

Allocation Intent prepares allocation context.

Payment Rail Bridge translates approved allocation intent toward external
payment circulation.

```text
Event Layer = what happened in a value-relevant way
Allocation Intent = what may be considered for allocation
Payment Rail Bridge = how allocation may later circulate
```

The bridge begins only after event context has passed through allocation logic.

This separation is the safety structure of Royalty OS.
