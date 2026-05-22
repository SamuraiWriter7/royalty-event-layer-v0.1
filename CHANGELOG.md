# Changelog

All notable changes to this repository will be documented in this file.

---

## v0.1.0 - Draft

Initial draft release of Royalty Event Layer v0.1.

Added:

- `README.md`
- `spec/royalty-event-layer-v0.1.yaml`
- `schemas/royalty-event.schema.json`
- `docs/architecture-overview.md`
- `docs/event-types.md`
- `docs/relationship-to-trace-architecture.md`
- `docs/relationship-to-allocation-intent.md`
- `docs/relationship-to-payment-rail-bridge.md`
- `examples/access-event.sample.yaml`
- `examples/citation-event.sample.yaml`
- `examples/reuse-event.sample.yaml`
- `examples/influence-event.sample.yaml`
- `examples/allocation-trigger-event.sample.yaml`
- `CITATION.cff`
- `LICENSE`

Defined:

- Royalty Event Layer as the bridge between trace systems and allocation intent
- Initial royalty event types:
  - `access_event`
  - `citation_event`
  - `reuse_event`
  - `influence_event`
  - `allocation_trigger_event`
- Event lifecycle model
- Event weighting guidance
- Review and dispute preservation principles
- Relationship to Trace Architecture
- Relationship to Allocation Intent
- Relationship to Payment Rail Bridge
- Flexible JSON Schema for sample royalty event objects

Clarified:

- Royalty Events are not payments
- Royalty Events are not legal ownership claims
- Access does not automatically create payment obligation
- Event records should preserve trace context
- Event records should remain review-aware and dispute-aware
- Payment execution belongs downstream of Allocation Intent and Payment Rail Bridge

Status:

- Version: v0.1.0
- Status: Draft
- Maturity: Conceptual event layer with schema and examples
- Scope: Royalty OS event modeling
