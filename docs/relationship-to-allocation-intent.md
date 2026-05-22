# Relationship to Allocation Intent

Royalty Event Layer v0.1 sits upstream of Allocation Intent.

A Royalty Event does not automatically become Allocation Intent.

Allocation Intent is prepared only when one or more Royalty Events become
sufficiently reviewed, relevant, aggregated, and allocation-ready.

This document explains how Royalty Events may support Allocation Intent
without collapsing events directly into payment or ownership claims.

---

## 1. Core Relationship

The basic relationship is:

```text
Royalty Event
        ↓
Event Bundle
        ↓
Allocation Candidate
        ↓
Allocation Intent
        ↓
Royalty OS
        ↓
Payment Rail Bridge
```

Royalty Events classify value-relevant signals.

Allocation Intent prepares those signals for possible allocation logic.

Payment execution remains further downstream.

---

## 2. Royalty Event vs Allocation Intent

A Royalty Event answers:

```text
What kind of value-relevant event occurred?
```

Allocation Intent answers:

```text
Should this event or event bundle move toward allocation logic?
Who may be considered as a recipient?
What trace and review context supports the proposed allocation?
```

The two should remain separate.

---

## 3. Why Separation Matters

If every Royalty Event automatically became Allocation Intent, the system would
be too aggressive.

For example:

```text
access_event → allocation_intent
```

would be unsafe.

Likewise:

```text
influence_event → payment instruction
```

would be too strong.

The proper flow requires review and readiness.

```text
event
  ↓
review
  ↓
aggregation
  ↓
allocation candidate
  ↓
allocation intent
```

---

## 4. Royalty Event Responsibilities

Royalty Events are responsible for preserving structured event context.

They may include:

- event ID
- event type
- source reference
- trace reference
- actor type
- actor reference
- target reference
- weight
- confidence
- review status
- dispute status
- allocation relevance

Royalty Events do not:

- determine final allocation
- execute payment
- establish legal ownership
- create automatic entitlement
- bypass dispute handling

---

## 5. Allocation Intent Responsibilities

Allocation Intent is responsible for preparing a proposed allocation context.

It may include:

- allocation ID
- origin reference
- trace references
- event references
- recipient reference
- contribution description
- proposed allocation value
- allocation basis
- review status
- dispute status
- payment eligibility
- settlement constraints

Allocation Intent does not execute payment by itself.

It prepares downstream systems such as Royalty OS and Payment Rail Bridge.

---

## 6. Event-to-Intent Escalation

A Royalty Event may support Allocation Intent when it passes escalation criteria.

Possible escalation path:

```text
single event
        ↓
reviewed event
        ↓
event bundle
        ↓
allocation candidate
        ↓
allocation intent
```

Escalation may depend on:

- event type
- event weight
- confidence
- trace quality
- review status
- dispute status
- aggregation with other events
- allocation relevance
- allocation readiness rules

---

## 7. Event Bundles

A single event may be weak.

A bundle of events may become stronger.

Example:

```yaml
event_bundle:
  bundle_id: bundle_royalty_001
  source_reference: source_framework_001
  events:
    - evt_access_001
    - evt_citation_001
    - evt_reuse_001
    - evt_influence_001
  aggregate_confidence: 0.78
  aggregate_weight: 0.64
  allocation_relevance: high
  review_status: pending
  dispute_status: none
```

Event bundles may help prepare Allocation Intent.

However, even bundles should not bypass review.

---

## 8. Allocation Candidate

An Allocation Candidate is an intermediate state between Event Bundle
and Allocation Intent.

It means:

```text
The event evidence is relevant enough to be considered for allocation,
but allocation intent has not yet been finalized.
```

A candidate may include:

```yaml
allocation_candidate:
  candidate_id: candidate_001
  source_reference: source_framework_001
  event_bundle_reference: bundle_royalty_001
  proposed_recipient_reference: contributor_001
  allocation_relevance: high
  confidence: 0.78
  review_status: pending
  dispute_status: none
```

