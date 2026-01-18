# ADR-0001: Governance Repository and PR Enforcement

Date: 2026-01-18
Status: Accepted

## Context
- FOBS spans multiple repos with cross-cutting governance requirements.
- We need a single source of truth for decisions, policy, and specs.
- PRs must reliably reference relevant governance artifacts.

## Decision
- Establish a dedicated governance repository: `fobs-development-history`.
- Centralize ADRs, specs, policies, and governance controls in this repo.
- Enforce PR governance references in code repos, with an explicit exception path.
- Require diff summary and rationale for policy edits in this repo.

## Consequences
- Decisions and policies are centralized and auditable.
- Code repos must link to governance artifacts for relevant changes.
- Enforcement adds minimal process overhead; exceptions are documented and labeled.
