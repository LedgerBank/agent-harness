# Rust harness core: proposed architecture

Status: design only. No Rust runtime, crate, executable, hosted endpoint or supported release is delivered by this document.

## Product boundary

The reusable harness coordinates a run. The headless financial platform owns financial authorization and business invariants. A model response, a client-side role, a Rust type, or a completed review does not independently grant permission to execute a financial action.

The proposed reusable core is written in Rust. Internal engineering, staff tools, accounting workflows and external product agents can consume the same contracts with separate identities and policy profiles. Private organization configuration is supplied through authenticated adapters; it is not compiled into a public release.

## Proposed workspace

These are design labels, not published crate names.

| Component | Responsibility |
| --- | --- |
| `harness-contracts` | Run/intent IDs, actor and tenant context, tool manifests, effect classes, approval bindings and execution receipts |
| `harness-core` | Explicit state transitions, bounded scheduling, checkpoints, cancellation and reconciliation decisions |
| `harness-store` | Persistence interfaces and reference fixtures for atomic intent/checkpoint/outbox operations |
| `harness-evals` | Synthetic conformance scenarios and fault-injection fixtures |

The `ledgerbank-rust` repository remains the financial API client. `ledgerbank-cli` can compose that client and the harness core. `ledgerbank-mcp` owns the LedgerBank MCP adapter; it should use the official Rust MCP SDK rather than implement a competing protocol stack. Generic skills live in `agent-skills`. Private engineering profiles live in `engineering-harness`.

## Run and effect contracts

Preserve the run contract: request -> scope -> plan -> prepare -> review -> authorize -> execute -> reconcile -> close. A checkpoint records facts; reaching it does not authorize the next stage. An ambiguous external result enters an awaiting-reconciliation state rather than being retried as if nothing happened.

Each effect binds its intent ID, actor, tenant, allowed action, payload digest, required authorization, expiry and observed result. The authoritative service validates those bindings at execution time. A local allow-list is an additional constraint, not a substitute for server authorization.

Persistence can coordinate local intent/outbox state, but cannot make an arbitrary remote action exactly once. External execution requires target idempotency or equivalent deduplication, stable retry keys, and receipt reconciliation. Replaying a run must not replay a completed effect.

Unknown usage, price or external state remains explicitly unknown. Admission policies receive that state rather than a fabricated zero. Model calls and subprocesses have owned lifecycles; cancellation must clean up only resources belonging to the current run and preserve independently owned processes.

## Adapters and durability

Keep model, memory, tool, persistence and workflow-engine integrations behind typed interfaces. Memory adapters return scoped evidence with provenance and source revision; they do not distribute an organization's memory store. External evidence cannot modify the run's authority.

Temporal's official Rust SDK is a candidate for durable workflow and activity adapters. Existing workflows are not automatically portable: compatibility, replay, serialization, task queues and worker versioning require explicit qualification before any migration. A Rust SDK release does not certify compatibility with a particular deployment.

MCP adapters should qualify initialization, negotiated capabilities, transport, cancellation and child-process cleanup against the official Rust SDK. Select and pin dependency versions during implementation review; this design does not promise compatibility with an untested version.

## First implementation acceptance

- A synthetic offline run can prepare, checkpoint, resume and reconcile without a real credential or financial provider.
- Cross-tenant calls, wrong actors, forged or expired approvals, unavailable authorization reads and unknown required cost are refused.
- Crash-after-effect and duplicate-intent tests prove that recovery does not duplicate an external effect.
- Untrusted documents cannot expand scope; a missing memory authorization never falls back to unrestricted retrieval.
- Independent reviewers verify state transitions and receipts. Compilation alone is not proof of permission or delivery.

## Primary references

- [Official Rust MCP SDK](https://github.com/modelcontextprotocol/rust-sdk)
- [Official Temporal Rust SDK](https://github.com/temporalio/sdk-rust)
- [Temporal Rust SDK stable release](https://github.com/temporalio/sdk-rust/releases/tag/v1.0.0)
