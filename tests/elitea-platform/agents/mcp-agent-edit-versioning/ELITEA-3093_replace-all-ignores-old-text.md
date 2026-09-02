---
id: ELITEA-3093
title: "replace_all Ignores/Does Not Require old_text to Match"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3093: replace_all Ignores/Does Not Require old_text to Match

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that when `replace_all: true` is set alongside a (non-matching or irrelevant) `old_text`, the entire instructions field is replaced by `replacement` regardless of `old_text`'s content, as long as the result isn't empty/no-op.

---

## Preconditions

- Sandbox agent (#414) with a draft version.

---

## Test Data

| Field | Value |
|-------|-------|
| `replace_all` | `true` |
| `old_text` | a phrase guaranteed **not** present in current instructions |
| `replacement` | new full instructions text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with `replace_all: true`, a non-matching `old_text`, and a valid `replacement`. | Call succeeds despite `old_text` not matching anything. |
| 2 | Inspect the resulting instructions. | Entirely equal to `replacement`; `old_text` had no bearing on the outcome. |

---

## Expected Final State

`old_text` is a no-op/ignored field whenever `replace_all` is true.

---

## Actual Result — 2026-09-02

**Pass.** Full-rewrite succeeded despite a non-matching `old_text`; resulting instructions equaled `replacement` exactly.

---

## Pass/Fail Criteria

**Pass:** `replace_all` succeeds independent of `old_text` content/match status.
**Fail:** Call fails or behaves differently based on `old_text` when `replace_all` is true.
