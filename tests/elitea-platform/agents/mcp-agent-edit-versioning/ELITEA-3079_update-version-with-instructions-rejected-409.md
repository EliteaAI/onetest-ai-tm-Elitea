---
id: ELITEA-3079
title: "Internal-MCP update_version Including instructions Is Rejected With 409 Before Any DB Work"
priority: critical
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3079: Internal-MCP update_version Including instructions Is Rejected With 409

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm an internal-MCP `update_version` (PUT) call whose body includes `instructions` is rejected with HTTP 409 and a message directing the caller to the safe patch tool, with no backup created and no fields changed.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | sandbox parent agent (#414) |
| Payload | `update_version` body containing an `instructions` key |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Via internal MCP, call `update_version` with `instructions` present in the body. | 409 response, message references the safe instructions patch tool. |
| 2 | List versions for the agent. | No new `mcp-backup-*` version created. |
| 3 | Re-read the draft version. | Instructions and all other fields unchanged. |

---

## Expected Final State

The rejection happens before any DB mutation — no side effects of any kind.

---

## Actual Result — 2026-09-02

**Pass.** Call returned 409 with the expected redirect-to-safe-patch-tool message; no backup created; draft unchanged.

---

## Pass/Fail Criteria

**Pass:** 409 with correct message, zero side effects.
**Fail:** Any backup/field change occurs, or the wrong status/message is returned.
