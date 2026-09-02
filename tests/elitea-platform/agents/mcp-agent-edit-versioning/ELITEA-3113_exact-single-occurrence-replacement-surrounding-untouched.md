---
id: ELITEA-3113
title: "Exact Single-Occurrence Replacement Leaves Surrounding Text Byte-Identical"
priority: high
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3113: Exact Single-Occurrence Replacement Leaves Surrounding Text Byte-Identical

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** High · **Type:** Functional

**Objective:** Confirm that an exact single-occurrence `old_text` → `replacement` patch changes only the targeted phrase, and every other character of the instructions is byte-identical before and after.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | a short unique phrase |
| `replacement` | a different short phrase |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Capture the full current instructions text (before). | Baseline captured. |
| 2 | Perform a safe-patch replacing the unique phrase. | Call succeeds. |
| 3 | Capture the full new instructions text (after) and diff against before. | Only the targeted phrase differs; all surrounding text is byte-identical. |

---

## Expected Final State

The patch is a surgical, minimal-diff edit.

---

## Actual Result — 2026-09-02

**Pass.** Only the targeted phrase changed; surrounding text verified byte-identical.

---

## Pass/Fail Criteria

**Pass:** Only the targeted text differs.
**Fail:** Any unrelated text is altered, reordered, or whitespace-shifted.
