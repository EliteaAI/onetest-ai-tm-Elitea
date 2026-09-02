---
id: ELITEA-3109
title: "No-Op Replacement (Result Identical to Current Instructions) Is Rejected"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3109: No-Op Replacement Is Rejected

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a safe-patch call whose resulting instructions would be byte-identical to the current instructions (a no-op edit) is rejected with a 409 ("The patch would not change the instructions"), with no backup created.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | a phrase in current instructions |
| `replacement` | identical to `old_text` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with `old_text` and an identical `replacement`. | 409 "The patch would not change the instructions." |
| 2 | Re-read the draft version. | Instructions unchanged. |
| 3 | List versions. | No new backup created. |

---

## Expected Final State

No-op edits are rejected rather than silently creating a redundant, identical backup.

---

## Actual Result — 2026-09-02

**Pass.** 409 with the expected no-op message; no backup created.

---

## Pass/Fail Criteria

**Pass:** Correct 409 rejection, zero side effects.
**Fail:** Call succeeds, or a backup is created for a no-op edit.
