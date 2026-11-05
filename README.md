# agent-harness

Product agent harness design, evaluation cases and execution boundaries.

**Status: presentation preview.** This repository contains scope and design documentation. It does not contain a released implementation or a live service.

## Role in the headless platform

LedgerBank is being organized around a common financial capability layer. Applications,
accounting workflows, SDKs, the CLI and agents are intended to consume that layer through
reviewed interfaces. Financial authority and permissions remain in the platform.

**Primary audience:** agents. **Repository visibility:** public.

## Planned scope

- Specify the product runtime for agents consuming the headless platform.
- Define run identity, scoped tools, checkpoints, approvals and audit evidence.
- Design model adapters without binding domain authority to one model vendor.
- Catalog evaluations for tenant isolation, untrusted evidence and duplicate actions.

## Read next

- [Rust core architecture](docs/RUST-CORE.md): reusable execution mechanics and proposed workspace
- [Public/private sharing boundary](docs/SHARING-BOUNDARY.md): what can be shared and what remains organization-specific
- [Scope and boundaries](docs/SCOPE.md)
- [First implementation acceptance criteria](docs/ACCEPTANCE.md)
- [Current repository status](STATUS.md)
- [developers](https://github.com/LedgerBank/developers) for the proposed public architecture and integration map

## Preview boundary

This is a new presentation scaffold. Existing repositories, branches, services and
documents have not been migrated here. Package names, hosted endpoints, releases and
support commitments will be documented only when they exist and have been verified.
