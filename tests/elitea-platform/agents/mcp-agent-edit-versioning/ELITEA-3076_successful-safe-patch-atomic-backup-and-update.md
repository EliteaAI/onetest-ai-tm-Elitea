---
id: ELITEA-3076
title: "Successful Safe-Patch Call Creates Exactly One Backup and Atomically Updates the Draft"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3076: Successful Safe-Patch Call Creates Exactly One Backup and Atomically Updates the Draft

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm a successful safe-patch call (a) creates exactly one new backup version named `mcp-backup-<version_id>-<timestamp>` containing the pre-edit instructions and full config, (b) updates the draft version's instructions, and (c) both happen atomically — both exist together, never just one.

---

## Preconditions

- Sandbox parent agent (#414) with a nested sub-agent (#415), a tag, and a variable configured on its draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| `old_text` | short unique phrase in current instructions |
| `replacement` | replacement text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Read `instructions_sha256` via `get_version_details`. | Hash obtained. |
| 2 | Call the safe patch tool with a valid `expected_instructions_sha256`, unique `old_text`, and `replacement`. | Call succeeds (2xx). |
| 3 | List versions for the agent. | Exactly one new version named `mcp-backup-<version_id>-<timestamp>` exists. |
| 4 | Inspect the backup version's instructions and config. | Contains the *pre-edit* instructions and the pre-edit toolkit/nested-agent/variable/tag config, unchanged. |
| 5 | Inspect the draft version. | Instructions now reflect the replacement; both backup and updated draft exist simultaneously. |

---

## Expected Final State

Backup and edit are both present after a successful call — never just one.

---

## Actual Result — 2026-09-02

**Pass.** Verified on sandbox agent #414: exactly one `mcp-backup-*` version created, pre-edit fidelity confirmed (toolkits/nested-agent/variables/tags carried over), draft updated atomically with both present.

---

## Pass/Fail Criteria

**Pass:** Exactly one accurate backup plus the correctly-updated draft, both present.
**Fail:** Backup missing, duplicated, missing pre-edit fidelity, or draft update missing/partial.
