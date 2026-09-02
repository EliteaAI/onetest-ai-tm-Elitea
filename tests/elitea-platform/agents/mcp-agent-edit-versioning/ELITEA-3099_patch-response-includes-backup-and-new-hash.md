---
id: ELITEA-3099
title: "Safe-Patch Response Includes mcp_backup_version and the New instructions_sha256"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3099: Safe-Patch Response Includes mcp_backup_version and the New instructions_sha256

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm the safe patch tool's success response includes `mcp_backup_version` (`{id, name}`) and the new `instructions_sha256`, so the calling model can reference the backup and chain further edits without re-reading.

---

## Preconditions

- Sandbox agent with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Perform a successful safe-patch call. | 2xx response. |
| 2 | Inspect the response body. | Contains `mcp_backup_version.id` and `mcp_backup_version.name` matching the actual created backup. |
| 3 | Inspect the response body further. | Contains `instructions_sha256` equal to `sha256()` of the newly-updated instructions. |

---

## Expected Final State

Response is self-sufficient — no extra read call needed to learn the backup identity or new fingerprint.

---

## Actual Result — 2026-09-02

**Pass.** Response included `mcp_backup_version` (matching the created backup) and the updated `instructions_sha256`.

---

## Pass/Fail Criteria

**Pass:** Both fields present and correct in the success response.
**Fail:** Either field missing, or values don't match the actual backup/new instructions.
