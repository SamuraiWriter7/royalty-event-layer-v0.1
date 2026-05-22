# Architecture Overview

Royalty Event Layer v0.1 defines the event layer between trace systems and
allocation intent.

It converts trace, access, citation, reuse, and influence signals into
structured Royalty Events.

A Royalty Event is not a payment.

A Royalty Event is not a legal ownership claim.

A Royalty Event is a structured signal that may later support allocation logic
inside Royalty OS.

---

## 1. Core Position

The Royalty Event Layer sits between trace records and allocation intent.

```text
Trace / Access / Impact
        ↓
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

This repository focuses only on the Royalty Event Layer.

It does not define payment execution.

It does not define final allocation.

It does not connect directly to payment rails.

---

## 2. Why This Layer Is Needed

Raw signals are not enough for Royalty OS.

For example:

- a document may be accessed
- a source may be cited
- a structure may be reused
- an idea may influence another output
- an AI agent may reference a prior artifact
- a platform may record engagement or usage

However, these signals have different meanings.

Access is not the same as citation.

Citation is not the same as reuse.

Reuse is not the same as influence.

Influence is not the same as allocation readiness.

The Royalty Event Layer separates these signals into explicit event types.

---

## 3. Core Flow

The basic flow is:

```text
Raw Signal
   ↓
Event Classification
   ↓
Royalty Event
   ↓
Review / Dispute Context
   ↓
Allocation Relevance
   ↓
Allocation Intent Candidate
```

This flow prevents raw traces from being treated as automatic payment claims.

---

## 4. Layer Responsibilities

### Trace / Signal Sources

Upstream systems may provide raw signals.

Examples include:

- access logs
- citation records
- reuse records
- influence signals
- structure fingerprint matches
- communication traces
- model reference events
- platform usage logs

These signals are not yet allocation-ready.

They must be classified.

---

### Royalty Event Layer

The Royalty Event Layer classifies raw signals into structured events.

Initial event types include:

```text
access_event
citation_event
reuse_event
influence_event
allocation_trigger_event
```

The layer preserves:

- source reference
- trace reference
- actor type
- target reference
- event type
- weight
- confidence
- review status
- dispute status
- allocation relevance

This allows downstream systems to review and process the event responsibly.

---

### Allocation Intent

Allocation Intent is downstream of the Royalty Event Layer.

A Royalty Event may support Allocation Intent, but it does not automatically
create Allocation Intent.

Allocation Intent should usually require:

- event review
- confidence evaluation
- aggregation
- dispute awareness
- allocation readiness checks

---

### Payment Rail Bridge

Payment Rail Bridge is further downstream.

```text
Royalty Event
   ↓
Allocation Intent
   ↓
Payment Rail Bridge
```

A Royalty Event should not directly execute payment.

Payment circulation belongs to a later layer.

---

## 5. Event Types

### Access Event

An `access_event` represents that a source, work, structure, or artifact was
accessed, read, viewed, queried, fetched, or otherwise consumed.

Examples:

- an AI agent accesses a document
- a platform records a read event
- a human reader opens a work
- a system fetches a source artifact

Access events may have allocation relevance, but access alone should not
automatically create payment obligation.

---

### Citation Event

A `citation_event` represents explicit citation, attribution, source mention,
or reference.

Examples:

- an article cites a source
- an AI output includes a source reference
- a document links to a prior specification
- a paper references a framework

Citation events are stronger than access events, but still require review.

---

### Reuse Event

A `reuse_event` represents reuse of a structure, expression, component,
schema, example, design pattern, or conceptual module.

Examples:

- a schema component is reused
- a protocol field structure is reused
- a conceptual architecture is reused
- terminology is reused in a downstream artifact

Reuse events may be highly relevant to allocation, but they must be
distinguished from coincidence or generic patterns.

---

### Influence Event

An `influence_event` represents inferred influence from one source, structure,
or idea to another output, artifact, model behavior, or document.

Examples:

- a downstream document shows structural influence
- an AI output reflects a prior conceptual framework
- a design follows a known lineage pattern
- multiple artifacts converge around a prior structure

Influence can be uncertain.

Therefore, influence events should preserve confidence and uncertainty.

---

### Allocation Trigger Event

An `allocation_trigger_event` represents an event or event bundle strong enough
to move toward allocation intent preparation.

Examples:

- reviewed citation and reuse events exceed a threshold
- a trace bundle supports allocation review
- impact score and lineage evidence support readiness review
- dispute-aware review approves allocation preparation

A trigger event is still not a payment instruction.

It only means the event may move toward allocation intent.

---

## 6. Event Lifecycle

A Royalty Event may move through the following lifecycle:

```text
raw_signal_detected
        ↓
