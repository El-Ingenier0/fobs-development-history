# Cross-Link Checklist

Purpose: ensure decisions, specs, and policies are discoverable from code repos and that code changes reference governance artifacts.

## Repos
- /home/clevere/fobs/fobs-development-history (canonical)
- /home/clevere/fobs/investments-intake
- /home/clevere/fobs/investment-prompts

## Checklist
- README in each code repo links to the governance repo.
- `docs/governance/REFERENCE.md` exists in each code repo and points to the canonical repo.
- PR templates include a Governance References section.
- PRs reference an ADR/spec/policy or use the `governance-exception` label.
- Governance repo ADRs/specs/policies cross-reference impacted code repos when applicable.
- Policy changes include a diff summary and rationale.
- CODEOWNERS covers `docs/decisions/`, `docs/governance/`, and `policy/`.

## Cadence
- Review monthly or whenever a new repo is added.

## Status Tracking
- Record completed checklist items in the relevant ADR or a dated note in this repo.
