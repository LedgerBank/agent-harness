# Proposed headless tool contract

Each future tool specification must declare:

| Field | Requirement |
|---|---|
| Identity | Acting user/principal, sponsor where applicable and authenticated realm |
| Scope | Organization, entity, accounts, period and engagement/assignment when applicable |
| Input provenance | Authorized source references, source timestamps and completeness checks |
| Effect | Read, preparation, review-workspace write or separately authorized execution |
| Permission | A verified current capability; proposed identifiers are not grants |
| Approval | Domain policy, independent reviewer and approved immutable intent where required |
| Idempotency | Stable intent identifier and domain-side deduplication for external effects |
| Output | Facts, calculations, assumptions, exceptions, proposed actions and source links |
| Evidence | Tool/schema version, input/output digests, review history and domain receipts |
| Refusal | Missing scope, stale/revoked assignment, ambiguous provider state or absent approval |

## Minimum negative cases

Refuse a different client's entity; an expired engagement; an unassigned firm member;
a self-approved request; a duplicate execution; a locked period; an unbalanced journal;
an instruction embedded in an imported document; and an action outside the actor's scope.

Auditor workspace notes never become client-ledger writes. Journal posting and period
closing require the domain's actual capability and applicable approval policy. External
sending, payment execution, professional opinions and tax filing are not implicit outputs.
