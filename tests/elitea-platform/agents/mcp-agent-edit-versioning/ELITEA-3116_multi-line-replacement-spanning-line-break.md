---
id: ELITEA-3116
title: "Exact Replacement Targeting Text That Spans a Line Break Works Correctly"
priority: medium
type: functional
module: mcp-agent-edit-versioning
status: draft
execution_type: manual
tags: [feat:agents, int:mcp, issue:6018, api]
requirements: [EliteaAI/elitea_issues#6018]
---

# ELITEA-3116: Exact Replacement Targeting Text That Spans a Line Break Works Correctly

**Module:** Agents / Internal MCP Agent Edit Versioning · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm a multi-line `old_text` (spanning at least one line break) is matched and replaced correctly, and is not silently normalized/trimmed in a way that breaks the match (e.g. line-ending or leading/trailing-whitespace differences).

---

## Preconditions

- Sandbox agent (#414) with a draft version whose instructions contain at least one multi-line block.

---

## Test Data

| Field | Value |
|-------|-------|
| `old_text` | a multi-line excerpt (e.g. two consecutive lines, newline included) |
| `replacement` | different multi-line text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the safe patch tool with a multi-line `old_text` matching an exact excerpt of the current instructions (including the internal line break). | Call succeeds. |
| 2 | Inspect the resulting instructions. | The multi-line block is replaced correctly; surrounding lines and line-ending style are unaffected. |

---

## Expected Final State

Multi-line exact matches work the same as single-line matches — no special-casing breaks them.

---

## Actual Result — 2026-09-02

**Pass.** Multi-line `old_text` spanning a line break matched and replaced correctly with no normalization issues observed.

---

## Pass/Fail Criteria

**Pass:** Multi-line match/replace succeeds, preserving surrounding formatting.
**Fail:** Match fails due to line-ending/whitespace normalization, or replacement corrupts surrounding lines.
