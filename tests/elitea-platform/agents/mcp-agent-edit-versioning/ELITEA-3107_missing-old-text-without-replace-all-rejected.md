---
id: ELITEA-3107
title: "Safe-Patch Call Omitting old_text Without replace_all Is Rejected by Validation"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3107: Safe-Patch Call Omitting old_text Without replace_all Is Rejected by Validation

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a safe-patch call that omits `old_text` while `replace_all` is not set (or false) is rejected by request validation ("old_text is required unless replace_all is true"), with no backup created and no change applied.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | omitted |
| `replace_all` | omitted/false |
| `replacement` | any non-empty text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with `replacement` set, `old_text` omitted, `replace_all` omitted/false. | Validation error ("old_text is required unless replace_all is true"). |
| 2 | Re-read the draft version. | Instructions unchanged. |
| 3 | List versions. | No new backup created. |

---

## Expected Final State

Invalid payload shape is rejected before any DB work.

---

## Actual Result — 2026-09-02

**Pass.** Validation error returned as expected; no backup; no change.

---

## Pass/Fail Criteria

**Pass:** Correct validation error, zero side effects.
**Fail:** Call is accepted, or produces a partial/incorrect mutation.
