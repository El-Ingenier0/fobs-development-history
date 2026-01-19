# ADR-0003: FOBS Mission and Scope

Date: 2026-01-18
Status: Accepted

## Context
- [FACT] The user wants capital management treated as a business.
- [FACT] FOBS should remove friction in gathering and processing information needed for decisions.
- [FACT] Information gathering must be daily; decisions are made as needed.
- [FACT] Recommendations should present a range of choices with reasoning.
- [FACT] Execution requires human-in-the-loop approval; automation may inform but not execute without approval.
- [FACT] FOBS can be extended to support execution with human-in-the-loop approval.
- [FACT] Initial custodial sources: Fidelity, Frec, AcreTrader.
- [ASSUMPTION] IBKR for VLCC and illiquidity/neglect sleeves within ~6 months.

## Decision
- [FACT] Adopt the mission and operating principles codified in `specs/fobs-mission.md` as the system constitution.

## Consequences
- [INFERENCE] System design prioritizes deterministic information processing and decision readiness over autonomous action.
- [INFERENCE] Governance and auditability are core requirements because the system supports capital-management workflows.
- [INFERENCE] Future execution capabilities will require explicit human approval checkpoints by design.
