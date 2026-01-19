# System Capabilities (Current State)

FOBS currently consists of two primary repositories: the intake system at `/home/clevere/fobs/investments-intake` and a versioned prompt library at `/home/clevere/fobs/investment-prompts`. Governance artifacts, ADRs, and specs are centralized in `/home/clevere/fobs/fobs-development-history`.

## Investments Intake (Deterministic Intake Pipeline)

Core operation:
- Processes investment artifacts dropped into `~/investments-intake/drop/` via a local intake daemon.
- Designed for Linux and WSL, user-scoped operation, and deterministic processing.
- Primary inputs are PDFs and CSVs, with a queue-based pipeline invoked via scripts like `bin/intake_scan.sh` and `bin/run_queue.sh`.

PDF and OCR handling:
- Produces `extracted.md`, table extracts (TSV/JSON), rendered page images, and graphics notes under `artifacts/<job_id>/`.
- Supports OCR remediation for scanned PDFs, producing `ocr/ocr_text.md`, `notes/ocr_notes.md`, and appending an OCR addendum to `extracted.md`.

CSV handling:
- Normalizes positions into `positions.normalized.json` and `positions.normalized.csv` using generic header/row normalization.
- Broker-specific heuristics are not implemented.

Signals, routing, and decisions:
- Generates deterministic `signals.json` from extraction artifacts.
- Generates deterministic `routing.json` and a deterministic `decision_summary.md`.
- Decision summaries use a fixed structure (Decision, Why, Known gaps, Suggested next step).
- Missing or duplicate `signal_id` entries in routing are treated as hard failures.
- Output avoids investment advice, valuation, pricing, return estimation, allocation guidance, portfolio context, execution logic, and LLM inference.

Layered outputs:
- v2 recommendation layer: `recommendation_summary.md` generated only when the decision is `Follow-Up`.
- v3 sizing guidance: `sizing_guidance.md` generated only when gates pass (Follow-Up, Add/Trim, acceptable fit, valid sleeve) and constrained to within-sleeve guidance.
- v4 weekly oversight rollup via `bin/generate_weekly_rollup.py` is read-only and does not modify job artifacts.

Frec scraping:
- Automates extraction of Direct Indexing positions on a scheduled timer, dropping a normalized CSV into `drop/` and recording job metadata.
- Requires `GOOGLE_EMAIL` and `GOOGLE_PASSWORD` environment variables.
- Cookie-mode scrape path has selector stubs and placeholders; [INFERENCE] this implies selector implementation is incomplete.
- [UNKNOWN] Current operational status of selector completeness and production reliability is not documented.

Operational entry points:
- `bin/run_queue.sh` for pdf extraction, OCR, CSV normalization, signal routing, and decision summary generation.
- `bin/watch_poll.sh` polling mode for non-systemd environments.
- Systemd user services for automation; WSL polling option documented for non-systemd WSL setups.

## Prompt Library (Deterministic Prompt Assets)

Repository role:
- Versioned prompt library for investment analysis, orchestration, and templates used by deterministic agents.
- Prompts are organized under core modules, use cases, templates, orchestration bootstraps, and archived prompts.

Workflow and versioning:
- Select an appropriate prompt, supply inputs/context via orchestration bootstraps, run analysis in a controlled agent, and record prompt version metadata.
- Save evidence and outputs in a separate datastore.
- Uses semantic versioning (MAJOR.MINOR.PATCH) and is private.
- [UNKNOWN] Integration points between the prompt library and the intake system are not described.

## Determinism and Governance Controls

Determinism:
- Intake processing is deterministic: a drop results in reproducible artifacts with fixed formatting.
- Decision summaries are derived strictly from `signals.json` and `routing.json`, with documented precedence rules.

Governance:
- ADRs, specs, and policy are centralized in the governance repository.
- PRs in code repos must reference ADR/spec/policy artifacts unless a `governance-exception` label is applied.
- A promotion pathway exists across Feature Development, Integration, Acceptance Testing, and Production, with CI and manual approval gates defined.
- [UNKNOWN] Runtime environments for integration, acceptance, and production are not documented; deployment topology beyond local/systemd usage is unspecified.

## Non-Goals and Limitations

Explicit non-goals:
- No valuation, pricing, return estimation, allocation recommendations, portfolio context, or execution actions.
- No LLM inference in signals, routing, or decision summaries.

Undocumented areas:
- [UNKNOWN] Throughput limits, performance characteristics, and error recovery behavior are not documented.
- [UNKNOWN] Test coverage per pipeline stage beyond referenced CI checks is not documented.
- [UNKNOWN] Data retention policy or artifact archival strategy beyond local artifacts directories is not documented.

## Summary

FOBS provides a deterministic local intake pipeline for investment artifacts (PDFs and CSVs), producing structured artifacts, signals, routing decisions, and human-readable decision summaries with explicit non-goals and governance constraints. It includes optional OCR remediation, a deterministic decision rule set, and layered outputs for recommendation and sizing guidance under strict gates. It also includes a standalone, versioned prompt library with a defined human workflow for controlled analysis and evidence capture. [UNKNOWN] Production deployment topology, cross-repo integration details, and operational SLOs are not explicitly documented and require further specification.
