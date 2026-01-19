# ADR-0004: Holdings News Intelligence

Date: 2026-01-18
Status: Accepted

## Context
- [FACT] FOBS should gather, collate, and process news about holdings that might influence valuation daily.
- [FACT] Holdings include anything owned, with emphasis on individual stocks, ETFs, and bonds.
- [FACT] The goal is situational awareness and disaster avoidance, not reacting to every news item.
- [FACT] Source priority: official filings -> press releases -> news.
- [FACT] Output format: on-demand status + disaster alerts during waking hours.
- [FACT] Waking hours: 6:30 am to 9:00 pm Central.
- [FACT] Disaster signals include bankruptcy, fraud, delisting, covenant breach, and regulatory action.
- [FACT] Sleeve-specific extensions may add additional signals (e.g., VLCC/Shipping/Offshore Drilling).
- [UNKNOWN] Alert delivery channel is TBD.

## Decision
- [FACT] Implement holdings news intelligence as defined in `specs/news-intelligence.md`.
- [FACT] Track the feature interview log in `specs/features/fobs-0001.md`.

## Consequences
- [INFERENCE] The system must support daily ingestion and prioritization of news sources.
- [INFERENCE] A wake-hours policy must be enforced for alerting.
- [INFERENCE] Delivery channel selection is a prerequisite for alert implementation.
