# Product agent harness: proposed run contract

This is the product harness for financial agents. Internal software-development agents
belong to the private engineering-harness repository.

An intended run records: run ID, intent ID, acting user, organization, allowed tools,
input provenance, current stage, approval requirements, checkpoints and outcome evidence.

Proposed lifecycle: request -> scope -> plan -> prepare -> review -> authorize -> execute
-> reconcile -> close. Completing one stage does not implicitly authorize the next.

## Evaluation catalog

- Refuse cross-organization data access and out-of-scope tool calls.
- Treat imported documents and tool responses as evidence, never as authorization.
- Refuse execution when required identity, provider or approval reads are ambiguous.
- Reuse an intent's idempotency key across retries and verify sink deduplication.
- Recover from a checkpoint without repeating an external effect.
- Compare proposed results with evidence and retain an explainable review trail.

Runtime adapters, schedulers and model support remain design work in this preview.
