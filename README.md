# Royalty Event Layer v0.1

Royalty Event Layer defines a minimal event layer for converting trace, access,
reuse, citation, and influence signals into Royalty OS allocation-ready events.

This repository sits before Allocation Intent and Payment Rail Bridge.

It does not execute payments.

It does not determine legal ownership.

It defines how value-related events may be represented before they become
allocation candidates.

---

## Purpose

The purpose of this repository is to define a minimal Royalty Event Layer
within the broader Royalty OS architecture.

A trace record alone does not automatically create a royalty claim.

An access log alone does not automatically create a payment obligation.

An influence signal alone does not automatically become allocation.

The Royalty Event Layer exists to convert raw signals into structured,
review-aware, allocation-ready events.

---

## Core Position

The Royalty Event Layer sits between trace systems and allocation intent.

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

Its role is to define event objects that can later be reviewed, scored,
aggregated, disputed, or transformed into allocation intent.

---

## Why This Layer Is Needed

Royalty OS requires more than raw traces.

For example:

- a text may be accessed
- an idea may be cited
- a structure may be reused
- a model may refer to a source
- an AI agent may use a prior output
- a platform may record influence or engagement

However, these signals are not all equal.

They must be classified before they can support allocation.

The Royalty Event Layer provides that classification.

---

## Event Types

This repository defines five initial event types.

```text
access_event
citation_event
reuse_event
influence_event
allocation_trigger_event
```

Each event type represents a different relationship between trace and value.

---

## Event Type Overview

| Event Type | Meaning |
|---|---|
| `access_event` | A source, work, structure, or artifact was accessed or read |
| `citation_event` | A source was explicitly cited or referenced |
| `reuse_event` | A structure, expression, or component was reused |
| `influence_event` | A source influenced, or appears to have influenced, another output or structure |
| `allocation_trigger_event` | An event or event bundle became strong enough to move toward allocation intent |

---

## Core Principle

A Royalty Event is not a payment.

A Royalty Event is not a legal claim.

A Royalty Event is not proof of ownership.

A Royalty Event is a structured signal that may support later allocation logic.

```text
Trace becomes event.
Event becomes allocation candidate.
Allocation candidate may become allocation intent.
Allocation intent may later reach a payment rail.
```

---

## Relationship to Royalty OS

Royalty OS requires structured events before value can be allocated.

The Royalty Event Layer provides those events.

```text
Trace Architecture
        ↓
Royalty Event Layer
        ↓
Allocation Intent
        ↓
Royalty OS
```

Royalty OS may use royalty events to determine whether an allocation should be
prepared, reviewed, disputed, or rejected.

---

## Relationship to Payment Rail Bridge

This repository does not connect directly to payment rails.

Payment Rail Bridge operates later in the stack.

```text
Royalty Event Layer
        ↓
Allocation Intent
        ↓
Payment Rail Bridge
        ↓
External Payment Rail
```

The Payment Rail Bridge should only receive allocation intent after royalty
events have been reviewed, aggregated, and translated into allocation logic.

---

## Minimal Event Object

A minimal royalty event may contain:

```yaml
royalty_event:
  event_id: string
  event_type: access | citation | reuse | influence | allocation_trigger
  source_reference: string
  trace_reference: string
  actor_type: human | ai_agent | platform | system
  target_reference: string
  weight: number
  confidence: number
  review_status: pending | approved | disputed | rejected
```

This is only a conceptual object.

A formal JSON Schema is included in this repository for the current sample files.

---

## Repository Structure

```text
.
├── README.md
├── spec/
│   └── royalty-event-layer-v0.1.yaml
├── schemas/
│   └── royalty-event.schema.json
├── docs/
│   ├── architecture-overview.md
│   ├── event-types.md
│   ├── relationship-to-trace-architecture.md
│   ├── relationship-to-allocation-intent.md
│   └── relationship-to-payment-rail-bridge.md
├── examples/
│   ├── access-event.sample.yaml
│   ├── citation-event.sample.yaml
│   ├── reuse-event.sample.yaml
│   ├── influence-event.sample.yaml
│   └── allocation-trigger-event.sample.yaml
├── CHANGELOG.md
├── CITATION.cff
└── LICENSE
```

---

## Start Here

If you are new to this repository, read the documents in the following order.

### 1. Architecture Overview

Start with:

```text
docs/architecture-overview.md
```

This document explains the overall position of Royalty Event Layer.

It defines the core flow:

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

Royalty Event Layer sits between raw trace signals and allocation intent.

---

### 2. Event Types

Next, read:

```text
docs/event-types.md
```

This document defines the initial royalty event types:

```text
access_event
citation_event
reuse_event
influence_event
allocation_trigger_event
```

