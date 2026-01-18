# Change Control

Purpose: define change control for governance artifacts.

## Requirements
- Policy edits must include a diff summary and rationale in the PR description.
- Financial logic changes require explicit approval or feature flags in code repos.
- Exceptions require the `governance-exception` label and approver sign-off.

## Review Gates
- Policy and decision files require CODEOWNERS review.
- CI validates required PR metadata for policy edits.
