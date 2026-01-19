# ADR-0005: Sleeve Decision Support Features

Date: 2026-01-18
Status: Accepted

## Context
- [FACT] FOBS should provide decision support for the VLCC/Shipping/Offshore Drilling capital cycle sleeve.
- [FACT] FOBS should provide decision support for the Illiquidity/Neglect sleeve.
- [FACT] FOBS should provide decision support for the Real Assets sleeves.
- [FACT] Each sleeve has unique inputs and outputs.

## Decision
- [FACT] Create separate features per sleeve:
  - fobs-0002: sleeve-decision-support-vlcc-shipping-offshore
  - fobs-0003: sleeve-decision-support-illiquidity-neglect
  - fobs-0004: sleeve-decision-support-real-assets
- [FACT] Capture sleeve-specific requirements in their respective interview logs.

## Consequences
- [INFERENCE] Requirements will be gathered and specified per sleeve to avoid over-generalization.
- [INFERENCE] Implementation sequencing can prioritize sleeves independently.