It explains how each event type differs in meaning, strength, and allocation relevance.

---

### 3. Relationship to Trace Architecture

Then read:

```text
docs/relationship-to-trace-architecture.md
```

This document explains how trace records become value-relevant event objects.

The basic relationship is:

```text
Trace Architecture
        ↓
Royalty Event Layer
        ↓
Allocation Intent
```

Trace records what happened.

Royalty Event Layer classifies whether what happened is value-relevant.

---

### 4. Relationship to Allocation Intent

Then read:

```text
docs/relationship-to-allocation-intent.md
```

This document explains how Royalty Events may support Allocation Intent.

The key distinction is:

```text
Royalty Event = what happened in a value-relevant way
Allocation Intent = what may be considered for allocation
```

A Royalty Event does not automatically become Allocation Intent.

---

### 5. Relationship to Payment Rail Bridge

Then read:

```text
docs/relationship-to-payment-rail-bridge.md
```

This document explains how Royalty Event Layer connects to the downstream
Payment Rail Bridge architecture.

The safe flow is:

```text
Royalty Event
        ↓
Allocation Intent
        ↓
Payment Rail Bridge
        ↓
External Payment Rail
```

Royalty Events should not directly trigger payment rails.

---

### 6. Specification File

After reading the documents, review:

```text
spec/royalty-event-layer-v0.1.yaml
```

This YAML file defines the conceptual specification, including:

- core position
- architecture flow
- principles
- event types
- minimal royalty event fields
- event lifecycle
- event weighting
- relationship to trace architecture
- relationship to allocation intent
- relationship to payment rail bridge
- safety principles
- non-goals

---

### 7. Schema

Then review:

```text
schemas/royalty-event.schema.json
```

This JSON Schema provides a flexible validation structure for the sample
Royalty Event objects.

It is intended for v0.1 sample validation and may be refined in later versions.

---

### 8. Examples

Finally, review the sample event files.

```text
examples/access-event.sample.yaml
examples/citation-event.sample.yaml
examples/reuse-event.sample.yaml
examples/influence-event.sample.yaml
examples/allocation-trigger-event.sample.yaml
```

These examples demonstrate the five initial event types.

#### Access Event

```text
examples/access-event.sample.yaml
```

Shows a low-relevance access or retrieval event.

#### Citation Event

```text
examples/citation-event.sample.yaml
```

Shows an explicit reference or attribution event.

#### Reuse Event

```text
examples/reuse-event.sample.yaml
```

Shows reuse or adaptation of a structure, schema, terminology, or conceptual module.

#### Influence Event

```text
examples/influence-event.sample.yaml
```

Shows an inferred influence event with uncertainty and alternative explanations.

#### Allocation Trigger Event

```text
examples/allocation-trigger-event.sample.yaml
```

Shows an event bundle strong enough to move toward Allocation Intent preparation.

This event still does not execute payment.

---

## Design Principles

### Events are not payments

A royalty event does not execute payment.

It only creates a structured signal that may later support allocation.

### Events are not legal ownership claims

This repository does not determine legal ownership.

It defines review-aware event records.

### Events must preserve trace context

Every royalty event should preserve its trace reference.

Without trace, the event becomes detached from its origin.

### Events should remain review-aware

Event confidence, review status, and dispute status should be preserved.

### Events should support allocation, not force it

An event may support allocation intent.

It should not automatically create allocation intent without review.

### Event types should remain distinguishable

Access, citation, reuse, influence, and allocation trigger events should not be
collapsed into one generic signal.

---

## Safety Structure

The safe flow is:

```text
Trace
   ↓
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

This repository focuses only on the Royalty Event layer.

It helps prevent raw signals from becoming premature allocation or payment claims.

---

## Non-Goals

This repository does not:

- execute payments
- define legal ownership
- replace copyright law
- bypass review
- bypass dispute resolution
- determine final royalty shares
- connect directly to payment rails
- claim that access alone creates payment obligation
- automatically convert influence into entitlement
- replace Allocation Readiness
- replace Royalty OS
- replace Payment Rail Bridge

It defines a minimal event layer for Royalty OS.

---

## Future Direction

Future versions may add:

- stricter JSON Schema
- valid and invalid examples
- event aggregation rules
- event weighting model
- dispute-aware event lifecycle
- allocation trigger thresholds
- validation workflow
- relationship to Seismic Score
- relationship to Structure Fingerprint
- relationship to Allocation Readiness
- relationship to Dispute Registry

---

## Status

Version: v0.1.0  
Status: Draft  
Maturity: Conceptual event layer with schema and examples  
Scope: Royalty OS event modeling

---

## Citation

If you use this specification, please cite this repository using `CITATION.cff`.

---

## License

MIT License
