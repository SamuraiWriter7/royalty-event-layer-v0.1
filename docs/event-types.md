# Event Types

This document defines the initial event types used in Royalty Event Layer v0.1.

A Royalty Event is a structured signal that may support later allocation logic.

It is not a payment.

It is not a legal ownership claim.

It is not final proof of contribution.

It is a review-aware, dispute-aware event object that preserves trace context.

---

## 1. Event Type Overview

Royalty Event Layer v0.1 defines five initial event types.

| Event Type | Meaning | Default Allocation Relevance |
|---|---|---|
| `access_event` | A source, work, structure, or artifact was accessed or consumed | Low |
| `citation_event` | A source was explicitly cited, referenced, or attributed | Medium |
| `reuse_event` | A structure, component, phrase, pattern, or concept was reused | Medium to High |
| `influence_event` | A source appears to have influenced a downstream artifact or behavior | Variable |
| `allocation_trigger_event` | An event or event bundle is strong enough to move toward allocation intent | High |

These event types should remain distinguishable.

Access should not be collapsed into citation.

Citation should not be collapsed into reuse.

Reuse should not be collapsed into influence.

Influence should not be collapsed into allocation readiness.

---

## 2. `access_event`

An `access_event` represents that a source, work, structure, artifact, or record
was accessed, read, viewed, fetched, queried, opened, or otherwise consumed.

### Typical Sources

An access event may come from:

- read logs
- access logs
- API calls
- AI agent fetch records
- platform view records
- document open records
- retrieval traces
- model context retrieval logs

### Example Situations

```text
An AI agent fetches a specification document.
A platform records that a user opened an article.
A model retrieves a source artifact into context.
A system reads a trace record for downstream processing.
```

### Allocation Relevance

Default relevance:

```text
low
```

Access may indicate consumption, but access alone should not automatically create
payment obligation.

Access events often require aggregation, review, or additional downstream signals
before they can support allocation intent.

### Cautions

Access events should not be treated as:

- proof of influence
- proof of reuse
- proof of contribution
- payment obligation
- legal entitlement

Correct interpretation:

```text
Something was consumed or accessed.
```

Incorrect interpretation:

```text
Payment is automatically owed because access occurred.
```

### Minimal Example

```yaml
royalty_event:
  event_id: evt_access_001
  event_type: access
  source_reference: source_doc_001
  trace_reference: trace_access_001
  actor_type: ai_agent
  actor_reference: agent_001
  target_reference: null
  weight: 0.10
  confidence: 0.80
  review_status: pending
  dispute_status: none
  allocation_relevance: low
```

---

## 3. `citation_event`

A `citation_event` represents explicit citation, reference, attribution,
source mention, or link-based acknowledgment.

### Typical Sources

A citation event may come from:

- bibliography records
- footnotes
- hyperlinks
- source references
- AI output citations
- article references
- documentation references
- academic or technical citations

### Example Situations

```text
An article cites a prior specification.
An AI output includes a source reference.
A GitHub README links to a related protocol.
A research paper references a conceptual framework.
```

### Allocation Relevance

Default relevance:

```text
medium
```

Citation is usually stronger than access because it explicitly identifies a
source relationship.

However, citation still does not automatically determine contribution weight.

### Cautions

Citation events should preserve:

- citation context
- citation quality
- citation target
- citation intent
- review status

A shallow citation may have lower allocation relevance than a deep structural reuse.

Correct interpretation:

```text
A source was explicitly referenced.
```

Incorrect interpretation:

```text
A citation alone determines final royalty allocation.
```

### Minimal Example

```yaml
royalty_event:
  event_id: evt_citation_001
  event_type: citation
  source_reference: source_spec_001
  trace_reference: trace_citation_001
  actor_type: human
  actor_reference: author_001
  target_reference: article_001
  weight: 0.35
  confidence: 0.90
  review_status: pending
  dispute_status: none
  allocation_relevance: medium
```

---

## 4. `reuse_event`

A `reuse_event` represents reuse of a structure, expression, component, schema,
example, design pattern, field model, phrase, terminology, or conceptual module.

### Typical Sources

A reuse event may come from:

- copied schema fields
- reused protocol modules
- repeated architectural patterns
- reused diagrams
- reused terminology
- adapted examples
- transformed text
- derived implementation patterns

### Example Situations

```text
A schema field structure is reused in another specification.
A protocol example is adapted into another repository.
A conceptual model is reused with different terminology.
A phrase or naming pattern appears in downstream documentation.
```

### Allocation Relevance

Default relevance:

```text
medium_to_high
```

Reuse may be highly relevant to allocation because it suggests that an earlier
structure helped shape a later artifact.

However, reuse must be distinguished from coincidence, common patterns,
or generic design conventions.

### Cautions

Reuse events should preserve:

- reused component description
- similarity basis
- transformation notes
- confidence
- uncertainty
- dispute status

Correct interpretation:

```text
A source structure appears to have been reused or adapted.
```

Incorrect interpretation:

```text
Any similarity automatically proves derivation or ownership.
```

### Minimal Example

```yaml
royalty_event:
  event_id: evt_reuse_001
  event_type: reuse
  source_reference: source_schema_001
  trace_reference: trace_reuse_001
  actor_type: organization
  actor_reference: org_001
  target_reference: downstream_schema_001
  weight: 0.62
  confidence: 0.76
  review_status: pending
  dispute_status: none
  allocation_relevance: high
```

---

## 5. `influence_event`