classified_as_event
        ↓
pending_review
        ↓
approved / disputed / rejected
        ↓
aggregated
        ↓
allocation_candidate
        ↓
allocation_triggered
```

It may also become:

```text
superseded
```

if a newer or more accurate record replaces it.

---

## 7. Review and Dispute Awareness

Royalty Events must preserve review and dispute context.

Possible review statuses include:

```text
pending
approved
disputed
rejected
superseded
```

Possible dispute statuses include:

```text
none
contested
suspended
resolved
reversed
superseded
```

This prevents event records from becoming irreversible claims too early.

---

## 8. Minimal Event Shape

A minimal Royalty Event may look like this:

```yaml
royalty_event:
  event_id: evt_sample_001
  event_type: citation
  source_reference: origin_sample_001
  trace_reference: trace_sample_001
  actor_type: ai_agent
  actor_reference: agent_sample_001
  target_reference: output_sample_001
  weight: 0.42
  confidence: 0.78
  review_status: pending
  dispute_status: none
  allocation_relevance: medium
  created_at: "2026-05-20T00:00:00Z"
  notes: >
    Sample citation event. This does not create payment or legal entitlement.
```

This object is conceptual.

Formal validation may be added in later versions.

---

## 9. Relationship to Trace Architecture

Trace Architecture records evidence context.

Royalty Event Layer classifies trace-related signals into event objects.

```text
Trace Architecture
        ↓
Royalty Event Layer
        ↓
Allocation Intent
```

A trace record says:

```text
Something happened.
```

A Royalty Event says:

```text
This happened in a value-relevant way.
```

This distinction is essential.

---

## 10. Relationship to Allocation Intent

Allocation Intent may be prepared from reviewed, aggregated, or trigger-level
Royalty Events.

```text
Royalty Event
        ↓
Event Bundle
        ↓
Allocation Candidate
        ↓
Allocation Intent
```

No single event type should automatically become allocation intent without
review-aware processing.

---

## 11. Relationship to Payment Rail Bridge

Payment Rail Bridge operates downstream of Allocation Intent.

Royalty Events do not directly connect to payment rails.

```text
Royalty Event
        ↓
Allocation Intent
        ↓
Payment Rail Bridge
        ↓
External Payment Rail
```

This separation prevents raw events from becoming automatic financial actions.

---

## 12. Safety Principles

This architecture follows several safety principles.

### Events are not payments

A Royalty Event must not execute payment directly.

### Events are not ownership claims

A Royalty Event does not determine legal authorship, copyright, or ownership.

### Access does not automatically equal payment

An access event may support later analysis, but access alone should not create
automatic payment obligation.

### Events require review

Events should preserve review status before downstream allocation.

### Disputes must be preserved

Event records should preserve dispute, correction, rejection, reversal, and
supersession paths.

### Event types must remain distinguishable

Access, citation, reuse, influence, and allocation trigger events should not
be collapsed into one generic signal.

---

## 13. Non-Goals

This architecture does not:

- execute payments
- determine legal ownership
- replace copyright law
- calculate final royalty shares
- connect directly to payment rails
- convert access logs into automatic payment
- bypass review
- bypass dispute handling
- replace Allocation Readiness
- replace Royalty OS

It defines the event layer before allocation.

---

## 14. Summary

Royalty Event Layer v0.1 defines the missing layer between trace and allocation.

```text
Trace becomes event.
Event becomes allocation candidate.
Allocation candidate may become allocation intent.
Allocation intent may later reach a payment rail.
```

The purpose of this layer is to prevent raw signals from becoming premature
claims while still preserving their value relevance.

In short:

```text
Trace records what happened.
Royalty Events classify what matters.
Allocation Intent prepares what may flow.
```