This object is not yet Allocation Intent.

It is a preparation stage.

---

## 9. Allocation Intent Example

An Allocation Intent may look like this:

```yaml
allocation_intent:
  allocation_id: alloc_001
  origin_reference: source_framework_001
  trace_references:
    - trace_access_001
    - trace_citation_001
    - trace_reuse_001
  event_references:
    - evt_access_001
    - evt_citation_001
    - evt_reuse_001
    - evt_influence_001
  recipient_reference: contributor_001
  contribution_description: >
    Conceptual structure contributed to downstream architecture and reuse.
  allocation_value:
    type: share
    value: 0.15
    unit: ratio
  allocation_basis:
    - reviewed_event_bundle
    - trace_context
    - contribution_scope
    - confidence_score
  review_status: pending
  dispute_status: none
  payment_eligibility: pending_review
```

This prepares allocation logic.

It does not execute settlement.

---

## 10. Event Type Influence on Allocation Intent

Different event types may influence Allocation Intent differently.

| Event Type | Typical Role in Allocation Intent |
|---|---|
| `access_event` | Weak supporting signal, often aggregated |
| `citation_event` | Explicit reference signal |
| `reuse_event` | Stronger structural contribution signal |
| `influence_event` | Contextual or inferred contribution signal |
| `allocation_trigger_event` | Direct candidate for allocation intent preparation |

This table is not a final scoring model.

It is a conceptual guide.

---

## 11. Review Status Requirements

Allocation Intent should usually require reviewed or review-pending events.

Recommended rule:

```text
raw event → not sufficient
pending event → may enter review
approved event → may support allocation candidate
disputed event → should preserve dispute state
rejected event → should not support allocation intent
superseded event → should defer to newer record
```

A disputed event may still be preserved.

But it should not silently become Allocation Intent without dispute awareness.

---

## 12. Dispute Status Requirements

Allocation Intent should preserve dispute status inherited from events.

Possible dispute states:

```text
none
contested
suspended
resolved
reversed
superseded
```

If any event in a bundle is disputed, the Allocation Intent should preserve
that status or explicitly explain why it does not block allocation preparation.

---

## 13. Allocation Readiness

Allocation Intent should still pass through Allocation Readiness.

```text
Royalty Event
        ↓
Allocation Intent
        ↓
Allocation Readiness
        ↓
Royalty OS
```

Allocation Readiness may evaluate:

- trace quality
- event confidence
- dispute status
- recipient clarity
- contribution scope
- allocation value uncertainty
- review completeness
- tolerance band requirements

Royalty Event Layer does not replace Allocation Readiness.

---

## 14. Relationship to Payment Rail Bridge

Payment Rail Bridge is downstream of Allocation Intent.

```text
Allocation Intent
        ↓
Payment Rail Bridge
        ↓
External Payment Rail
```

The bridge should receive allocation intent, not raw Royalty Events.

This ensures payment rails do not act on unreviewed event signals.

---

## 15. Anti-Automation Rule

The key rule is:

```text
Royalty Event should not automatically become payment.
```

A safer chain is:

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
Payment Rail Bridge
```

Each layer adds context and safety.

---

## 16. Non-Goals

This relationship does not imply that Royalty Events or Allocation Intent:

- execute payment
- determine legal ownership
- bypass Allocation Readiness
- replace human or multi-agent review
- calculate final royalty shares automatically
- remove dispute handling
- connect directly to payment rails
- make every access event payable

Allocation Intent is preparation, not execution.

---

## 17. Summary

Royalty Event Layer provides structured value-relevant events.

Allocation Intent prepares those events for possible allocation logic.

The relationship can be summarized as:

```text
Event = what happened in a value-relevant way.
Intent = what may be considered for allocation.
Bridge = how allocation may later circulate.
```

The purpose is to preserve the path from trace to value circulation without
allowing raw events to become premature claims.
