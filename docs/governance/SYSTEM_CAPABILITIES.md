# System Capabilities (Current State)

[FACT] The Family Office Bespoke System (FOBS) currently consists of two primary repositories: the intake system at `/home/clevere/fobs/investments-intake` and a versioned prompt library at `/home/clevere/fobs/investment-prompts`. [FACT] Governance artifacts, ADRs, and specs are centralized in `/home/clevere/fobs/fobs-development-history`.

## Investments Intake (Deterministic Intake Pipeline)

[FACT] The intake system runs as a local "intake daemon" that processes investment artifacts dropped into `~/investments-intake/drop/`. [FACT] It is designed to be installable on Linux and WSL, user-scoped, deterministic, and avoids secrets in git. [FACT] The primary inputs are PDFs and CSVs, with a queue-based pipeline invoked via scripts such as `bin/intake_scan.sh` and `bin/run_queue.sh` for specific stages.

[FACT] For PDFs, the system produces `extracted.md`, table extracts in TSV/JSON, rendered page images, and graphics notes, all stored under `artifacts/<job_id>/`. [FACT] OCR remediation is supported for scanned PDFs, producing `ocr/ocr_text.md`, `notes/ocr_notes.md`, and appending an OCR addendum to `extracted.md`. [FACT] For CSVs, the system normalizes positions into `positions.normalized.json` and `positions.normalized.csv` using a generic header/row normalization process.

[FACT] The pipeline then generates deterministic `signals.json` from extraction artifacts, followed by deterministic `routing.json` and a deterministic `decision_summary.md`. [FACT] Decision summaries follow a fixed structure (Decision, Why, Known gaps, Suggested next step), and decision selection is deterministic based on signal categories and routing actions. [FACT] Missing or duplicate `signal_id` entries in routing are treated as hard failures. [FACT] The decision summary explicitly avoids investment advice, valuation, pricing, return estimation, allocation guidance, portfolio context, or execution logic, and it does not use LLM inference.

[FACT] A v2 recommendation layer exists as `recommendation_summary.md`, generated only when the decision is `Follow-Up`. [FACT] A v3 sizing guidance layer exists as `sizing_guidance.md`, generated only when gates pass (Follow-Up, Add/Trim, acceptable fit, valid sleeve), and is constrained to within-sleeve guidance. [FACT] A v4 weekly oversight rollup can be generated via `bin/generate_weekly_rollup.py` as a read-only summary that does not modify job artifacts.

[FACT] The intake system includes a Frec scraper that can automate extraction of Direct Indexing positions on a scheduled timer, dropping a normalized CSV into `drop/` for intake and recording job metadata. [FACT] The Frec scraper requires `GOOGLE_EMAIL` and `GOOGLE_PASSWORD` environment variables. [FACT] The README also notes a cookie-mode scrape path with selector stubs and placeholders, implying that selector implementation is incomplete. [UNKNOWN] The current operational status of selector completeness and the reliability of Frec extraction in production are not documented in the provided materials.

[FACT] Operational entry points include `bin/run_queue.sh` for pdf extraction, OCR, CSV normalization, signal routing, and decision summary generation, as well as a polling mode for non-systemd environments. [FACT] The system supports systemd user services for automation, and a non-systemd polling option is documented for WSL.

## Prompt Library (Deterministic Prompt Assets)

[FACT] The prompt repository is a versioned prompt library for investment analysis, orchestration, and templates used by deterministic agents. [FACT] Prompts are organized into directories such as core modules, use cases, templates, orchestration bootstraps, and archived prompts. [FACT] The documented workflow is to select a prompt, supply required inputs/context via orchestration bootstraps, run analysis in a controlled agent, record prompt version metadata, and save evidence/outputs in a separate datastore.

[FACT] The prompt repository follows semantic versioning (MAJOR.MINOR.PATCH) and is private. [UNKNOWN] The exact integration points between the prompt library and the intake system are not described in the current documentation.

## Determinism and Governance Controls

[FACT] The intake pipeline emphasizes deterministic processing: a drop results in a reproducible set of artifacts with fixed formatting and consistent decision summary rules. [FACT] Decision summaries are derived strictly from `signals.json` and `routing.json`, with a documented precedence order for decision outcomes. [FACT] The system explicitly avoids investment advice, portfolio context, and execution logic.

[FACT] Governance artifacts and requirements are centralized in the governance repository. [FACT] PRs in code repos must reference ADR/spec/policy artifacts unless a `governance-exception` is applied. [FACT] A promotion pathway exists across Feature Development, Integration, Acceptance Testing, and Production, with CI and manual approval gates defined as the expected standard. [UNKNOWN] The current runtime environments for integration, acceptance, and production are not described in the intake or prompts repos, and there is no documented deployment topology beyond local/systemd usage.

## Non-Goals and Limitations

[FACT] The intake system has explicit non-goals: it does not perform valuation, pricing, return estimation, allocation recommendations, portfolio context, or execution actions. [FACT] It also avoids LLM inference in signals, routing, and decision summaries. [FACT] CSV normalization is currently generic; broker-specific heuristics (e.g., Fidelity/Vanguard-specific normalization) are not implemented.

[UNKNOWN] The system’s current throughput limits, performance characteristics, and error recovery behavior are not documented in the provided materials. [UNKNOWN] The extent of test coverage for each pipeline stage, beyond referenced CI checks, is not described in the provided documentation. [UNKNOWN] There is no documented data retention policy or artifact archival strategy beyond the local artifacts directory.

## Summary

[FACT] In its current state, FOBS provides a deterministic local intake pipeline for investment artifacts (PDFs and CSVs), producing structured artifacts, signals, routing decisions, and human-readable decision summaries with explicit non-goals and governance constraints. [FACT] It includes optional OCR remediation, a deterministic decision rule set, and layered outputs for recommendation and sizing guidance under strict gates. [FACT] It also includes a standalone, versioned prompt library with a defined human workflow for controlled analysis and evidence capture. [UNKNOWN] The production deployment topology, cross-repo integration details, and operational SLOs are not explicitly documented and would require further specification.
