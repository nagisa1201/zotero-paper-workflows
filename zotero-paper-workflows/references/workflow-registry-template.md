# Extending the workflow registry

When adding a later workflow, use this template:

## Workflow N — short name

- Trigger: the explicit user request that activates it.
- Depends on: earlier workflow numbers and required manifest fields.
- Inputs: exact Zotero items, files, or external sources.
- Ordered steps: numbered actions with mutation boundaries.
- Outputs: deterministic files, records, or attachments.
- Verification: authoritative checks proving the workflow is complete.
- Stop conditions: missing authority, unsafe mutation, unresolved identity, or failed quality gate.

Add the workflow to the numbered registry in `SKILL.md` and link its reference file. Do not turn a later workflow into an implicit shortcut around an earlier workflow.