An `influence_event` represents inferred influence from one source, structure,
idea, artifact, or model output to another downstream artifact, behavior,
document, or system.

### Typical Sources

An influence event may come from:

- structural similarity
- lineage analysis
- model output comparison
- repeated conceptual patterns
- semantic similarity
- historical sequence
- citation plus transformation
- multi-source convergence

### Example Situations

```text
A downstream document reflects the structure of an earlier article.
An AI output follows a known conceptual framework.
A protocol appears to inherit architecture from a prior specification.
Multiple artifacts converge around an earlier terminology system.
```

### Allocation Relevance

Default relevance:

```text
variable
```

Influence can be important, but it is often uncertain.

It should preserve confidence, uncertainty, and review status.

### Cautions

Influence events are especially sensitive.

They should not be treated as automatic proof of ownership, copying, or direct derivation.

Influence may be:

- direct
- indirect
- partial
- weak
- strong
- coincidental
- contested
- multi-source

Correct interpretation:

```text
A source may have influenced a downstream artifact.
```

Incorrect interpretation:

```text
Influence automatically proves ownership or payment obligation.
```

### Minimal Example

```yaml
royalty_event:
  event_id: evt_influence_001
  event_type: influence
  source_reference: source_framework_001
  trace_reference: trace_influence_001
  actor_type: system
  actor_reference: system_001
  target_reference: downstream_doc_001
  weight: 0.48
  confidence: 0.64
  review_status: pending
  dispute_status: none
  allocation_relevance: medium
```

---

## 6. `allocation_trigger_event`

An `allocation_trigger_event` represents an event, or aggregation of events,
strong enough to move toward allocation intent preparation.

This event type sits closest to Allocation Intent.

It is still not a payment instruction.

### Typical Sources

An allocation trigger event may come from:

- aggregated citation events
- reviewed reuse events
- high-confidence influence bundles
- combined trace and score evidence
- allocation readiness review
- threshold-based event bundles
- human or multi-agent approval

### Example Situations

```text
A bundle of citation and reuse events passes review.
A trace bundle supports allocation readiness.
A high-confidence lineage relation becomes allocation-relevant.
A multi-agent review approves allocation intent preparation.
```

### Allocation Relevance

Default relevance:

```text
high
```

This event type indicates that the system may prepare allocation intent.

However, it should still pass allocation readiness and dispute checks.

### Cautions

An allocation trigger event should not be treated as:

- direct payment
- final allocation
- legal entitlement
- irreversible judgment
- dispute-free conclusion

Correct interpretation:

```text
The event bundle is strong enough to move toward allocation intent.
```

Incorrect interpretation:

```text
Payment should be executed immediately.
```

### Minimal Example

```yaml
royalty_event:
  event_id: evt_allocation_trigger_001
  event_type: allocation_trigger
  source_reference: source_framework_001
  trace_reference: trace_bundle_001
  actor_type: system
  actor_reference: review_system_001
  target_reference: allocation_intent_candidate_001
  weight: 0.84
  confidence: 0.81
  review_status: approved
  dispute_status: none
  allocation_relevance: trigger_candidate
```

---

## 7. Event Type Comparison

| Event Type | Signal Strength | Requires Review | Can Trigger Payment Directly |
|---|---:|---:|---:|
| `access_event` | Low | Yes | No |
| `citation_event` | Medium | Yes | No |
| `reuse_event` | Medium to High | Yes | No |
| `influence_event` | Variable | Yes | No |
| `allocation_trigger_event` | High | Yes | No |

No event type should directly trigger payment.

All payment-related actions must pass through Allocation Intent, Royalty OS,
and Payment Rail Bridge.

---

## 8. Event Escalation

Events may escalate through aggregation.

```text
access_event
        ↓
citation_event
        ↓
reuse_event
        ↓
influence_event
        ↓
allocation_trigger_event
```

This is not a mandatory sequence.

It is only a conceptual escalation pattern.

For example:

- many access events may support attention analysis
- citation plus reuse may support contribution review
- reuse plus influence may support allocation relevance
- reviewed event bundles may support allocation trigger

Escalation should remain review-aware and dispute-aware.

---

## 9. Event Bundles

A single event may be weak.

A bundle of events may be stronger.

Example bundle:

```yaml
event_bundle:
  bundle_id: bundle_001
  source_reference: source_framework_001
  events:
    - evt_access_001
    - evt_citation_001
    - evt_reuse_001
    - evt_influence_001
  aggregate_confidence: 0.78
  allocation_relevance: high
  review_status: pending
```

Event bundles may help prepare allocation intent.

However, bundles should not bypass review.

---

## 10. Event Anti-Collapse Rule

The core design rule is:

```text
Do not collapse different event types into one generic influence signal.
```

Why?

Because each event type means something different.

```text
Access means consumption.
Citation means explicit reference.
Reuse means structural borrowing or adaptation.
Influence means possible downstream effect.
Allocation trigger means readiness for allocation preparation.
```

Keeping these distinctions prevents premature or unfair allocation.

---

## 11. Summary

Royalty Event Layer v0.1 defines five initial event types:

```text
access_event
citation_event
reuse_event
influence_event
allocation_trigger_event
```

Each event type has different meaning, different strength, and different
allocation relevance.

The purpose of this layer is to convert raw traces into structured,
review-aware, dispute-aware events.

In short:

```text
Trace records what happened.
Event type defines what kind of value-relevant thing happened.
Allocation Intent determines whether value may later flow.
```
