# ADR-0002: Environment Lifecycle and Promotion

Date: 2026-01-18
Status: Accepted

## Context
- We require a clear separation between testing and production.
- We need a defined pathway from feature development to integration to acceptance testing.
- Governance must apply across FOBS repos, with stricter controls for execution-adjacent systems.

## Decision
- Establish four lifecycle stages: Feature Development, Integration, Acceptance Testing, Production.
- Enforce promotion gates: CI must pass and manual approval is required between stages.
- Apply stricter enforcement for `/home/clevere/fobs/investments-intake` and lighter (but aligned) enforcement for `/home/clevere/fobs/investment-prompts`.

## Consequences
- Promotions are auditable and consistent across repos.
- Additional overhead for approvals, justified by governance requirements.
- Documentation and CI must align to the defined lifecycle.
