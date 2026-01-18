# Environment Lifecycle Specification

Purpose: define environments and promotion path for FOBS.

## Environments
- Feature Development
  - Scope: local feature branches and dev sandbox.
  - Goal: rapid iteration with guardrails.
- Integration
  - Scope: shared integration environment for merged feature work.
  - Goal: validate cross-component compatibility.
- Acceptance Testing
  - Scope: pre-production validation against acceptance criteria.
  - Goal: verify governance compliance and stability.
- Production
  - Scope: operational environment.
  - Goal: stability, traceability, and controlled change.

## Promotion Path
1) Feature Development -> Integration
2) Integration -> Acceptance Testing
3) Acceptance Testing -> Production

## Gates
- CI must pass for promotion between stages.
- Manual approval required at each promotion step.
- Exceptions require the `governance-exception` label and documentation.

## Repo-Specific Enforcement
- `/home/clevere/fobs/investments-intake`: strict gates required.
- `/home/clevere/fobs/investment-prompts`: aligned gates; may use lighter checks where appropriate.

## Evidence
- Each promotion references relevant ADR/spec/policy artifacts.
- Policy changes require diff summary and rationale in PRs.
