---
id: ELITEA-3086
title: "replace_all With Empty/Whitespace-Only Replacement Is Rejected"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3086: replace_all With Empty/Whitespace-Only Replacement Is Rejected

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm a safe-patch call with `replace_all: true` and an empty or whitespace-only `replacement` is rejected with a 409 ("Refusing to replace non-empty instructions with empty content"), leaving the draft and any prior backups untouched.

---

## Preconditions

- Sandbox agent (#414) with a draft version containing non-empty instructions.

---

## Test Data

| Field | Value |
|-------|-------|
| `replace_all` | `true` |
| `replacement` | `""` and, separately, `"   "` (whitespace-only) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with `replace_all: true`, `replacement: ""`. | 409 "Refusing to replace non-empty instructions with empty content." |
| 2 | Repeat with `replacement: "   "` (whitespace-only). | Same 409 rejection. |
| 3 | Re-read the draft version after both attempts. | Instructions unchanged. |
| 4 | List versions. | No new backups created by either attempt. |

---

## Expected Final State

Instructions can never be wiped to empty/whitespace via the patch tool, even in full-rewrite mode.

---

## Actual Result — 2026-09-02

**Pass.** Both empty and whitespace-only full-rewrite attempts were rejected with the expected 409 message; draft and prior backups untouched.

---

## Pass/Fail Criteria

**Pass:** Both cases rejected, zero side effects.
**Fail:** Either case succeeds in wiping instructions to empty/whitespace.
