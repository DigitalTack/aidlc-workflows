# Codex AI-DLC Entry Point

This file is the Codex entry point for the AI-DLC workflow.

## Load Workflow
- Load the workflow from `.codex/aidlc-rules/core-workflow.md`.
- Load rule details from `.codex/aidlc-rule-details/`.
- Ignore any legacy rules outside `.codex/` (do not load `.kiro` or `.amazonq` paths).

## Notes
- Follow the workflow exactly as written, including all mandatory logging, question formats, and content validation rules.
- Generate documentation artifacts only under `aidlc-docs/` as required by the workflow.
- Ensure audit logging is written to `aidlc-docs/audit.md` with raw user input and timestamps per the workflow rules.
- When asking questions, use the required multiple-choice format and [Answer]: tag per the question-format guide.
