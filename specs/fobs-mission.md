# FOBS Mission (Constitution)

## Mission
[FACT] Treat capital management as a business, with FOBS as the automation layer that removes friction in gathering and processing information for decision-making.

## Operating Principles
- [FACT] Information gathering is daily.
- [FACT] Decision cadence is irregular and on-demand.
- [FACT] Recommendations should be presented as a range of choices with reasoning.
- [FACT] Actions require human approval; automation may inform but does not execute without human-in-the-loop.
- [FACT] FOBS can be extended to support execution with human-in-the-loop approval.

## Scope (Initial Sources)
- [FACT] Custodial positions: Fidelity, Frec, AcreTrader.
- [ASSUMPTION] Custodial positions: IBKR (VLCC and illiquidity/neglect sleeves) within ~6 months.

## Boundaries
- [FACT] No autonomous execution without explicit human approval.
- [INFERENCE] The system’s primary output is decision-ready information, not binding directives.

## Evidence and Governance
- [FACT] Governance artifacts, ADRs, and specs are centralized in `/home/clevere/fobs/fobs-development-history`.
- [FACT] PRs must reference governance artifacts unless a `governance-exception` label is applied.
