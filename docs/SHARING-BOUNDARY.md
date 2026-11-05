# Public core and private operating profiles

Status: proposed sharing boundary. This document publishes original interface design, not an extraction of an existing internal harness.

## What can be shared

| Surface | Public candidate | Kept private |
| --- | --- | --- |
| Runtime | Generic Rust run state machine and extension interfaces | Organization deployment and operating configuration |
| Tools | Schemas, effect classes and synthetic adapters | Live credentials, actual grants and restricted connectors |
| Policy | Policy evaluation interface and synthetic examples | Real role bindings, approval chains, budgets and exceptions |
| Memory | Scoped retrieval contracts and provenance formats | Memory contents, RAG corpora, private prompts and customer evidence |
| Skills | Independently reviewed generic workflows using synthetic data | Proprietary business procedures and engagement-specific instructions |
| Evaluation | Fault cases, fake providers and conformance fixtures | Real incidents, private transcripts and production traces |

The same runtime can be reusable while policy and data remain private. Public financial examples must use synthetic evidence and sandbox interfaces; publishing a tool schema does not expose or activate that tool for a caller.

## Distribution audiences

- Public developers receive reviewed contracts, examples and, after implementation qualification, a release artifact.
- Staff receive a managed client profile with their own identity and the capabilities returned by the authorized gateway.
- Partners receive separately scoped adapters or private integration packages under their engagement boundary.
- Operators administer private orchestration and deployment profiles. A user client does not receive the controller's credentials or private memory.

## Release boundary

Existing private source remains in place. Reuse requires component provenance, dependency/license review, removal of organization configuration, synthetic fixtures and independent verification of the actual release contents. Redacting a few strings is not an extraction strategy. No existing source, canonical memory or internal documents are migrated by this design update.

Credentials are provisioned outside Git and outside public packages. Private configuration is not a public artifact with a hidden download link. An installer must discover its authorized profile and validate the backend's actual enforcement; it must not claim tenant isolation merely because it passes a role name to a server.

This repository currently publishes design documents only. There is no crate release, runtime deployment or new access grant in this change. An open-source license for future implementation code remains a separate recorded release decision.
